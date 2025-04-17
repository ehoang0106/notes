
[[Migration]]

## 4 Questions to Ask

- Where are we going? Moving data from on-prem to AWS or AWS to on-prem, between cloud vendor or third-party SaaS from AWS?
- How do get there? Do we use Snowball device to do a bulk upload to Amazon or do we use a migration service like AWS DMS?
- Is it all at once? Do we leverage a Snowball device to move all of our data in one big move or do we migrate in small increments using replication for our servers?
- Or is it a partial migration? How do we want to partially migrate this?

### AWS Snow

- Snowball choices are often based on how much data you are moving.
- Snowcone and Snowmobile won't be on the exam as much
- When do we use Snowball? Best used in situation where you have slow to no internet. Snowball is faster and more secure in these situation
### Storage Gateway

- **Hybrid**: Anytime on-prem storage brought up, think: "Which version of Storage Gateway could complement this?"
- **Out of Space**: File Gateway prefect solution if your local network-attached storage is full
- It's a VM: Storage Gateway is run locally as a VM on-prem

### DataSync

- An agent-based that excels at on-time migrations or file shares into AWS
- EFS and FSx are bot viable locations for DataSync to transfer content into
- Transfer Family allows to use legacy files transfer protocols give older applications ability to read and write from S3

### Migration Hub

- Organizational tool to organize all your steps. You will need other tools to complete the migration though
- Database Migration Services is your go-to tool for any sort of database migration. Works for on-prem to cloud or moving data between different RDS databases
- Server Migration Services is the tool to migrate out of the data center and into AWS

### Application Discovery Service

- Quickly migrate entire application to AWS
- Agentless discovery can be used via OVA file deployment to vSphere
- Agent-based discovery collects detailed information of VMs on both Linux and Windows

### Application Migration Service

- AWS MGN
- Automated lift and shift service for migrating infrastructure to AWS
- Replicates source servers (VM, physical, or Azure VM) into AWS no non-disruptive
- RTO of minutes and RPO of sub-seconds