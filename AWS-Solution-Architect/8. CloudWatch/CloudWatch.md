[[AWS]] [[CloudWatch]]

# CloudWatch Overview

CloudWatch is a monitoring and observability platform that was designed to give us insight into our AWS architecture. Allowing to monitor multiple level of our applications and identify potential issue

# Features

- **System Metrics**
- **Application metrics**: Installing CloudWatch agent
- **Alarms**

## Type of Metrics

### Metrics

- **Default**: These metrics are provided out of the box and do not require any additional work on your part to configure
	Default metrics: **CPU Utilization, Network Throughput**

- **Custom**: These metrics will need to be provided by using CloudWatch agent installed on the host
	Custom metrics: **EC2 Memory Utilization, EBS Storage Capacity**


## Exam tips

- CloudWatch is a **go to tool** anything monitor come up
- No default alarms defined. Anything you want to hear about must be created
- **Default vs Custom**: AWS can't see past the hypervisor level for EC2
- Managed services: The more managed a service is, the more checks you get out of the box
- **Basic vs. Detailed**: Basic is 5-minute intervals (not paying extra), whereas detailed is 1-minute (have to pay extra)
