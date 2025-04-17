           [[Automation]]

## CloudFormation

- Understand CloudFormation sections. Need to know what the parameters, mappings, and resource sections of the CloudFormation templates do. Just need to know use case for the parameter
- If questions asking the end user who's building the template. The mappings, how they can control or automatically fill in a value such as what is the particular AMI that I would like to use for this region, and the resource section (instances, networks, databases)

- Immutable architecture is preferable. Select answers that favor having resources than can be replaced at anytime. Stateless is better than stateful on the exam

- Mapping and parameter Store can be useful to help make templates more flexible. Hardcoded IDs (e.g., AMI or snapshot ID) are a source of problem.

## Elastic Beanstalk and Systems Manager
### Elastic Beanstalk

- Is a **one-stop shop** for all thing AWS. Questions looking for a simple solution to bundle and deploy applications should favor this over CloudFormation
- Automation documents are the primary method used in scenarios asking to configure the inside of an EC2 instances
- Don't go too deep on Systems Manager. While it has a lot of options, this text will focus on Automation documents, Parameter Store, and possibly Session Manager

Focus on using Automation documents to control thing inside of AWS account and inside of EC2 instances