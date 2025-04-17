# 4 questions to ask

- Is the application right for containers? Or should be hosted on something like EC2
- Do you need those servers that are running your application or can you shift to something more serverless?
- Is the application AWS specific? If it is, might leverage services like ECS or Lambda
- How long does the code need to run?

# AWS Lambda

- Lambda loves roles: Whenever talking about credentials and Lambda, ensure you're attaching a role to the function
- Be familiar with Lambda triggers: Will see questions asking what can kick off a Lambda function. Know that S3 Event, Kinesis, and EventBridge are common triggers
- Lambda limitation: Function should short. Can allocate up to 10 GB of RAM and 15 min of runtime
- Any AWS API call: Can be trigger to kick off EventBridge rule. This is fater than trying to scrape through CloudTrail

# Containers and Images

- Open source = Kubernetes: Container management solution that can run in AWS and on-prem -> EKS, EKS anywhere
- Fargate can't work alone: To use Fargate, must using ECS or EKS. Keep in mind not all scenarios specify ECS or EKS, and they make it sound as if Fargate is a service by itself
-  Containers can encompass just about any workload. Generally, it's preferred to use containers rather than EC2 on the exam

# AWS Aurora Serverless

- On-demand or auto scaling database: Question about auto scaling databases should involve AWS Aurora Serverless databases
- Variable traffic or workloads: If designing a new application with unknown workloads or traffic spike to database -> Aurora Serverless
- Capacity planning: Questions mention capacity planning for a new application with database -> Aurora Serverless

# AWS X-Ray

- AWS X-Ray: Used to gain application insights using requests and responses of services and functions at different points in a application flow
- Traces and downstream response times -> AWS X-Ray
- Lambda or API Gateway insights -> X-Ray integration

# AWS AppSync

- Managed GraphQL: Managed GrapQL interfact for any frontend application -> AppSync