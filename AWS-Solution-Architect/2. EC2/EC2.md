[[EC2]] [[AWS]]
EC2 (Elastic Compute)

## Pricing

- On-demand: Pay by the hour or the second, depending on the type of instance you run
- Reserved: Reserved capacity for 1 or 3 years.
- Spot: Purchase unused capacity at a discount of up to 90%. Prices fluctuate with supply and demand
- Dedicated: A physical EC2 server dedicated for your use. The most expensive option


### On-Demand Instances

- **Flexible**: Low cost and flexibility of EC2 without any upfront cost or long-term commitment
- **Short-term**: Applications with short-term, or unpredictable workloads that cannot be interrupted
- **Testing the water:** Applications being developed or tested on EC2 first time

### Reserved Instances
	Commit to 1 or 3 years to use a specific amount of compute power

- **Predictable usage**: Applications with steady state or predictable usage
- **Specific capacity requirements**: Application that require reserved capacity
- **Pay up front**: Make upfront payments to reduce the total computing costs even further

There are 3 type of RIs:
- ***Standard***: Up to 72% off the on-demand price
- ***Convertible***: Up to 54% off the-demand price. Has the option to change to a different RI type of equal or greater value
- ***Schedule***: Launch within the time window you define. Match your capacity reservation to a predictable recurring schedule that only requires a fraction of a day, week or month

*Reserved instance operate at a regional level*
Example: When you reserve an instance in say us-east-1, you are just doing that inside us-east-1. You can't take that reservation and apply it to Japan or Paris, etc.

### Spot Instances
- Use spot instance when have start and end times
- Applications that are only feasible at very low compute prices
- Users with an urgent need for large amount of additional computing capacity

### Dedicated Host

**Compliance**: Regulatory requirements that may not support multi-tenant virtualization
**On-demand**: 
**Licensing**: Great for licensing that does not support milt-tenancy or cloud deployment
**Reserved**: Can be purchased as a reservation for up to 70% off the on-demand price


## Exam tips

Any question that talk about special licensing requirements or compliance requirements, think about dedicated host