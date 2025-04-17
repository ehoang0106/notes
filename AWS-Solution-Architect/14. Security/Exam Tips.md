[[Security]]


## 1. AWS CloudTrail

CloudTrail allows
- After-the-fact incident investigation
- Near real-time instruction detection
- Industry and regulatory compliance

***Remember that CloudTrail is basically just CCTV for your AWS account. It logs all API calls made to AWS account and stores logs in S3***

## 2. AWS Shield

Only protect layer 3 and 4 and used to protect against DDoS.]

Advanced subscribe costs $3,000/month

## 3. AWS WAF

- Allow all request except the ones you specific
- Block all requests except the ones you specific
- Count the request that match the properties you specific

WAF only block at layer 7 as well as thing like SQL injections and cross-site scripting

If you need to block access to specific countries or IP address -> AWS WAF

## 4. AWS Firewall Manager

Scenario about multiple AWS accounts and resources that need to be secured centrally -> AWS Firewall Manager

## 5. AWS GuardDuty

- Uses AI to learn what normal behavior looks like and alert of any abnormal or malicious behavior
- Monitor CloudTrail logs, VPC Flow Logs, and DNS logs
- Finding appear in the GuardDuty dashboard. CloudWatch Events can be used to trigger a Lambda function to address a threat

## 6. AWS Macie

- Uses AI to analyze data in S3 and helps identify PII, PHI, and financial data
- Great for HIPAA and GDPR compliance as well as preventing identify theft
- Macie alert can be sent to Amazon EventBridge and integrated

## 7. AWS Inspector

- It's used to perform vulnerability scan on both EC2 instances and VPCs

## 8. KMS and CloudHSM

- KMS is a managed service that can help create and control the encryption keys used to encrypt data
- Start using service by requesting the creation of CMK (custom master key)
- 3 ways to generate CMK: Amazon creates for us, import our own key management infra and have the key material generated and used in CloudHSM cluster
- 3 ways to control permission: Use the key policy. Use IAM policies in combination with the key policy
- Use grants in combination with the key policy.
##### * **See KMS vs CloudHSM***

## 9. Secrets Manager

- Used to store your application secrets: database credentials, API keys, SSH keys, password, etc.
- Application use the Secrets Manager API
- Rotating credentials
- When enabled, SM will rotate credentials immediately

## 10. Presigned URL
- Share private files in S3 bucket without public the bucket

## 11. Advanced IAM Policies

- Remember *not explicitly allowed* == **implicitly denied**
- Explicit deny > everything else
- Only attached policies have effect
- AWS joins all applicable policies

## 12. AWS Certificate Manager

- Integration with SSL certificates
- Integrates with ELB, CloudFront, API Gateway
- Free service, auto renew your SSL certificates (rotate old certificate)

## 13. AWS Audit Manager

- HIPPA or GDPR compliance -> Audit Manager

## 14. AWS Artifact 

- Compliance report

## 15. Cognito

- Authentication without custom code

## 16. AWS Detective

- Distract answer
- Scan EC2 and container for software vulnerabilities and unintended network

## 17. Network Firewall

- Filter network traffic before reach to internet gateway
- Block specific countries or IP address

## 18. AWS Security Hub

- Single place to view all security alert across mutiple AWS security services and AWS accounts

