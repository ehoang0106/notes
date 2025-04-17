
## 4 Questions to ask in the Exam

- **Is it highly available?**
-> Always want to pick answers that include high availability. Even if the question isn't specifically asking is this solution high availability

- **Which is appropriate for the situation: Horizontal or Vertical?**
-> Focus on Horizontal Scaling because we can continue to spin up more resources

- **Is it cost effective?**
-> Even if the question is not specifically asking for a cost effective solution, we want to keep cost in mind. Might be seen a questions that says: how do we scale out this architecture?

- **Would switching databases fix the problem or could we switch the DB?**
-> Yes

## Auto scaling questions

What to know for the exam:

- **Auto scaling is only for EC2**, no other service can be scaled using auto scaling. Other service might have a built-in option, but they aren't included in ASG.

- **Select the answer Get ahead of the workload**. Whenever possible, favor solutions that re predictive than reactive. 

- **Bake AIMs to reduce build times**. You can avoid long provisioning times by putting everything in an AMI. This is better than using user data whenever possible. 
-> Scenarios: Talk about how do we better fine tune or tweak our ASG or the EC2 takes to long to come online, and you have really long provisioning time time, and cause the issue when you need those EC2 to respond to a workload -> **Bake everything inside of that AMI**
-> Pick the answer with **short provisioning time whenever possible**


- **Spread out**. Make sure you're always spreading your ASG over multi-AZs

- **Steady state group**: allow us to create a situation where the failure of a legacy codebase or resource that can't be scaled can automatically from failure

- **ELBs are essential**. ELB is a best friend of ASG. Make sure enable health checks from load balancers - otherwise, instances won't be terminated and replaced when they fail health checks

## Scaling Databases

- **RDS** has the most database scaling options
- **Horizontal scaling** is usually preferred over vertical
- **Read replicas** are your friend
- **DynamoDB scaling** comes down to access patterns (provisioned or on-demand)