Clipped from: [https://tutorialsdojo.com/amazon-elastic-compute-cloud-amazon-ec2/](https://tutorialsdojo.com/amazon-elastic-compute-cloud-amazon-ec2/)

- A Linux-based/Windows-based/Mac-based virtual server that you can provision.
- You are limited to running On-Demand Instances per your vCPU-based On-Demand Instance limit, purchasing 20 Reserved Instances, and requesting Spot Instances per your dynamic Spot limit per region.

## Amazon EC2 Features

- The AWS Nitro System is the underlying platform of the next generation of EC2 instances. Traditionally, hypervisors protect the physical hardware and bios, virtualize the CPU, storage, networking, and provide a rich set of management capabilities. With the Nitro System, these functions are offloaded to dedicated hardware and software, thereby reducing the costs of your instances in the process. Hence, the Nitro Hypervisor delivers performance that is indistinguishable from bare metal and performs better than its predecessor: the Xen Hypervisor.
- Server environments are called instances.
- Package OS and additional installations in a reusable template called Amazon Machine Images.
- Various configurations of CPU, memory, storage, and networking capacity for your instances, known as instance types

- t-type and m-type for general purpose
- c-type for compute optimized
- r-type, x-type, and z-type for memory-optimized
- d-type, h-type, and i-type for storage optimized
- f-type, g-type, and p-type for accelerated computing

- Secure login information for your instances using key pairs
- Storage volumes for temporary data that are deleted when you STOP or TERMINATE your instance, known as instance store volumes. Take note that you can stop an EBS-backed instance but not an Instance Store-backed instance. You can only either start or terminate an Instance Store-backed instance.
- Persistent storage volumes for your data using Elastic Block Store volumes (see AWS storage services).
- Multiple physical locations for deploying your resources, such as instances and [EBS](https://tutorialsdojo.com/amazon-ebs/) volumes, known as regions and Availability Zones (see AWS overview).
- A firewall that enables you to specify the protocols, ports, and source IP ranges that can reach your instances using security groups (see aws networking and content delivery).
- Static IPv4 addresses for dynamic cloud computing, known as Elastic IP addresses (see aws networking and content delivery).
- Metadata, known as tags, that you can create and assign to your EC2 resources
- Virtual networks you can create that are logically isolated from the rest of the AWS cloud, and that you can optionally connect to your own network, known as [virtual private clouds](https://tutorialsdojo.com/amazon-vpc/) or VPCs (see aws networking and content delivery).
- Add a script that will be run on instance boot called user-data.
- Host Recovery for Amazon EC2 automatically restarts your instances on a new host in the event of an unexpected hardware failure on a Dedicated Host.
- EC2 Hibernation is available for On-Demand and Reserved Instances running on freshly launched M3, M4, M5, C3, C4, C5, R3, R4, and R5 instances running Amazon Linux and Ubuntu 18.04 LTS. You can enable hibernation for your EBS-backed instances at launch. You can then hibernate and resume your instances through the AWS Management Console, or through the AWS SDK and CLI using the existing stop-instances and start-instances commands. Hibernation requires an EC2 instance to be an encrypted EBS-backed instance.
- You can allow automatic connection of one or more EC2 instances to an [RDS](https://tutorialsdojo.com/amazon-relational-database-service-amazon-rds/) database.

## Instance states

- Start – run your instance normally. You are continuously billed while your instance is running.
- Stop – is just a normal instance shut down. You may restart it again anytime. All EBS volumes remain attached, but data in instance store volumes are deleted. You won’t be charged for usage while instance is stopped. You can attach or detach EBS volumes. You can also create an AMI from the instance, and change the kernel, RAM disk, and instance type while in this state.
- Hibernate – When an instance is hibernated, it writes the in-memory state to a file in the root EBS volume and then shuts itself down. The AMI used to launch the instance must be encrypted, and also the root EBS volume of the instance. The encryption ensures proper protection for sensitive data when it is copied from memory to the EBS volume. While the instance is in hibernation, you pay only for the EBS volumes and Elastic IP Addresses attached to it; there are no hourly charges.
- Terminate – instance performs a normal shutdown and gets deleted. You won’t be able to restart an instance once you terminate it. The root device volume is deleted by default, but any attached EBS volumes are preserved by default. Data in instance store volumes are deleted.
- To prevent accidental termination, enable termination protection.
- By enabling instance stop protection, you can prevent an instance from being accidentally stopped.

## Root Device Volumes

- The root device volume contains the image used to boot the instance.
- You can replace the root volume of a running EC2 instance using the following:

- Initial launch state
- Snapshot
- AMI

- Instance Store-backed Instances

- Any data on the instance store volumes are deleted when the instance is terminated (instance store-backed instances do not support the Stop action) or if it fails (such as if an underlying drive has issues).
- You should also back up critical data from your instance store volumes to persistent storage on a regular basis.

- [Amazon EBS](https://tutorialsdojo.com/amazon-ebs/)-backed Instances

- An Amazon EBS-backed instance can be stopped and later restarted without affecting data stored in the attached volumes.
- When in a stopped state, you can modify the properties of the instance, change its size, or update the kernel it is using, or you can attach your root volume to a different running instance for debugging or any other purpose.
- By default, the root device volume for an AMI backed by Amazon EBS is deleted when the instance terminates.
- Previously, to launch an encrypted EBS-backed EC2 instance from an unencrypted AMI, you would first need to create an encrypted copy of the AMI and use that to launch the EC2 instance. Now, you can [launch encrypted EBS-backed EC2 instances](https://aws.amazon.com/about-aws/whats-new/2019/05/launch-encrypted-ebs-backed-ec2-instances-from-unencrypted-amis-in-a-single-step/) from unencrypted AMIs directly.

## Amazon EC2 – AMI

- Includes the following:

- A template for the root volume for the instance (OS, application server, and applications)
- Launch permissions that control which AWS accounts can use the AMI to launch instances
- A block device mapping that specifies the volumes to attach to the instance when it’s launched

- Backed by Amazon EBS – root device for an instance launched from the AMI is an Amazon EBS volume. AMIs backed by Amazon EBS snapshots can use EBS encryption.
- Backed by Instance Store – root device for an instance launched from the AMI is an instance store volume created from a template stored in [S3](https://tutorialsdojo.com/amazon-s3/).

- You can copy AMIs to different regions.
- Recycle Bin

- You can restore deleted AMIs using recycle bin.
- You can set lock retention rules to protect against modifications and deletions.

- Check the LastLaunchedTime timestamp to see when your AMI was last used to launch an instance.
- By default, a public AMI is deprecated after 2-years from the creation date.

- In the EC2 console, public AMIs owned by Amazon or a verified Amazon partner is marked as a verified provider.

- When an AMI changes state, an event is automatically generated, and you can use Amazon EventBridge to detect and respond to these events.
- With UEFI Secure Boot, you can ensure that an instance only boots software signed with cryptographic keys.
- You can configure an AMI to use Instance Metadata Service Version 2 (IMDSv2) when requesting instance metadata.
- If an AMI has been shared with your AWS account, you can remove your account from the AMI’s launch permissions.

##   Amazon EC2 Image Builder

- A fully managed AWS service that automates the creation, management, and deployment of your Amazon Machine Images (AMIs)
- The AWS Management Console, AWS Command Line Interface, or AWS APIs can be used to create custom images in your AWS account.
- The customized images that Image Builder creates in your account are owned by you, and you can configure pipelines to automate updates as well as system patching for the images in your AWS account.
- Amazon EC2 Image Builder also provides a stand-alone command to create an AMI with the configuration resources that you have defined.

##   Amazon EC2 Pricing

- On-Demand  – pay for the instances that you use by the second, with no long-term commitments or upfront payments.
- Reserved – make a low, one-time, up-front payment for an instance, reserve it for a one– or three-year term, and pay a significantly lower hourly rate for these instances. It has two offering classes: Standard and Convertible.

- The Standard class provides the most significant discount but you can only modify some of its attributes during the term. It can also be sold in the Reserved Instance Marketplace.
- The Convertible class provides a lower discount than Standard Reserved Instances, but can be exchanged for another Convertible Reserved Instance with different instance attributes. However, this one cannot be sold in the Reserved Instance Marketplace.

|   |   |   |
|---|---|---|
||Standard RI|Convertible RI|
|Terms<br><br>(average discount off On-Demand)|1 year (40%)<br><br>3 years (60%)|1 year (31%)<br><br>3 years (54%)|
|Change Availability Zone, Instance size (for Linux OS), Networking type|Yes|Yes|
|Change instance families, operating system, tenancy, and payment option||Yes|
|Benefit from Price Reductions||Yes|

- When purchasing a Reserved Instance, you’ll need to determine its scope (regional or zonal).

|   |   |   |
|---|---|---|
||Regional RI|Zonal RI|
|Ability to Reserve Capacity|No|Yes|
|Availability Zone Flexibility|The discount is valid for instance usage in any Availability Zone within the specified Region.|The discount only applies to instance usage in the specified Availability Zone.|
|Instance Size Flexibility|The discount applies to instance usage within the instance family.|The discount only applies to instance usage for the specified instance type and size.|
|Queuing A Purchase|Yes|No|

- Spot – request unused EC2 instances, which can lower your costs significantly. Spot Instances are available at up to a 90% discount compared to On-Demand prices.

- Spot Instances with a defined duration (also known as Spot blocks) are designed not to be interrupted and will run continuously for the duration you select. This makes them ideal for jobs that take a finite time to complete, such as batch processing, encoding and rendering, modeling and analysis, and continuous integration.
- A Spot Fleet is a collection of Spot Instances and optionally On-Demand Instances. The service attempts to launch the number of Spot Instances and On-Demand Instances to meet your specified target capacity. The request for Spot Instances is fulfilled if there is available capacity and the maximum price you specified in the request exceeds the current Spot price. The Spot Fleet also attempts to maintain its target capacity fleet if your Spot Instances are interrupted.
- A Spot Capacity pool is a set of unused EC2 instances with the same instance type, operating system, Availability Zone, and network platform.
- You can start and stop your Spot Instances backed by Amazon EBS at will.
- You can modify instance types and weights for a running EC2 Fleet or Spot Fleet without having to recreate it.

- Allocation strategy for Spot Instances

- LowestPrice – The Spot Instances come from the pool with the lowest price. This is the default strategy.
- Diversified – The Spot Instances are distributed across all pools.
- CapacityOptimized – The Spot Instances come from the pool with optimal capacity for the number of instances that are launching.
- InstancePoolsToUseCount – The Spot Instances are distributed across the number of Spot pools that you specify. This parameter is valid only when used in combination with the lowest Price.

- Dedicated Hosts – pay for a physical host that is fully dedicated to running your instances, and bring your existing per-socket, per-core, or per-VM software licenses to reduce costs.
- Dedicated Instances – pay, by the hour, for instances that run on single-tenant hardware.
- On-Demand Capacity Reservations – reserve capacity for your Amazon EC2 instances in a specific Availability Zone for any duration.

- Unlike Reserved instances, you don’t need to have a one-year or three-year term commitment.
- When you create a Capacity Reservation, you specify:

- The Availability Zone in which to reserve the capacity
- The number of instances for which to reserve capacity
- The instance attributes, including the instance type, tenancy, and platform/OS

- Your Savings Plans and regional Reserved Instances can be applied with your capacity reservations to receive discounts. Without these, your capacity reservations do not have billing discounts.
- Capacity Reservations can be created in placement groups
- Capacity Reservations can’t be used with Dedicated Hosts
- Your capacity reservation usage metrics can be monitored in Amazon Cloudwatch.

- There is a data transfer charge when copying AMI from one region to another
- EBS pricing is different from instance pricing. (see AWS storage services)
- AWS imposes a small hourly charge if an Elastic IP address is not associated with a running instance, or if it is associated with a stopped instance or an unattached network interface.
- You are charged for any additional Elastic IP addresses associated with an instance.
- If data is transferred between these two instances, it is charged at “Data Transfer Out from EC2 to Another AWS Region” for the first instance and at “Data Transfer In from Another AWS Region” for the second instance.

## Amazon Elastic Compute Cloud Security

- Use [IAM](https://tutorialsdojo.com/aws-identity-and-access-management-iam/) to control access to your instances (see AWS Security and Identity Service).

- IAM policies
- IAM roles

- Restrict access by only allowing trusted hosts or networks to access ports on your instance.
- A security group acts as a virtual firewall that controls the traffic for one or more instances.

- Create different security groups to deal with instances that have different security requirements.
- You can add rules to each security group that allows traffic to or from its associated instances.
- You can modify the rules for a security group at any time.
- New rules are automatically applied to all instances that are associated with the security group.
- Evaluates all the rules from all the security groups that are associated with an instance to decide whether to allow traffic or not.
- By default, security groups allow all outbound traffic.
- Security group rules are always permissive; you can’t create rules that deny access.
- Security groups are stateful

- If you don’t specify a security group when you launch an instance, the instance is automatically associated with the default security group for the VPC, which has the following rules:

- Allows all inbound traffic from other instances associated with the default security group
- Allows all outbound traffic from the instance.

- Disable password-based logins for instances launched from your AMI, since passwords can be cracked or found.
- You can replicate the network traffic from an EC2 instance within your Amazon VPC and forward that traffic to security and monitoring appliances for content inspection, threat monitoring, and troubleshooting.
- When creating a new key pair, you can specify the key format (.pem & .ppk).
- Querying of the public key and creation date of an EC2 key pair is supported.
- For EC2 Instance Connect and EC2 Serial Console, ED25519 keys are now supported.

## Amazon EC2 Networking

- An Elastic IP address is a static IPv4 address designed for dynamic cloud computing. With it, you can mask the failure of an instance or software by rapidly remapping the address to another instance in your account.
- If you have not enabled auto-assign public IP address for your instance, you need to associate an Elastic IP address with your instance to enable communication with the internet.
- An Elastic IP address is for use in a specific region only.
- By default, all AWS accounts are limited to five (5) Elastic IP addresses per region, because public (IPv4) internet addresses are a scarce public resource.
- You can transfer Elastic IP addresses from one AWS account to another.
- By default EC2 instances come only with a private IP when created in a private subnet, and public and private IP when created in a public subnet.
- An elastic network interface is a logical networking component in a VPC that represents a virtual network card, which directs traffic to your instance
- Every instance in a VPC has a default network interface, called the primary network interface (eth0). You cannot detach a primary network interface from an instance.
- You can create and attach additional network interfaces. The maximum number of network interfaces that you can use varies by instance type.
- You can attach a network interface to an instance in a different subnet as long as its within the same AZ
- Default interfaces are terminated with instance termination.
- Scale with EC2 Scaling Groups and distribute traffic among instances using Elastic Load Balancer.
- You can configure EC2 instances as bastion hosts (aka jump boxes) in order to access your VPC instances for management, using SSH or RDP protocols
- Enhanced Networking – It provides higher bandwidth, higher packet per second (PPS) performance, and consistent lower inter-instance latencies, which are being used in Placement Groups. It uses single root I/O virtualization (SR-IOV) to provide high-performance networking capabilities. SR-IOV is a method of device virtualization that provides higher I/O performance and lower CPU utilization when compared to traditional virtualized network interfaces.
- Elastic Fabric Adapter (EFA) – This is a network device that you can attach to your EC2 instance to significantly accelerate machine learning applications and High Performance Computing (HPC). It empowers your computing resources to achieve the application performance of an on-premises HPC cluster, with the elasticity and scalability provided by AWS. Compared with a TCP transport that is traditionally used in cloud-based HPC systems, EFA provides lower and more consistent latency and higher throughput as it enhances the performance of inter-instance communication.

## Amazon EC2 Monitoring

- EC2 items to monitor

- CPU utilization, Network utilization, Disk performance, Disk Reads/Writes using EC2 metrics
- Memory utilization, disk swap utilization, disk space utilization, page file utilization, log collection using a monitoring agent/CloudWatch Logs

- Automated monitoring tools include:

- System Status Checks – monitor the AWS systems required to use your instance to ensure they are working properly. These checks detect problems with your instance that require AWS involvement to repair.
- Instance Status Checks – monitor the software and network configuration of your individual instance. These checks detect problems that require your involvement to repair.
- [Amazon CloudWatch](https://tutorialsdojo.com/amazon-cloudwatch/) Alarms – watch a single metric over a time period you specify, and perform one or more actions based on the value of the metric relative to a given threshold over a number of time periods.
- Amazon CloudWatch Events – automate your AWS services and respond automatically to system events.
- Amazon CloudWatch Logs – monitor, store, and access your log files from Amazon EC2 instances, [AWS CloudTrail](https://tutorialsdojo.com/aws-cloudtrail/), or other sources.

- Monitor your EC2 instances with CloudWatch. By default, EC2 sends metric data to CloudWatch in 5-minute periods.
- You can also enable detailed monitoring to collect data in 1-minute periods.

## Instance Metadata and User Data

- Instance metadata is data about your instance that you can use to configure or manage the running instance.
- Instance metadata and user data are not protected by cryptographic methods.
- View all categories of instance metadata from within a running instance at [http://169.254.169.254/latest/meta-data/](http://169.254.169.254/latest/meta-data/)
- You can pass two types of user data to EC2: shell scripts and cloud-init directives.
- User data is limited to 16 KB.
- If you stop an instance, modify its user data, and start the instance, the updated user data is not executed when you start the instance.
- Retrieve user data from within a running instance at [http://169.254.169.254/latest/user-data](http://169.254.169.254/latest/user-data)
- An instance tag can be accessed from the instance metadata.
- When using Auto Scaling groups, the instance metadata contains information about an instance’s target lifecycle state.

## Placement Groups

- You can launch or start instances in a placement group, which determines how instances are placed on underlying hardware.

- Cluster – clusters instances into a low-latency group in a single Availability Zone. Recommended for applications that benefit from low network latency, high network throughput, or both, and if the majority of the network traffic is between the instances in the group.
- Spread – spreads instances across underlying hardware. Recommended for applications that have a small number of critical instances that should be kept separate from each other. Note: A spread placement group can span multiple Availability Zones, and you can have a maximum of seven running instances per Availability Zone per group.

- Partition placement groups is an Amazon EC2 placement strategy that helps reduce the likelihood of correlated failures for large distributed and replicated workloads such as HDFS, HBase, and Cassandra running on EC2.
- Partition placement groups spread EC2 instances across logical partitions and ensure that instances in different partitions do not share the same underlying hardware. In addition, partition placement groups offer visibility into the partitions and allow topology aware applications to use this information to make intelligent data replication decisions, increasing data availability and durability.

## Amazon EC2 Rules

- The name you specify for a placement group must be unique within your AWS account for the region.
- You can’t merge placement groups.
- An instance can be launched in one placement group at a time; it cannot span multiple placement groups.
- Instances with a tenancy of host cannot be launched in placement groups.

## Amazon EC2 Storage

- EBS (see AWS Storage Services)

- Provides durable, block-level storage volumes that you can attach to a running instance.
- Use as a primary storage device for data that requires frequent and granular updates.
- To keep a backup copy of your data, create a snapshot of an EBS volume, which is stored in S3. You can create an EBS volume from a snapshot, and attach it to another instance.

- Instance Store

- Provides temporary block-level storage for instances.
- The data on an instance store volume persists only during the life of the associated instance; if you stop or terminate an instance, any data on instance store volumes is lost.

- [Elastic File System](https://tutorialsdojo.com/amazon-efs/) (EFS) (see AWS Storage Services)

- Provides scalable file storage for use with Amazon EC2. You can create an EFS file system and configure your instances to mount the file system.
- You can use an EFS file system as a common data source for workloads and applications running on multiple instances.

- FSx 

- [Amazon FSx](https://tutorialsdojo.com/amazon-fsx/) for Windows File Server is a fully-managed file storage built on Windows Server.
- Amazon FSx for Lustre is a fully-managed file storage built on the world’s most popular high-performance file system, Lustre.
- Amazon FSx for NetApp ONTAP is a fully managed shared storage solution based on NetApp’s ONTAP file system.
- Amazon FSx for OpenZFS is a fully managed shared storage solution that is based on the OpenZFS file system.

- S3 (see AWS Storage Services)

- Provides access to reliable and inexpensive data storage infrastructure.
- Storage for EBS snapshots and instance store-backed AMIs.

- With torn write prevention (block storage feature), you can improve the performance of your I/O-intensive relational database workloads and reduce latency without compromising data resiliency.
- Resources and Tagging

- EC2 resources include images, instances, volumes, and snapshots. When you create a resource, AWS assigns the resource a unique resource ID.
- Some resources can be used in all regions (global), and some resources are specific to the region or Availability Zone in which they reside.  
     

|   |   |   |
|---|---|---|
|Resource|Type|Description|
|AWS account|Global|You can use the same AWS account in all regions.|
|Key pairs|Global or Regional|The key pairs that you create using EC2 are tied to the region where you created them. You can create your own RSA key pair and upload it to the region in which you want to use it; therefore, you can make your key pair globally available by uploading it to each region.|
|Amazon EC2 resource identifiers|Regional|Each resource identifier, such as an AMI ID, instance ID, EBS volume ID, or EBS snapshot ID, is tied to its region and can be used only in the region where you created the resource.|
|User-supplied resource names|Regional|Each resource name, such as a security group name or key pair name, is tied to its region and can be used only in the region where you created the resource. Although you can create resources with the same name in multiple regions, they aren’t related to each other.|
|AMIs|Regional|An AMI is tied to the region where its files are located within S3. You can copy an AMI from one region to another.|
|Elastic IP addresses|Regional|An Elastic IP address is tied to a region and can be associated only with an instance in the same region.|
|Security groups|Regional|A security group is tied to a region and can be assigned only to instances in the same region. You can’t enable an instance to communicate with an instance outside its region using security group rules.|
|EBS snapshots|Regional|An EBS snapshot is tied to its region and can only be used to create volumes in the same region. You can copy a snapshot from one region to another.|
|EBS volumes|Availability Zone|An EBS volume is tied to its Availability Zone and can be attached only to instances in the same Availability Zone.|
|Instances|Availability Zone|An instance is tied to the Availability Zones in which you launched it. However, its instance ID is tied to the region.|

- You can optionally assign your own metadata to each resource with tags, which consist of a key and an optional value that you both define.

## Additional Amazon EC2 related Cheat Sheet:

## Validate Your Knowledge

#### Question 1

Which of the following Amazon EC2 instance purchasing options can help you address compliance requirements and reduce costs by allowing you to use your existing server-bound software licenses?

1. On-Demand Instance
2. Dedicated Instance
3. Reserved Instance
4. Dedicated Host

#### [Show me the answer!](https://tutorialsdojo.com/amazon-elastic-compute-cloud-amazon-ec2/#bfe8b13f0819a6485)

Correct Answer: 4

An Amazon EC2 Dedicated Host is a physical server with EC2 instance capacity fully dedicated to your use. Dedicated Hosts can help you address compliance requirements and reduce costs by allowing you to use your existing server-bound software licenses.

Dedicated Hosts allow you to use your existing per-socket, per-core, or per-VM software licenses, including Microsoft Windows Server, Microsoft SQL Server, SUSE Linux Enterprise Server, Red Hat Enterprise Linux, or other software licenses that are bound to VMs, sockets, or physical cores, subject to your license terms.

You can use Dedicated Hosts and Dedicated instances to launch Amazon EC2 instances on physical servers that are dedicated to your use. An important difference between a Dedicated Host and a Dedicated instance is that a Dedicated Host gives you additional visibility and control over how instances are placed on a physical server, and you can consistently deploy your instances to the same physical server over time. As a result, Dedicated Hosts enable you to use your existing server-bound software licenses and address corporate compliance and regulatory requirements.

The following table highlights the key similarities and differences in the features available to you when using Dedicated Hosts and Dedicated instances:

You have the option to launch instances onto a specific Dedicated Host, or you can let Amazon EC2 place the instances automatically. Controlling instance placement allows you to deploy applications to address licensing, corporate compliance, and regulatory requirements.

Hence, the correct answer is: Dedicated Host.

On-Demand Instance purchasing option is incorrect because this only enables you to pay for compute capacity per hour or per second depending on which instances you run. You cannot use your existing server-bound software licenses with this option.

Dedicated Instance purchasing option is incorrect. Although Dedicated instances also run on dedicated hardware, Dedicated Hosts provide further visibility and control by allowing you to place your instances on a specific, physical server.

Reserved Instance purchasing option is incorrect as you would not be able to use your existing server-bound software licenses with this one. You have to use a Dedicated Host instead.

## Amazon EC2 Cheat Sheet References:

[https://aws.amazon.com/ec2/dedicated-hosts/](https://aws.amazon.com/ec2/dedicated-hosts/) [https://aws.amazon.com/windows/faq/#byol](https://aws.amazon.com/windows/faq/#byol)

Note: This question was extracted from our [AWS Certified Cloud Practitioner Practice Exams](https://portal.tutorialsdojo.com/courses/aws-certified-cloud-practitioner-practice-exams/).

#### Question 2

A company deployed a high-performance computing (HPC) cluster that spans multiple EC2 instances across multiple Availability Zones and processes various wind simulation models. Currently, the Solutions Architect is experiencing a slowdown in their applications and upon further investigation, it was discovered that it was due to latency issues.

Which is the MOST suitable solution that the Solutions Architect should implement to provide low-latency network performance necessary for tightly-coupled node-to-node communication of the HPC cluster?

1. Set up a spread placement group across multiple Availability Zones in multiple AWS Regions.
2. Set up AWS Direct Connect connections across multiple Availability Zones for increased bandwidth throughput and more consistent network experience.
3. Use EC2 Dedicated Instances.
4. Set up a cluster placement group within a single Availability Zone in the same AWS Region.

#### [Show me the answer!](https://tutorialsdojo.com/amazon-elastic-compute-cloud-amazon-ec2/#daef1c39db8fa9d65)

Correct Answer: 4

When you launch a new EC2 instance, the EC2 service attempts to place the instance in such a way that all of your instances are spread out across underlying hardware to minimize correlated failures. You can use placement groups to influence the placement of a group of interdependent instances to meet the needs of your workload. Depending on the type of workload, you can create a placement group using one of the following placement strategies:

Cluster – packs instances close together inside an Availability Zone. This strategy enables workloads to achieve the low-latency network performance necessary for tightly-coupled node-to-node communication that is typical of HPC applications.

Partition – spreads your instances across logical partitions such that groups of instances in one partition do not share the underlying hardware with groups of instances in different partitions. This strategy is typically used by large distributed and replicated workloads, such as Hadoop, Cassandra, and Kafka.

Spread – strictly places a small group of instances across distinct underlying hardware to reduce correlated failures.

Cluster placement groups are recommended for applications that benefit from low network latency, high network throughput, or both. They are also recommended when the majority of the network traffic is between the instances in the group. To provide the lowest latency and the highest packet-per-second network performance for your placement group, choose an instance type that supports enhanced networking.

Partition placement groups can be used to deploy large distributed and replicated workloads, such as HDFS, HBase, and Cassandra, across distinct racks. When you launch instances into a partition placement group, Amazon EC2 tries to distribute the instances evenly across the number of partitions that you specify. You can also launch instances into a specific partition to have more control over where the instances are placed.

Spread placement groups are recommended for applications that have a small number of critical instances that should be kept separate from each other. Launching instances in a spread placement group reduces the risk of simultaneous failures that might occur when instances share the same racks. Spread placement groups provide access to distinct racks and are therefore suitable for mixing instance types or launching instances over time. A spread placement group can span multiple Availability Zones in the same Region. You can have a maximum of seven running instances per Availability Zone per group.

Hence, the correct answer is: Set up a cluster placement group within a single Availability Zone in the same AWS Region.

The option that says: Set up a spread placement group across multiple Availability Zones in multiple AWS Regions is incorrect. Although using a placement group is valid for this particular scenario, you can only set up a placement group in a single AWS Region only. A spread placement group can span multiple Availability Zones in the same Region.

The option that says: Set up AWS Direct Connect connections across multiple Availability Zones for increased bandwidth throughput and more consistent network experience is incorrect because this is primarily used for hybrid architectures. It bypasses the public Internet and establishes a secure, dedicated connection from your on-premises data center into AWS and not used for having low latency within your AWS network.

The option that says: Use EC2 Dedicated Instances is incorrect because these are EC2 instances that run in a VPC on hardware that is dedicated to a single customer and are physically isolated at the host hardware level from instances that belong to other AWS accounts. It is not used for reducing latency.

## Amazon EC2  Cheat Sheet References:

[http://docs.aws.amazon.com/AWSEC2/latest/UserGuide/placement-groups.html](http://docs.aws.amazon.com/AWSEC2/latest/UserGuide/placement-groups.html) [https://aws.amazon.com/hpc/](https://aws.amazon.com/hpc/)

Note: This question was extracted from our [AWS Certified Solutions Architect Associate Practice Exams](https://portal.tutorialsdojo.com/courses/aws-certified-solutions-architect-associate-practice-exams/).

For more [AWS practice exam](https://portal.tutorialsdojo.com/shop/) questions with detailed explanations, visit the [Tutorials Dojo Portal](https://portal.tutorialsdojo.com/):

### Additional Training Materials: Amazon EC2 Video Courses on Udemy

## Amazon EC2 Cheat Sheet References:

[https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/) [https://aws.amazon.com/ec2/features/](https://aws.amazon.com/ec2/features/) [https://aws.amazon.com/ec2/pricing/](https://aws.amazon.com/ec2/pricing/) [https://aws.amazon.com/ec2/faqs/](https://aws.amazon.com/ec2/faqs/)