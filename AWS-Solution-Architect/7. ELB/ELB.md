[[AWS]] [[ELB]]

# ELB Overview

ELB automatically distributes incoming application traffic across multiple targets such as EC2, and can be done across AZs

## Application Load Balancer (LB)

- Best suited for load balancing of HTTP and HTTPS traffic. Operate at Layer 7 and are application aware.
- **For Intelligent LB

## Network LB

- Operating at connection level (Layer 4) on the OSI model. Network LB are cable of handling millions of request per second while maintaining ultra low latencies
- **For Performance LB**

## Gateway LB

(Hiem khi ra exam)
- Operating at network level on the OSI model (Layer 3). Use Gateway LB when deploying inline virtual appliances where network traffic is not destined for Gateway LB itself
- **For Inline Virtual Appliance Load Balancing**

## Classic LB

- Legacy LB. Use in test and dev when you are going and deploying to production. 
- Can load balance HTTP/HTTPS applications and use Layer 7-specific features such as X-Forwarded and sticky session
- **For dev/test load balancer**

## Health Checks

- All AWS load balancers can be configured with health checks.
- **The status of the instances that are healthy at time of the heath check is InService**
- **Unhealthy is OutOfService**

The load balancer routes request only to the healthy instances. When the LB determines an instance is unhealthy, it stop routing request to that instance and will resume request when healthy

## Exam tips

- Remember the different ELB types
- Use healthy to route traffic to instances or targets that are healthy
