# ─────────────────────────────────────────────────────────────────────────────
# AWS ERP Three‑Tier (IIS + .NET 4.8 API + SQL Server) — Terraform Starter
# One‑region, multi‑AZ, production‑ready baseline with ALB + path routing.
#
# Files in this single snippet are separated with big headers like:
#   === FILE: variables.tf ===
# Copy each section into separate files inside a new Terraform folder.
#
# Requirements:
# - Terraform >= 1.4
# - AWS provider ~> 5.0
# - An existing ACM certificate in the same region for the ALB HTTPS listener
# - Optional: existing Route53 hosted zone if you want DNS
#
# Notes:
# - RDS engine defaults to sqlserver-web (license-included) for broad compatibility.
#   Adjust to sqlserver-se if your account/region supports it. Multi-AZ enabled.
# - User data installs IIS and enables basic features on front-end; API tier has .NET 4.8 features.
# - Replace placeholders marked with TODO.
# - For internal (private) app, set ALB to internal and front with VPN/Direct Connect.
# - This is a starter; tune sizes, tags, and hardening as needed.
# ─────────────────────────────────────────────────────────────────────────────

# === FILE: versions.tf ===
terraform {
  required_version = ">= 1.4.0"
  required_providers {
    aws = {
      source  = "hashicorp/aws"
      version = "~> 5.0"
    }
    random = {
      source  = "hashicorp/random"
      version = "~> 3.6"
    }
  }
}

# === FILE: providers.tf ===
provider "aws" {
  region = var.region
}

# === FILE: variables.tf ===
variable "project" { type = string  default = "erp" }
variable "environment" { type = string  default = "prod" }
variable "region" { type = string  default = "us-west-2" }

variable "vpc_cidr" { type = string  default = "10.20.0.0/16" }
variable "az_count" { type = number  default = 2 }

variable "public_subnet_cidrs" {
  description = "List of CIDRs for public subnets (one per AZ)"
  type        = list(string)
  default     = ["10.20.0.0/24", "10.20.1.0/24"]
}

variable "app_subnet_cidrs" {
  description = "List of CIDRs for app (IIS/API) private subnets"
  type        = list(string)
  default     = ["10.20.10.0/24", "10.20.11.0/24"]
}

variable "db_subnet_cidrs" {
  description = "List of CIDRs for database private subnets"
  type        = list(string)
  default     = ["10.20.20.0/24", "10.20.21.0/24"]
}

variable "alb_certificate_arn" {
  description = "ACM certificate ARN in the same region for the ALB 443 listener"
  type        = string
}

variable "route53_zone_id" {
  description = "Hosted Zone ID for Route 53 (optional)"
  type        = string
  default     = ""
}

variable "app_domain" {
  description = "FQDN for the ERP app (optional if no Route53)"
  type        = string
  default     = "app.example.com"
}

variable "key_name" {
  description = "EC2 key pair name for emergency access (optional if using SSM)"
  type        = string
  default     = null
}

variable "iis_instance_type" { type = string  default = "m6i.large" }
variable "api_instance_type" { type = string  default = "m6i.large" }

variable "iis_desired_capacity" { type = number default = 2 }
variable "api_desired_capacity" { type = number default = 2 }

variable "rds_instance_class" { type = string  default = "db.m6i.large" }
variable "rds_engine_edition" {
  description = "sqlserver-web or sqlserver-se"
  type        = string
  default     = "sqlserver-web"
}
variable "rds_allocated_storage" { type = number default = 100 }
variable "rds_multi_az" { type = bool default = true }

# If you already manage the password elsewhere, set create_db_secret = false and supply rds_master_password.
variable "create_db_secret" { type = bool default = true }
variable "rds_master_username" { type = string default = "erp_admin" }
variable "rds_master_password" {
  type      = string
  default   = null
  sensitive = true
}

variable "tags" {
  type = map(string)
  default = {
    Application = "ERP"
  }
}

# === FILE: data_windows_ami.tf ===
# Use the SSM parameter for latest Windows Server 2022 English Full Base AMI
data "aws_ssm_parameter" "win2022_base" {
  name = "/aws/service/ami-windows-latest/Windows_Server-2022-English-Full-Base"
}

# === FILE: networking.tf ===
resource "aws_vpc" "main" {
  cidr_block           = var.vpc_cidr
  enable_dns_hostnames = true
  enable_dns_support   = true
  tags = merge(var.tags, {
    Name = "${var.project}-${var.environment}-vpc"
  })
}

resource "aws_internet_gateway" "igw" {
  vpc_id = aws_vpc.main.id
  tags   = { Name = "${var.project}-${var.environment}-igw" }
}

# Get AZs deterministically
data "aws_availability_zones" "available" { state = "available" }

# Public subnets + route tables
resource "aws_subnet" "public" {
  for_each = { for idx, cidr in var.public_subnet_cidrs : idx => cidr }
  vpc_id                  = aws_vpc.main.id
  cidr_block              = each.value
  availability_zone       = data.aws_availability_zones.available.names[tonumber(each.key)]
  map_public_ip_on_launch = true
  tags = { Name = "${var.project}-${var.environment}-public-${each.key}" }
}

resource "aws_route_table" "public" {
  vpc_id = aws_vpc.main.id
  tags   = { Name = "${var.project}-${var.environment}-public-rt" }
}

resource "aws_route" "public_internet" {
  route_table_id         = aws_route_table.public.id
  destination_cidr_block = "0.0.0.0/0"
  gateway_id             = aws_internet_gateway.igw.id
}

resource "aws_route_table_association" "public_assoc" {
  for_each       = aws_subnet.public
  subnet_id      = each.value.id
  route_table_id = aws_route_table.public.id
}

# NAT per AZ for resilience
resource "aws_eip" "nat" {
  for_each = aws_subnet.public
  domain   = "vpc"
  tags     = { Name = "${var.project}-${var.environment}-nat-${each.key}" }
}

resource "aws_nat_gateway" "nat" {
  for_each      = aws_subnet.public
  subnet_id     = each.value.id
  allocation_id = aws_eip.nat[each.key].id
  tags          = { Name = "${var.project}-${var.environment}-nat-${each.key}" }
  depends_on    = [aws_internet_gateway.igw]
}

# Private app subnets (IIS/API)
resource "aws_subnet" "app" {
  for_each            = { for idx, cidr in var.app_subnet_cidrs : idx => cidr }
  vpc_id              = aws_vpc.main.id
  cidr_block          = each.value
  availability_zone   = data.aws_availability_zones.available.names[tonumber(each.key)]
  map_public_ip_on_launch = false
  tags = { Name = "${var.project}-${var.environment}-app-${each.key}" }
}

resource "aws_route_table" "app" {
  for_each = aws_subnet.app
  vpc_id   = aws_vpc.main.id
  tags     = { Name = "${var.project}-${var.environment}-app-rt-${each.key}" }
}

resource "aws_route" "app_to_internet_via_nat" {
  for_each               = aws_route_table.app
  route_table_id         = each.value.id
  destination_cidr_block = "0.0.0.0/0"
  nat_gateway_id         = aws_nat_gateway.nat[each.key].id
}

resource "aws_route_table_association" "app_assoc" {
  for_each       = aws_subnet.app
  subnet_id      = each.value.id
  route_table_id = aws_route_table.app[each.key].id
}

# Private DB subnets
resource "aws_subnet" "db" {
  for_each            = { for idx, cidr in var.db_subnet_cidrs : idx => cidr }
  vpc_id              = aws_vpc.main.id
  cidr_block          = each.value
  availability_zone   = data.aws_availability_zones.available.names[tonumber(each.key)]
  map_public_ip_on_launch = false
  tags = { Name = "${var.project}-${var.environment}-db-${each.key}" }
}

resource "aws_db_subnet_group" "db" {
  name       = "${var.project}-${var.environment}-db-subnets"
  subnet_ids = [for s in aws_subnet.db : s.id]
  tags       = { Name = "${var.project}-${var.environment}-db-subnets" }
}

# === FILE: security_groups.tf ===
# SG: ALB (ingress 80/443 from world)
resource "aws_security_group" "alb" {
  name        = "${var.project}-${var.environment}-alb-sg"
  description = "ALB SG"
  vpc_id      = aws_vpc.main.id

  ingress { from_port = 80  to_port = 80  protocol = "tcp" cidr_blocks = ["0.0.0.0/0"] }
  ingress { from_port = 443 to_port = 443 protocol = "tcp" cidr_blocks = ["0.0.0.0/0"] }

  egress  { from_port = 0   to_port = 0   protocol = "-1" cidr_blocks = ["0.0.0.0/0"] }

  tags = { Name = "${var.project}-${var.environment}-alb-sg" }
}

# SG: IIS (only from ALB)
resource "aws_security_group" "iis" {
  name        = "${var.project}-${var.environment}-iis-sg"
  description = "IIS tier SG"
  vpc_id      = aws_vpc.main.id

  ingress {
    description     = "ALB to IIS"
    from_port       = 80
    to_port         = 80
    protocol        = "tcp"
    security_groups = [aws_security_group.alb.id]
  }

  # Optional RDP via SSM tunnel only; no direct 3389 from internet
  egress { from_port = 0 to_port = 0 protocol = "-1" cidr_blocks = ["0.0.0.0/0"] }
  tags = { Name = "${var.project}-${var.environment}-iis-sg" }
}

# SG: API (from ALB or IIS depending on routing)
resource "aws_security_group" "api" {
  name        = "${var.project}-${var.environment}-api-sg"
  description = "API tier SG"
  vpc_id      = aws_vpc.main.id

  ingress {
    description     = "ALB to API (/api/* path)"
    from_port       = 80
    to_port         = 80
    protocol        = "tcp"
    security_groups = [aws_security_group.alb.id]
  }

  # If IIS calls API privately (not via ALB), also allow IIS SG
  ingress {
    description     = "IIS to API direct (optional)"
    from_port       = 80
    to_port         = 80
    protocol        = "tcp"
    security_groups = [aws_security_group.iis.id]
  }

  egress { from_port = 0 to_port = 0 protocol = "-1" cidr_blocks = ["0.0.0.0/0"] }
  tags = { Name = "${var.project}-${var.environment}-api-sg" }
}

# SG: DB (only from API)
resource "aws_security_group" "db" {
  name        = "${var.project}-${var.environment}-db-sg"
  description = "DB tier SG"
  vpc_id      = aws_vpc.main.id

  ingress {
    description     = "API to SQL Server"
    from_port       = 1433
    to_port         = 1433
    protocol        = "tcp"
    security_groups = [aws_security_group.api.id]
  }

  egress { from_port = 0 to_port = 0 protocol = "-1" cidr_blocks = ["0.0.0.0/0"] }
  tags = { Name = "${var.project}-${var.environment}-db-sg" }
}

# === FILE: iam_ssm.tf ===
# EC2 role with SSM permissions and CloudWatch agent
resource "aws_iam_role" "ec2_role" {
  name = "${var.project}-${var.environment}-ec2-role"
  assume_role_policy = jsonencode({
    Version = "2012-10-17",
    Statement = [{
      Effect = "Allow",
      Principal = { Service = "ec2.amazonaws.com" },
      Action = "sts:AssumeRole"
    }]
  })
}

resource "aws_iam_role_policy_attachment" "ssm_core" {
  role       = aws_iam_role.ec2_role.name
  policy_arn = "arn:aws:iam::aws:policy/AmazonSSMManagedInstanceCore"
}

resource "aws_iam_role_policy_attachment" "cw_agent" {
  role       = aws_iam_role.ec2_role.name
  policy_arn = "arn:aws:iam::aws:policy/CloudWatchAgentServerPolicy"
}

resource "aws_iam_instance_profile" "ec2_profile" {
  name = "${var.project}-${var.environment}-ec2-profile"
  role = aws_iam_role.ec2_role.name
}

# === FILE: alb.tf ===
resource "aws_lb" "app" {
  name               = "${var.project}-${var.environment}-alb"
  internal           = false # set true if private-only
  load_balancer_type = "application"
  security_groups    = [aws_security_group.alb.id]
  subnets            = [for s in aws_subnet.public : s.id]
  enable_deletion_protection = false
  tags = { Name = "${var.project}-${var.environment}-alb" }
}

resource "aws_lb_target_group" "tg_iis" {
  name     = "${var.project}-${var.environment}-tg-iis"
  port     = 80
  protocol = "HTTP"
  vpc_id   = aws_vpc.main.id
  health_check {
    path                = "/"
    matcher             = "200-399"
    interval            = 30
    unhealthy_threshold = 2
    healthy_threshold   = 3
    timeout             = 5
  }
}

resource "aws_lb_target_group" "tg_api" {
  name     = "${var.project}-${var.environment}-tg-api"
  port     = 80
  protocol = "HTTP"
  vpc_id   = aws_vpc.main.id
  health_check {
    path                = "/health" # TODO: implement health endpoint in API
    matcher             = "200-399"
    interval            = 30
    unhealthy_threshold = 2
    healthy_threshold   = 3
    timeout             = 5
  }
}

resource "aws_lb_listener" "https" {
  load_balancer_arn = aws_lb.app.arn
  port              = 443
  protocol          = "HTTPS"
  ssl_policy        = "ELBSecurityPolicy-2016-08"
  certificate_arn   = var.alb_certificate_arn

  default_action {
    type             = "forward"
    target_group_arn = aws_lb_target_group.tg_iis.arn
  }
}

resource "aws_lb_listener_rule" "api_path" {
  listener_arn = aws_lb_listener.https.arn
  priority     = 10

  action {
    type             = "forward"
    target_group_arn = aws_lb_target_group.tg_api.arn
  }

  condition {
    path_pattern { values = ["/api/*"] }
  }
}

# Optional HTTP -> HTTPS redirect
resource "aws_lb_listener" "http_redirect" {
  load_balancer_arn = aws_lb.app.arn
  port              = 80
  protocol          = "HTTP"

  default_action {
    type = "redirect"
    redirect {
      port        = "443"
      protocol    = "HTTPS"
      status_code = "HTTP_301"
    }
  }
}

# === FILE: route53.tf ===
resource "aws_route53_record" "app_alias" {
  count   = var.route53_zone_id == "" ? 0 : 1
  zone_id = var.route53_zone_id
  name    = var.app_domain
  type    = "A"
  alias {
    name                   = aws_lb.app.dns_name
    zone_id                = aws_lb.app.zone_id
    evaluate_target_health = true
  }
}

# === FILE: user_data_iis.ps1.tpl ===
#cloud-config
# (Note: EC2 Windows ignores cloud-config syntax; keeping as a visual separator)
<powershell>
Install-WindowsFeature Web-Server, Web-Mgmt-Tools, Web-Http-Redirect, Web-Static-Content, Web-Http-Logging, Web-Request-Monitor
# Simple landing page so Target Group health checks pass
New-Item -ItemType Directory -Force -Path C:\inetpub\wwwroot
Set-Content -Path C:\inetpub\wwwroot\index.html -Value "<h1>ERP Front-End (IIS)</h1>"
</powershell>

# === FILE: user_data_api.ps1.tpl ===
<powershell>
# Install .NET Framework features needed for 4.8 apps
Install-WindowsFeature NET-Framework-45-Core, Web-Server, Web-WebServer
# Simple health endpoint
New-Item -ItemType Directory -Force -Path C:\inetpub\wwwroot
Set-Content -Path C:\inetpub\wwwroot\health.html -Value "healthy"
# Bind default site to port 80
</powershell>

# === FILE: compute_iis_api.tf ===
locals {
  win2022_ami_id = jsondecode(data.aws_ssm_parameter.win2022_base.value).ImageId
  common_tags    = merge(var.tags, { Environment = var.environment, Project = var.project })
}

# Launch template — IIS
resource "aws_launch_template" "iis" {
  name_prefix   = "${var.project}-${var.environment}-iis-"
  image_id      = local.win2022_ami_id
  instance_type = var.iis_instance_type
  key_name      = var.key_name

  iam_instance_profile { name = aws_iam_instance_profile.ec2_profile.name }

  user_data = base64encode(templatefile("${path.module}/user_data_iis.ps1.tpl", {}))

  vpc_security_group_ids = [aws_security_group.iis.id]

  block_device_mappings {
    device_name = "/dev/sda1"
    ebs {
      volume_size           = 80
      volume_type           = "gp3"
      delete_on_termination = true
      encrypted             = true
    }
  }
  tag_specifications {
    resource_type = "instance"
    tags          = merge(local.common_tags, { Role = "iis" })
  }
}

resource "aws_autoscaling_group" "iis" {
  name                      = "${var.project}-${var.environment}-iis-asg"
  min_size                  = 2
  max_size                  = 6
  desired_capacity          = var.iis_desired_capacity
  vpc_zone_identifier       = [for s in aws_subnet.app : s.id]
  health_check_type         = "ELB"
  health_check_grace_period = 300

  launch_template {
    id      = aws_launch_template.iis.id
    version = "$Latest"
  }

  target_group_arns = [aws_lb_target_group.tg_iis.arn]
  tag {
    key                 = "Name"
    value               = "${var.project}-${var.environment}-iis"
    propagate_at_launch = true
  }
}

# Launch template — API
resource "aws_launch_template" "api" {
  name_prefix   = "${var.project}-${var.environment}-api-"
  image_id      = local.win2022_ami_id
  instance_type = var.api_instance_type
  key_name      = var.key_name

  iam_instance_profile { name = aws_iam_instance_profile.ec2_profile.name }

  user_data = base64encode(templatefile("${path.module}/user_data_api.ps1.tpl", {}))

  vpc_security_group_ids = [aws_security_group.api.id]

  block_device_mappings {
    device_name = "/dev/sda1"
    ebs {
      volume_size           = 80
      volume_type           = "gp3"
      delete_on_termination = true
      encrypted             = true
    }
  }
  tag_specifications {
    resource_type = "instance"
    tags          = merge(local.common_tags, { Role = "api" })
  }
}

resource "aws_autoscaling_group" "api" {
  name                      = "${var.project}-${var.environment}-api-asg"
  min_size                  = 2
  max_size                  = 6
  desired_capacity          = var.api_desired_capacity
  vpc_zone_identifier       = [for s in aws_subnet.app : s.id]
  health_check_type         = "ELB"
  health_check_grace_period = 300

  launch_template {
    id      = aws_launch_template.api.id
    version = "$Latest"
  }

  target_group_arns = [aws_lb_target_group.tg_api.arn]
  tag {
    key                 = "Name"
    value               = "${var.project}-${var.environment}-api"
    propagate_at_launch = true
  }
}

# === FILE: rds_sqlserver.tf ===
# Optional: create a strong random password and store in Secrets Manager
resource "random_password" "db" {
  length  = 24
  special = true
}

resource "aws_secretsmanager_secret" "db" {
  count      = var.create_db_secret ? 1 : 0
  name       = "${var.project}/${var.environment}/sqlserver/credentials"
  kms_key_id = null
}

resource "aws_secretsmanager_secret_version" "db" {
  count     = var.create_db_secret ? 1 : 0
  secret_id = aws_secretsmanager_secret.db[0].id
  secret_string = jsonencode({
    username = var.rds_master_username,
    password = coalesce(var.rds_master_password, random_password.db.result)
  })
}

# Pull password from either variable or random
locals {
  db_master_password = var.create_db_secret ? jsondecode(aws_secretsmanager_secret_version.db[0].secret_string).password : var.rds_master_password
}

resource "aws_db_instance" "sql" {
  identifier              = "${var.project}-${var.environment}-sql"
  engine                  = var.rds_engine_edition         # sqlserver-web or sqlserver-se
  engine_version          = "15.00"                        # SQL Server 2019 family; let AWS choose minor
  license_model           = "license-included"
  instance_class          = var.rds_instance_class
  allocated_storage       = var.rds_allocated_storage
  storage_type            = "gp3"
  multi_az                = var.rds_multi_az
  db_subnet_group_name    = aws_db_subnet_group.db.name
  vpc_security_group_ids  = [aws_security_group.db.id]
  username                = var.rds_master_username
  password                = local.db_master_password
  backup_retention_period = 7
  deletion_protection     = true
  skip_final_snapshot     = false
  apply_immediately       = false
  storage_encrypted       = true
  auto_minor_version_upgrade = true
  monitoring_interval     = 60
  publicly_accessible     = false
  copy_tags_to_snapshot   = true
  maintenance_window      = "Sun:10:00-Sun:12:00"
  backup_window           = "07:00-09:00"
  tags = merge(local.common_tags, { Name = "${var.project}-${var.environment}-sql" })
}

# === FILE: outputs.tf ===
output "alb_dns_name" { value = aws_lb.app.dns_name }
output "alb_arn"      { value = aws_lb.app.arn }
output "iis_asg_name" { value = aws_autoscaling_group.iis.name }
output "api_asg_name" { value = aws_autoscaling_group.api.name }
output "rds_endpoint" { value = aws_db_instance.sql.address  sensitive = true }
output "rds_identifier" { value = aws_db_instance.sql.id }

# === FILE: README-quickstart.md ===
# Quickstart
# 1) Create a folder, paste each section into separate files as named above.
# 2) terraform init
# 3) terraform apply -var="alb_certificate_arn=arn:aws:acm:REGION:ACCOUNT:certificate/XXXXXXXX" \
#                    -var="route53_zone_id=Z123ABC" -var="app_domain=erp.example.com"
# 4) After apply, browse https://erp.example.com (or the ALB DNS) and you should see the IIS landing page.
#
# Deploying your app
# - Bake AMIs (Packer/EC2 Image Builder) or use CodeDeploy to push artifacts to IIS/API tiers.
# - Switch health_check.path in tg_api to your real /health endpoint.
#
# Hardening to add soon
# - WAF on ALB, SSM Parameter Store/Secrets for app settings, FSx for Windows (shared uploads), CloudWatch Logs agent, NAT cost tuning.
