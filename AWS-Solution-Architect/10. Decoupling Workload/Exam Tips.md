4 questions to ask in Exam:
- Is it synchronous or asynchronous workload?
- What type of decoupling makes sense?
- Does the order of messages matter?
- What type of application load will you see?
## SQS

- SQS can duplicate messages: This is only once in a while, so if it's happening consistency misconfigured visibility timeout or if the developer is failing to make the delete API call
- Queue are not bi-directional: If you need communication to return to the instance that sent the message, you will need a second queue
- Know the default: Understand the standard values for all the SQS settings
- Nothing lasts forever: Messages in SQS up to 14 days
- Does order matter? If message ordering is important, SQS FIFO
## SNS and API Gateway

- Proactive notification = SNS: Anytime a question asks about email, text, or any type of push-based notification, SNS
- CloudWatch <3 SNS:
- API Gateway: Don't need to in-depth understanding. Only need to know it acts as a secure front door to external communication coming to our environment
## AWS Batch

- Long-running, batched workloads: Anything related to batch workloads that is long-running (? 15 min) will likely involve AWS Batch. Because execution time of Lambda limited at 15 min
- Queued workloads: If you  see a question about batch workloads requiring queues, then think AWS Batch
- On-demand alternative to AWS Lambda

## Amazon MQ

- Managed messaging broker: If there is any mention of managed broker service, think Amazon MQ
- Support RabbitMQ and ActiveMQ: Any mention of these two, Amazon MQ
- Specific messaging protocol: If see JMS, AMQP 0-9-1, AMPQ 1.0, MQTT, OpenWire, or STOMP -> AWS MQ

## AWS Step Function

- Serverless orchestration service: Any questions with this saying will likely involve AWS Step
- Different workflow decision requirements: Whenever the answer require different state or logic during workflows (e.g: condition check, failure catches) -> Step functions

## AWS AppFlow

- SaaS data ingestion (tieu thu): For architectures requiring simplified data ingestion -> AppFlow
- Support **Bi-directional**
- 