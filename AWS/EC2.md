# EC2


## Instance type
[https://aws.amazon.com/ec2/instance-types/](https://aws.amazon.com/ec2/instance-types/)
`m5.2xlarge`
- m: instance class
- 5: generation
- 2xlarge: size of the instance class

### General purpose
- Web servers
- Code repositories
### Compute optimised
- Batch processing workloads
- Media transcoding
- High performance web servers
- High performance computing
- Scientific modeling & machine learning
- Dedicated gaming servers
### Memory optimised
- High performance, relational/non-relational databases
- Distributed web scale cache stores
- In memory databases optimised for BI (Business Intelligence)
- Applications performing real-time processing of big unstructured data
### Storage Optimised
- High frequency online transaction processing (OLTP) systems
- Relational & and NoSQL databases
- Cache for in-memory databases (e.g. Redis)
- Data warehousing applications
- Distributed file systems

For more info:
https://instances.vantage.sh

## EC2 Instance purchasing options
### EC2 On demand
- Pay for what you use
	- Linux and Windows - billing per second after the first minute
	- All other Operating Systems - billing per hour
- Has the highest cost but not upfront payment
- No long-term commitment
- Recommended for short-term and un-interrupted workloads, where you can't predict the application will behave

### Reserved Instances
- Up to 72% discount compared to On-Demand
- You reserve a specific attribute (Instance type, Region, Tenancy, OS)
- Reserved period - 1 year (+ Discount) or 3 years (+++ discount)
- Payment options - No up-front (+ Discount), partial up-front (++ Discount), all up-front (+++ Discount)
- Reserved instance's scope - Regional or Zonal (reserved capacity in a AZ) 
- Recommended for steady state usage applications (tink database)
- You can buy and sell int the Reserved Instance Marketplace 
#### Convertible reserved instance
- Can change the EC2 instance type, instance family, OS, scope and tenancy
- Up to 66% discount

### EC2 Saving Plans
- Get a discount based on long-term usage (up to 72%)
- Commit to a certain type of usage ($10/hour for 1 or 3 years)
- Usage beyond EC2 Saving Plans is billed at the On-Demand price
- Locked to a specific instance family & AWS Region (e.g. M5 in eu-west-1)
- Flexible across:
	- Instance size (e.g. M5.xlarge, M5.2xlarge)
	- OS(e.g. Windows, Linux)
	- Tenancy (Host, Dedicated, Default)

### EC2 Spot Instances
- Can get a discount of up to 90% compared to On-Demand
- You can lose this instances at any point in time if your max price is below the current spot price
- These are the most cost-efficient instances in AWS
- Useful for workloads that are resilient to failure
	- Batch jobs
	- Data analysis
	- Image processing
	- Any distributed workloads
	- Workloads with a flexible start and end time
- Not suitable for critical jobs or databases

### EC2 Dedicated Hosts
- A physical server with EC2 capacity fully dedicated to your use
- Allows you to address compliance requirements and use you existing server bound software licenses (per-socket, per-core, per-VM software licenses)
- Purchasing options:
	- On Demand - pay per second per active dedicated host
	- Reserved  - 1 or 3 years (Not upfront, Partial up-front, All up-front)
- This is the most expensive option
- Useful for software that has complicated licensing model (BYOL - Bring Your Own License)
- Or for companies that have strong regulatory or compliance needs

### EC2 Dedicated Instances
- Instances run in hardware that is dedicated to you
- May share hardware with other instances in the same account 
- No control over instance placement (can move hardware after Stop/Start)

### EC2 Capacity Reservations
- Reserve On-Demand instances in a specific AZ for any duration
- You always have access to EC2 capacity when you need it
- Not time commitment (create/cancel any time), no billing discount
- Combine with Regional Reserved Instances and Saving Plans to benefit from billing discounts
- You are charged at On-Demand rate whether you run instances or not
- Suitable for sort-term, uninterrupted workloads that need to be in a specific AZ 

