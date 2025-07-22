
| Item                 | Should Be                        |
| -------------------- | -------------------------------- |
| Private subnet route | `0.0.0.0/0 → NAT Gateway`        |
| NAT Gateway          | In public subnet, EIP attached   |
| Public subnet route  | `0.0.0.0/0 → IGW`                |
| Private EC2 SG       | Outbound: allow 0.0.0.0/0        |
| VPC DNS settings     | Both DNS options enabled         |
| NACLs                | Allow outbound/inbound as needed |
