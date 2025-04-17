[[AWS]], [[SNS]]

## Amazon SNS

SNS is a push-based messaging service. It delivers messages to the endpoints that are subscribed to it

### Large message payloads

SNS Extended Library allows for sending messages up to 2 GB in size.
The payload is stored in S3, then SNS publishes a reference to the object

### SNS Fanout

- Messages published to SNS topic are replicated to multiple endpoint subscriptions

# Exam Tips

- For any scenarios require real-time alerting, think Amazon SNS
- Push-based message application, think SNS
- Be familiar with different subscriber options such as, SQS, Lambda, emails, HTTP endpoint
- SNS only support custom retry policies for HTTP(s) endpoints
- FIFO topics support ordering and deduplication
