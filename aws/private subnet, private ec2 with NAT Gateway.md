require:
- 2 `subnets` one `public` and one `private`
- `NAT Gateway`in the public subnet with EIP
- 2 route table: 1 route table for public subnet with internet gateway, 1 route table for private with NAT Gateway
- 

| Item                 | Should Be                        |
| -------------------- | -------------------------------- |
| Private subnet route | `0.0.0.0/0 → NAT Gateway`        |
| NAT Gateway          | In public subnet, EIP attached   |
| Public subnet route  | `0.0.0.0/0 → IGW`                |
| Private EC2 SG       | Outbound: allow 0.0.0.0/0        |
| VPC DNS settings     | Both DNS options enabled         |
| NACLs                | Allow outbound/inbound as needed |
