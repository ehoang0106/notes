
[[Governance]]

## 4 Questions to Ask in Exam

- Can it be centralized?
- How do we standardize?
- How do we enforce the standard?
- Are the users internal or external?

## What to Know for the Exam

- Service control policies (SCPs) have the ultimate say as to whether an API call goes through. They are the **only** way to restrict what the root account can do
- **Centralized logs** are always the right answer. CloudTrail offers support to log everything into a single AWS account
- **Isolating workloads** into a separate account is a great way to add more layers of security and controls. Avoid answer that lump everything together


### 3 Exam Tips for AWS Config

- **Standardization**: Anytime a "rule" needs to be set up for an account, think about using Config to check for compliance
- **Automate the Response**: Config offers to automatically remediate problems using Automation documents
- **Know what changed**: one-stop shop to see what changed. Provide history of all architecture