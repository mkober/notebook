In 2002, [Peter Norvig](http://norvig.com/21-days.html#answers) published a list of timings for common computer operations like reading from disk. Later, these were memorialized as [latency numbers every programmer should know](https://colin-scott.github.io/personal_website/research/interactive_latency.html). In 2023, with cloud resources that cost real money, we are publishing a list of costs every programmer should know.

|   |   |
|---|---|
|Resource|Monthly Cost|
|10 GB data inter AZ|$0.10|
|10 GB blob storage|$0.50|
|10 GB attached storage|$0.80|
|10 GB data egress|$0.90|
|10 database IOPS|$1.00|
|10 custom metrics|$2.00|
|1 IPv4 address|$4.00|
|10 GB logs|$5.00|
|10 GB memory|$25.00|
|1 vCPU|$30.00|
|Redis server|$160.00|
|Postgres server|$180.00|
|1 GPU (A100)|$3,000.00|
|1 GPU (H100)|$9,000.00|

Cloud costs every programmer should know. [References](https://www.vantage.sh/blog/cloud-costs-every-programmer-should-know?utm_source=tldrnewsletter#cost-estimation-references).

The explanations and calculations for these costs are below, with some estimates of what applications look like scaled out.

How to use these costs

Knowing these numbers will help programmers quickly make back-of-the-napkin cost estimations for a variety of different projects. Once you have an idea of the architecture and size of the completed project, you can calculate the ballpark cost quickly, and without needing any complex cost calulator.

Kubernetes

Project specs: Kubernetes cluster with 12 pods (four cores each), 64 GB of memory, and 200 custom metrics

Twelve pods with four cores each is a total of 48 cores. Looking at our table, we can estimate the total cost of the cores to be $1,440.

Add 64 GB of memory (8 GB is roughly $20, so total would be $160) and 200 custom metrics (100 custom metrics is roughly $20, so total would be $40).

The total approximate cost of this project would be $1,640 per month.

Postgres deployment

Project specs: A large Postgres server (64 cores) and 5 TB of attached storage. Backups of 10 TB to blob storage, and 1 TB of logs

1. The Postgres server needs 64 cores. Given that 2 cores cost $60, 64 cores will cost (64/2) * $60 = $1920.
2. The project requires 5 TB of attached storage. Given that 100 GB costs $8, 5 TB (or 5000 GB) will cost (5000/100)* $8 = $400.
3. Backups of 10 TB to blob storage are needed. Given 1 TB costs $50, 10 TB will cost 10 * $50 = $500.
4. Finally, 1 TB of logs are required. From the provided assumption, 10 GB of logs cost $5. So 1 TB (or 1000 GB) will cost (1000/10) * $5 = $500.

The total approximate cost of this project would be $3,320 per month.

Self-managed Kafka

Project specs: Kafka, the popular event streaming service, can be self-managed if not using [MSK or Confluent](https://www.vantage.sh/blog/amazon-msk-confluent-pricing-comparison). Our Kafka service will stream a decent amout of data, so we’ll estimate 20 TB of cross AZ traffic with five 32-core machines.

1. The Kafka service will use five 32-core machine. From the previous assumptions, two cores cost $60, so 160 total cores will cost (160/2) * $60 = $4,800.
2. The project will use 20 TB of cross AZ traffic. From the assumptions, 1 TB of data inter AZ costs $10, so 20 TB will cost 20 * $10 = $200.

The total approximate cost of this project would be $5,000 per month.

Cost Estimation References

Note: Most services below have a free tier but we are not taking that into consideration. Most large cloud deployments will also come with discounts such as EDPs, Savings Plans, Reservations and other instruments. In many cases, these discounts will be transparent to you as a developer. If these are in place in some form you can apply a 50% discount to the compute estimates below.

10 GB data inter AZ

Inter AZ traffic is most likely being done by the systems running your applications instead of the applications themselves. Things like database replication, [event streaming](https://www.confluent.io/blog/understanding-and-optimizing-your-kafka-costs-part-1-infrastructure/#networking), and backups all consume inter AZ networking costs. Compared to data egress, we’ll make the assumption that there’s 10X more data flowing within the region than out of it.

Fortunately, traffic between availability zones is 10X cheaper than traffic leaving the cloud, at $10 per TB per month, or $0.10 per 10 GB per month.

10 GB blob storage

Using [Cloudflare’s R2 calculator](https://r2-calculator.cloudflare.com/) we’ll say we have 10 GB in S3 with 500K reads and 50K writes per month. It’s important to include reads and writes because S3 charges for “operations”. This comes out to $0.53 per month, or $0.50 per 10 GB per month.

As a reminder, in Cloudflare’s model is to [only a charge for storage](https://www.vantage.sh/blog/cloudflare-r2-aws-s3-comparison). Reads and writes are free.

10 GB attached storage

[EBS](https://handbook.vantage.sh/aws/services/ebs-pricing/) charges for storage and bandwidth consumed. At $0.08 per GB for GP3 and $0.10 per GB for GP2 we’ll say that roughly every 100 GB of storage volumes will cost $8 per month or $0.80 per 10 GB per month.

The type of storage does matter. GP3 is “network attached” storage. For extremely low disk access latency, opt for “d” type instances, such as the [c5d.xlarge](https://instances.vantage.sh/aws/ec2/c5d.large) which comes with a built-in 100 GB NVME SSD. The upcharge on that instance from a [c5.xlarge](https://instances.vantage.sh/aws/ec2/c5d.large) is $14 per month.

10 GB data egress

For the first 10 TB that leave AWS, the rate is $0.09 per GB. Note that the first TB is free, but assuming a normal amount of egress, we’ll peg this at $0.90 per 10 GB per month. Of course, there are tiers for data transfer charges and regional differences. For example, India has higher data transfer charges.

10 database IOPS

As database usage scales, CPU utilization goes up. The best way to relieve pressure on the CPU is to add further [provisioned IOPS](https://handbook.vantage.sh/aws/services/rds-pricing/). These come in at $0.10 per IOPs per month, and are generally purchased in chunks of 1,000. For comparison purposes with the other resources, this comes out to $1 per 10 IOPS per month. For each chunk that will run you about $100 per month. There’s a bit of a song and dance to do here because most [RDS instances](https://instances.vantage.sh/rds) have a maximum number of IOPS supported. A common failure mode is to overprovision IOPS for an instance which cannot support the total amount.

10 custom metrics

Earlier we looked at logging costs. The second of the three pillars of monitoring (the third is tracing) is metrics. Metrics suffer from a cost issue related to cardinality - the more dimensions a metric can have the more custom metrics [CloudWatch](https://www.vantage.sh/blog/cloudwatch-metrics-pricing-explained-in-plain-english) and Datadog charge for.

If you are monitoring 20 endpoints in your application with 5 parameters each, that is 100 custom metrics collected. [CloudWatch charges](https://handbook.vantage.sh/aws/services/cloudwatch-pricing/) $0.30 per metric per month. Datadog pricing actually comes in at half this cost with 100 custom metrics for $15 per month so we’ll land our estimate in between at $20 per month, or $2 per 10 custom metrics per month.

1 IPv4 address

Recently, AWS [announced pricing](https://aws.amazon.com/blogs/aws/new-aws-public-ipv4-address-charge-public-ip-insights/) for IPv4 internet addresses, which were formerly free. The pricing comes in slightly higher than [Google Cloud’s pricing](https://cloud.google.com/vpc/network-pricing) (under “External IP address pricing”), which is $0.004 per hour versus AWS at $0.005 per hour. We generally define a month as having 730 hours, so we’ll round up to $4 per IP address per month from there.

10 GB logs

CloudWatch logs are $0.50 per GB ingested plus $0.03 for storage and some smaller charges for querying and displaying them. The amount of log volume can vary considerably but we think 10 GB is a good starting point for the monthly volume of logs generated.

10 GB memory

Memory is trickier to calculate than cost per core but we can set it at $25 per 8 GB per month. We can look at [Google Cloud](https://cloud.google.com/compute/vm-instance-pricing), which allows you to flexibly combine different vCPU and memory amounts to build a machine. Their costs come in at $2.40 per GB for the e5 series.

On AWS, we can look at the step up in memory for machines with the same vCPU count. A [c5.2xlarge](https://instances.vantage.sh/aws/ec2/c5.2xlarge) has 8 vCPUs and 16 GB of memory while a [m5.2xlarge](https://instances.vantage.sh/aws/ec2/m5.2xlarge) has 8 vCPUs with 32 GB of memory. The price jump for an extra 16 GB memory? $32 per month, or close to the same cost per GB of memory as GCP.

1 vCPU

The c5 is the most commonly used EC2 instance, [costing $62](https://instances.vantage.sh/aws/ec2/c5.large?cost_duration=monthly&region=us-east-1&os=linux&reserved_term=Standard.noUpfront) at on-demand pricing for a month. The m5 and r5 classes are also commonly used, but if we are thinking about what a core costs in the cloud, the Xeon Platinum c5 is a good proxy. The m5.large is $70 and the r5.large is $90. Taking c5, we can estimate the cost of CPU compute at $30 per core per month.

Of course, on Intel and AMD CPUs, a core is really a hyperthreaded core, which comes with some overhead. On Graviton CPUs, a vCPU is actually equivalent to a physical core.

Redis server (100K OPS)

Moving on from components of infrastructure to actual wholesale services, we’ll look at Redis a caching system typically provisioned through ElastiCache, Memorystore, or Redis Cloud. [Redis benchmarks](https://redis.com/blog/redis-enterprise-extends-linear-scalability-200m-ops-sec/) typically measure operations per second (OPS).

To do some quick math here, we need to figure out what instance is needed to support a chunk of OPS. KeyDB, a Redis alternative, published a [blog](https://github.com/Snapchat/KeyDB/issues/166) using the r5 instance class and measuring OPS. They were able to achieve over 100K OPS with a [cache.r5.large](https://instances.vantage.sh/aws/elasticache/cache.r5.large?cost_duration=monthly&compare_on=true&region=us-east-1&os=Redis&reserved_term=Standard.noUpfront) so this cost comes out to $160 per month Redis server per month.

Postgres server (1M rows, 100 TPS)

Although many teams self manage a Postgres cluster as described above, the most common workload we see is to deploy Postgres as a managed service. [Postgres benchmarks](https://aiven.io/blog/postgresql-12-gcp-aws-performance) typically measure transactions per second (TPS) with some consideration towards data size. For this estimate we’ll use 1M rows and 100 TPS.

A recent [MigOps benchmark](https://www.migops.com/blog/is-aurora-postgresql-really-faster-and-cheaper-than-rds-postgresql-benchmarking/) used [db.r5.xlarge](https://instances.vantage.sh/aws/rds/db.r5.xlarge?region=us-east-1&os=PostgreSQL&cost_duration=monthly&reserved_term=Standard.partialUpfront) instances to achieve 475 TPS on the pgbench benchmark. Choosing a smaller instance and adding more data, we’ll estimate that 100 TPS on 1M rows of data is doable by a [db.r5.large](https://instances.vantage.sh/aws/rds/db.r5.large?region=us-east-1&os=PostgreSQL&cost_duration=monthly&reserved_term=Standard.partialUpfront) for an estimate of $180 per Postgres server per month.

1 GPU (A100 & H100)

Some massive caveats apply here. Using previous generation GPUs from Nvidia, the [p4d.24xlarge](https://instances.vantage.sh/aws/ec2/p4d.24xlarge) with 8 A100 GPUs is $23,932 per month on-demand. On Google Cloud, an [A2 with an A100](https://cloud.google.com/compute/vm-instance-pricing) is $2,956 per month. So we feel comfortable landing this estimate at $3,000 per GPU per month.

Of course, most serious AI teams will reserve these GPUs for a longer period of time, brining the price down. The latest GPUs - [h100s](https://instances.vantage.sh/aws/ec2/p5.48xlarge) - are 3X more expensive, coming in around $9,000 per month on AWS.

Conclusion: Building in the cloud

When every resource costs money, the pricing units for different pieces of infrastructure are good to be aware of. Disagree with these numbers? Let us know on [X](https://twitter.com/joinvantage).

From <[https://www.vantage.sh/blog/cloud-costs-every-programmer-should-know?utm_source=tldrnewsletter](https://www.vantage.sh/blog/cloud-costs-every-programmer-should-know?utm_source=tldrnewsletter)>