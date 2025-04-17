[[AWS]] [[EBS]]
EBS: Elastic Block Store, the storage you can attach to EC2 Instances

## Mission Critical

1. Production Workloads: Designed for mission-critical workloads
2. Highly Available: Automatically replicated within a single AZ to protect against hardware failures
3. Scalable: Dynamically increase capacity and change the volume type with no downtime

## EBS Volume Types

### 1. SSD - General Purpose SSD IOPS

General Purpose SSD
#### a. gp2

General Purpose SSD (gp2). 

gp2 is good for boot volumes or development and test applications that are not latency sensitive

*IOPS: Input/Output Operation per second*
#### b. gp3

This is new generation replacing gp2. gp3 is 4 times faster than gp2.

gp3 is a ideal for applications that require high performance at a low cost, such as MySQL, Cassandra, virtual desktops, and Hadoop analytics

Customers looking for higher performance can scale up to 16,000 IOPS and 1,000 MiB/s for an additional fee.

#### c. io1 and io2

If you need more than 16,000 IOPS, think about io1 and io2. they are same price and they are latest generation with higher durability and more IOPS.

### 2. HDD - Throughput

#### a. Throughput Optimized HDD (st1)

- Low-cost HDD volume. 
- This is for frequently accessed, throughput-intensive workloads, big data, data warehouses. 
- But it cannot be a boot volume

#### b. Cold HDD (sc1)

- Lowest cost option. 
- Good choice for colder data requiring fewer scans per day. 
- Good for applications that need the lowest cost and performance is not a factor
- Also cannot be a boot volume


## Exam tips

- Just remember if you need more than `16,000 IOPS` per volume, you're gonna go from general purpose to IO intensive (io1 or io2)