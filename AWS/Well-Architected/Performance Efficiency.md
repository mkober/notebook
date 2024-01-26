The Performance Efficiency pillar includes the ability to use computing resources efficiently to meet system requirements, and to maintain that efficiency as demand changes and technologies evolve.

The performance efficiency pillar provides an overview of design principles, [best practices](https://wa.aws.amazon.com/wat.concept.best-practice.en.html "Proven ways of achieving successful outcomes."), and questions. You can find prescriptive guidance on implementation in the Performance Efficiency Pillar whitepaper .

## Design Principles

There are five design principles for performance efficiency in the cloud:

- **Democratize advanced technologies**: Make advanced technology implementation easier for your team by delegating complex tasks to your cloud vendor. Rather than asking your IT team to learn about hosting and running a new technology, consider consuming the technology as a service. For example, [NoSQL](https://wa.aws.amazon.com/wat.concept.nosql.en.html "NoSQL databases are purpose built for specific data models and have flexible schemas for building modern applications. 85015F42-FBBF-405D-80DF-EA0D02C507E2") databases, media transcoding, and machine learning are all technologies that require specialized expertise. In the cloud, these technologies become services that your team can consume, allowing your team to focus on product development rather than resource provisioning and management.
    
- **Go global in minutes**: Deploying your [workload](https://wa.aws.amazon.com/wat.concept.workload.en.html "The set of components that together deliver business value.") in multiple [AWS Regions](https://wa.aws.amazon.com/wat.concept.region.en.html "A named set of AWS resources in the same geographical area. A Region comprises at least two Availability Zones.") around the world allows you to provide lower [latency](https://wa.aws.amazon.com/wat.concept.latency.en.html "A measurement of the amount of time between an action and the result, often between a request and a response.") and a better experience for your customers at minimal [cost](https://wa.aws.amazon.com/wat.pillar.costOptimization.en.html "The ability to run systems to deliver business value at the lowest price point.").
    
- **Use serverless architectures**: Serverless [architectures](https://wa.aws.amazon.com/wat.concept.architecture.en.html "How components interact and communicate.") remove the need for you to run and maintain physical servers for traditional compute activities. For example, serverless storage services can act as static websites (removing the need for web servers) and [event](https://wa.aws.amazon.com/wat.concept.event.en.html "An instance of something happening that is significant to the workload.") services can host code. This removes the operational burden of managing physical servers, and can lower transactional [costs](https://wa.aws.amazon.com/wat.pillar.costOptimization.en.html "The ability to run systems to deliver business value at the lowest price point.") because managed services operate at cloud scale.
    
- **Experiment more often**: With virtual and automatable resources, you can quickly carry out comparative testing using different types of instances, storage, or configurations.s.
    
- **Consider mechanical sympathy**: Use the technology approach that aligns best with your goals. For example, consider data access patterns when you select database or storage for your [workload](https://wa.aws.amazon.com/wat.concept.workload.en.html "The set of components that together deliver business value.").
    

## Definition

There are five best practice areas for performance efficiency in the cloud:

- [Architecture selection](https://wa.aws.amazon.com/wat.pillar.performance.en.html#perf.select)
- [Compute and hardware](https://wa.aws.amazon.com/wat.pillar.performance.en.html#perf.compute)
- [Data management](https://wa.aws.amazon.com/wat.pillar.performance.en.html#perf.data)
- [Networking and content delivery](https://wa.aws.amazon.com/wat.pillar.performance.en.html#perf.network)
- [Process and culture](https://wa.aws.amazon.com/wat.pillar.performance.en.html#perf.process)

Take a data-driven approach to building a high-performance [architecture](https://wa.aws.amazon.com/wat.concept.architecture.en.html "How components interact and communicate."). Gather data on all aspects of the [architecture](https://wa.aws.amazon.com/wat.concept.architecture.en.html "How components interact and communicate."), from the high-level design to the selection and configuration of resource types.

Reviewing your choices on a regular basis ensures that you are taking advantage of the continually evolving AWS Cloud. Monitoring ensures that you are aware of any deviance from expected performance. Make trade-offs in your [architecture](https://wa.aws.amazon.com/wat.concept.architecture.en.html "How components interact and communicate.") to improve performance, such as using compression or caching, or relaxing [consistency](https://wa.aws.amazon.com/wat.concept.consistency.en.html "A state where two systems, storing the same information, return the same results.") requirements.

## Best Practices

### Architecture selection

The optimal solution for a particular [workload](https://wa.aws.amazon.com/wat.concept.workload.en.html "The set of components that together deliver business value.") varies, and solutions often combine multiple approaches. Well-architected [workloads](https://wa.aws.amazon.com/wat.concept.workload.en.html "The set of components that together deliver business value.") use multiple solutions and allow different features to improve [performance](https://wa.aws.amazon.com/wat.pillar.performance.en.html "The ability to use computing resources efficiently to meet system requirements, and to maintain that efficiency as demand changes and technologies evolve.").

AWS resources are available in many types and configurations, which makes it easier to find an approach that closely matches your needs. You can also find options that are not easily achievable with on-premises infrastructure. For example, a managed service such as Amazon DynamoDB provides a fully managed [NoSQL](https://wa.aws.amazon.com/wat.concept.nosql.en.html "NoSQL databases are purpose built for specific data models and have flexible schemas for building modern applications. 85015F42-FBBF-405D-80DF-EA0D02C507E2") database with single-digit millisecond [latency](https://wa.aws.amazon.com/wat.concept.latency.en.html "A measurement of the amount of time between an action and the result, often between a request and a response.") at any scale.

The following questions focus on these considerations for performance efficiency.

|   |
|---|
|[**PERF 1:** How do you select the appropriate cloud resources and architecture patterns for your workload?](https://wa.aws.amazon.com/wat.question.PERF_1.en.html)|

Use a data-driven approach to select the patterns and implementation for your [architecture](https://wa.aws.amazon.com/wat.concept.architecture.en.html "How components interact and communicate.") and achieve a [cost](https://wa.aws.amazon.com/wat.pillar.costOptimization.en.html "The ability to run systems to deliver business value at the lowest price point.") effective solution. AWS Solutions Architects, AWS Reference [Architectures](https://wa.aws.amazon.com/wat.concept.architecture.en.html "How components interact and communicate."), and [AWS Partner Network](https://wa.aws.amazon.com/wat.concept.apn.en.html "The AWS Partner Network (APN) is the global partner program for AWS.") (APN) partners can help you select an [architecture](https://wa.aws.amazon.com/wat.concept.architecture.en.html "How components interact and communicate.") based on industry knowledge, but data obtained through benchmarking or load testing will be required to optimize your [architecture](https://wa.aws.amazon.com/wat.concept.architecture.en.html "How components interact and communicate.").

Your [architecture](https://wa.aws.amazon.com/wat.concept.architecture.en.html "How components interact and communicate.") will likely combine a number of different architectural approaches (for example, [event](https://wa.aws.amazon.com/wat.concept.event.en.html "An instance of something happening that is significant to the workload.")-driven, ETL, or pipeline). The implementation of your [architecture](https://wa.aws.amazon.com/wat.concept.architecture.en.html "How components interact and communicate.") will use the AWS services that are specific to the optimization of your [architecture](https://wa.aws.amazon.com/wat.concept.architecture.en.html "How components interact and communicate.")'s [performance](https://wa.aws.amazon.com/wat.pillar.performance.en.html "The ability to use computing resources efficiently to meet system requirements, and to maintain that efficiency as demand changes and technologies evolve."). In the following sections we discuss the four main resource types to consider (compute, storage, database, and network).

### Compute and hardware

The optimal compute choice for a particular [workload](https://wa.aws.amazon.com/wat.concept.workload.en.html "The set of components that together deliver business value.") can vary based on application design, usage patterns, and configuration settings. [Architectures](https://wa.aws.amazon.com/wat.concept.architecture.en.html "How components interact and communicate.") may use different compute choices for various [components](https://wa.aws.amazon.com/wat.concept.component.en.html "The code, configuration and AWS Resources that deliver against a business requirement.") and allow different features to improve [performance](https://wa.aws.amazon.com/wat.pillar.performance.en.html "The ability to use computing resources efficiently to meet system requirements, and to maintain that efficiency as demand changes and technologies evolve."). Selecting the wrong compute choice for an [architecture](https://wa.aws.amazon.com/wat.concept.architecture.en.html "How components interact and communicate.") can lead to lower [performance efficiency](https://wa.aws.amazon.com/wat.pillar.performance.en.html "The ability to use computing resources efficiently to meet system requirements, and to maintain that efficiency as demand changes and technologies evolve.").

BLANK PARA

The following questions focus on these considerations for performance efficiency.

|   |
|---|
|[**PERF 2:** How do you select and use compute resources in your workload?](https://wa.aws.amazon.com/wat.question.PERF_2.en.html)|

BLANK PARA

### Data management

The optimal data management solution for a particular system varies based on the kind of data type (block, file, or object), access patterns (random or sequential), required throughput, frequency of access (online, offline, archival), frequency of update (WORM, dynamic), and [availability](https://wa.aws.amazon.com/wat.concept.availability.en.html "A measurement of a system's ability to provide its designed functionality.") and [durability](https://wa.aws.amazon.com/wat.concept.durability.en.html "The ability of a system to remain functional when faced with the challenges of normal operation over its lifetime.") constraints. Well-Architected [workloads](https://wa.aws.amazon.com/wat.concept.workload.en.html "The set of components that together deliver business value.") use purpose-built data stores which allow different features to improve [performance](https://wa.aws.amazon.com/wat.pillar.performance.en.html "The ability to use computing resources efficiently to meet system requirements, and to maintain that efficiency as demand changes and technologies evolve.").

BLANK PARA

The following questions focus on these considerations for performance efficiency.

|   |
|---|
|[**PERF 3:** How do you store, manage, and access data in your workload?](https://wa.aws.amazon.com/wat.question.PERF_3.en.html)|

BLANK PARA

### Networking and content delivery

The optimal networking solution for a [workload](https://wa.aws.amazon.com/wat.concept.workload.en.html "The set of components that together deliver business value.") varies based on [latency](https://wa.aws.amazon.com/wat.concept.latency.en.html "A measurement of the amount of time between an action and the result, often between a request and a response."), throughput requirements, jitter, and bandwidth. Physical constraints, such as user or on-premises resources, determine location options. These constraints can be offset with [edge locations](https://wa.aws.amazon.com/wat.concept.edge-location.en.html "A site that CloudFront uses to cache copies of your content for faster delivery to users at any location.") or resource placement.

On AWS, networking is virtualized and is available in a number of different types and configurations. This makes it easier to match your networking needs. AWS offers product features (for example, [Enhanced Networking](https://wa.aws.amazon.com/wat.concept.enhanced-networking.en.html "Enhanced networking uses single root I/O virtualization (SR-IOV) to provide high-performance networking capabilities on supported instance types."), Amazon EC2 networking optimized instances, [Amazon S3 transfer acceleration](https://wa.aws.amazon.com/wat.concept.amazon-s3-transfer-acceleration.en.html "Amazon S3 Transfer Acceleration enables fast, easy, and secure transfers of files over long distances between your client and an S3 bucket. Transfer Acceleration takes advantage of Amazon CloudFront's globally distributed edge locations. As the data arrives at an edge location, data is routed to Amazon S3 over an optimized network path."), and dynamic Amazon CloudFront) to optimize network traffic. AWS also offers networking features (for example, Amazon Route 53 [latency](https://wa.aws.amazon.com/wat.concept.latency.en.html "A measurement of the amount of time between an action and the result, often between a request and a response.") routing, Amazon [VPC endpoints](https://wa.aws.amazon.com/wat.concept.vpc-endpoint.en.html "A VPC endpoint enables you to privately connect your VPC to supported AWS services and VPC endpoint services powered by PrivateLink without requiring an internet gateway, NAT device, VPN connection, or AWS Direct Connect connection. Instances in your VPC do not require public IP addresses to communicate with resources in the service. Traffic between your VPC and the other service does not leave the Amazon network."), AWS Direct Connect, and AWS Global Accelerator) to reduce network distance or jitter.

The following questions focus on these considerations for performance efficiency.

|   |
|---|
|[**PERF 4:** How do you select and configure networking resources in your workload?](https://wa.aws.amazon.com/wat.question.PERF_4.en.html)|

BLANK PARA

### Process and culture

When architecting [workloads](https://wa.aws.amazon.com/wat.concept.workload.en.html "The set of components that together deliver business value."), there are principles and practices that you can adopt to help you better run efficient high-performing cloud [workloads](https://wa.aws.amazon.com/wat.concept.workload.en.html "The set of components that together deliver business value.").

BLANK PARA

The following questions focus on these considerations for performance efficiency.

|   |
|---|
|[**PERF 5:** What process do you use to support more performance efficiency for your workload?](https://wa.aws.amazon.com/wat.question.PERF_5.en.html)|

To adopt a culture that fosters [performance efficiency](https://wa.aws.amazon.com/wat.pillar.performance.en.html "The ability to use computing resources efficiently to meet system requirements, and to maintain that efficiency as demand changes and technologies evolve.") of cloud [workloads](https://wa.aws.amazon.com/wat.concept.workload.en.html "The set of components that together deliver business value."), consider these key principles and practices:

**Infrastructure as code:** Define your infrastructure as code using approaches such as AWS CloudFormation templates. The use of templates allows you to place your infrastructure into source control alongside your application code and configurations. This allows you to apply the same practices you use to develop software in your infrastructure so you can iterate rapidly.

**Deployment pipeline:** Use a [continuous integration](https://wa.aws.amazon.com/wat.concept.continuous-integration.en.html "Automation that is used to perform builds of software and automate tests against that software.")/[continuous deployment](https://wa.aws.amazon.com/wat.concept.continuous-deployment.en.html "Automated deployment to production which is dependent on results from testing and building. Every time a build and all the tests occur with no errors or failed tests, code is deployed automatically.") (CI/CD) pipeline (for example, source code repository, build systems, deployment, and testing automation) to deploy your infrastructure. This allows you to deploy in a repeatable, consistent, and low-[cost](https://wa.aws.amazon.com/wat.pillar.costOptimization.en.html "The ability to run systems to deliver business value at the lowest price point.") fashion as you iterate.

**Well-defined metrics:** Set up and monitor metrics to capture key [performance](https://wa.aws.amazon.com/wat.pillar.performance.en.html "The ability to use computing resources efficiently to meet system requirements, and to maintain that efficiency as demand changes and technologies evolve.") indicators (KPIs). We recommend that you use both technical and business metrics. For websites or mobile apps, key metrics are capturing time to first byte or rendering. Other generally applicable metrics include thread count, garbage collection rate, and wait states. Business metrics, such as the aggregate cumulative [cost](https://wa.aws.amazon.com/wat.pillar.costOptimization.en.html "The ability to run systems to deliver business value at the lowest price point.") per request, can alert you to ways to drive down [costs](https://wa.aws.amazon.com/wat.pillar.costOptimization.en.html "The ability to run systems to deliver business value at the lowest price point."). Carefully consider how you plan to interpret metrics. For example, you could choose the maximum or 99th percentile instead of the average.

**[Performance](https://wa.aws.amazon.com/wat.pillar.performance.en.html "The ability to use computing resources efficiently to meet system requirements, and to maintain that efficiency as demand changes and technologies evolve.") test automatically:** As part of your deployment process, automatically start [performance](https://wa.aws.amazon.com/wat.pillar.performance.en.html "The ability to use computing resources efficiently to meet system requirements, and to maintain that efficiency as demand changes and technologies evolve.") tests after the quicker running tests have passed successfully. The automation should create a new environment, set up initial conditions such as test data, and then run a series of benchmarks and load tests. Results from these tests should be tied back to the build so you can track [performance](https://wa.aws.amazon.com/wat.pillar.performance.en.html "The ability to use computing resources efficiently to meet system requirements, and to maintain that efficiency as demand changes and technologies evolve.") changes over time. For long running tests, you can make this part of the pipeline asynchronous from the rest of the build. Alternatively, you could run [performance](https://wa.aws.amazon.com/wat.pillar.performance.en.html "The ability to use computing resources efficiently to meet system requirements, and to maintain that efficiency as demand changes and technologies evolve.") tests overnight using Amazon EC2 Spot Instances.

**Load generation:** You should create a series of test scripts that replicate synthetic or prerecorded user journeys. These scripts should be idempotent and not coupled, and you might need to include pre-warming scripts to yield valid results. As much as possible, your test scripts should replicate the behavior of usage in production. You can use software or software-as-a-service (SaaS) solutions to generate the load. Consider using AWS Marketplace solutions and Spot Instances — they can be [cost](https://wa.aws.amazon.com/wat.pillar.costOptimization.en.html "The ability to run systems to deliver business value at the lowest price point.")-effective ways to generate the load.

**[Performance](https://wa.aws.amazon.com/wat.pillar.performance.en.html "The ability to use computing resources efficiently to meet system requirements, and to maintain that efficiency as demand changes and technologies evolve.") visibility:** Key metrics should be visible to your team, especially metrics against each build version. This allows you to see any significant positive or negative trend over time. You should also display metrics on the number of errors or exceptions to make sure you are testing a working system.

**Visualization:** Use visualization techniques that make it clear where [performance](https://wa.aws.amazon.com/wat.pillar.performance.en.html "The ability to use computing resources efficiently to meet system requirements, and to maintain that efficiency as demand changes and technologies evolve.") issues, hot spots, wait states, or low utilization is occurring. Overlay [performance](https://wa.aws.amazon.com/wat.pillar.performance.en.html "The ability to use computing resources efficiently to meet system requirements, and to maintain that efficiency as demand changes and technologies evolve.") metrics over [architecture](https://wa.aws.amazon.com/wat.concept.architecture.en.html "How components interact and communicate.") diagrams — call graphs or code can help identify issues quickly.

This [performance](https://wa.aws.amazon.com/wat.pillar.performance.en.html "The ability to use computing resources efficiently to meet system requirements, and to maintain that efficiency as demand changes and technologies evolve.") review process can be implemented as a simple extension of your existing deployment pipeline and then evolved over time as your testing requirements become more sophisticated. For future [architectures](https://wa.aws.amazon.com/wat.concept.architecture.en.html "How components interact and communicate."), you can generalize your approach and reuse the same process and artifacts.

[Architectures](https://wa.aws.amazon.com/wat.concept.architecture.en.html "How components interact and communicate.") performing poorly is usually the result of a non-existent or broken [performance](https://wa.aws.amazon.com/wat.pillar.performance.en.html "The ability to use computing resources efficiently to meet system requirements, and to maintain that efficiency as demand changes and technologies evolve.") review process. If your [architecture](https://wa.aws.amazon.com/wat.concept.architecture.en.html "How components interact and communicate.") is performing poorly, implementing a [performance](https://wa.aws.amazon.com/wat.pillar.performance.en.html "The ability to use computing resources efficiently to meet system requirements, and to maintain that efficiency as demand changes and technologies evolve.") review process will allow you to apply Deming’s plan-do-check-act (PDCA) cycle to drive iterative improvement.

**Continual optimization:** Adopt a culture to continually optimize the [performance efficiency](https://wa.aws.amazon.com/wat.pillar.performance.en.html "The ability to use computing resources efficiently to meet system requirements, and to maintain that efficiency as demand changes and technologies evolve.") of your cloud [workload](https://wa.aws.amazon.com/wat.concept.workload.en.html "The set of components that together deliver business value.").

## Resources

Refer to the following resources to learn more about our best practices for Performance Efficiency.

 [Performance Efficiency Pillar](https://d1.awsstatic.com/whitepapers/architecture/AWS-Performance-Efficiency-Pillar.pdf?ref=wellarchitected)  
 [Amazon S3 Performance Optimization](http://docs.aws.amazon.com/AmazonS3/latest/dev/PerformanceOptimization.html?ref=wellarchitected)  
 [Amazon EBS Volume Performance](http://docs.aws.amazon.com/AWSEC2/latest/UserGuide/EBSPerformance.html?ref=wellarchitected)  
 [Well-Architected Labs - Performance Efficiency](https://wellarchitectedlabs.com/performance-efficiency?ref=wellarchitected)  
 [AWS re:Invent 2019: Amazon EC2 foundations (CMP211-R2)](https://www.youtube.com/watch?v=kMMybKqC2Y0&ref=wellarchitected)  
 [AWS re:Invent 2019: Leadership session: Storage state of the union (STG201-L)](https://www.youtube.com/watch?v=39vAsGi6eEI&ref=wellarchitected)  
 [AWS re:Invent 2019: Leadership session: AWS purpose-built databases (DAT209-L)](https://www.youtube.com/watch?v=q81TVuV5u28&ref=wellarchitected)  
 [AWS re:Invent 2019: Connectivity to AWS and hybrid AWS network architectures (NET317-R1)](https://www.youtube.com/watch?v=eqW6CPb58gs&ref=wellarchitected)  
 [AWS re:Invent 2019: Powering next-gen Amazon EC2: Deep dive into the Nitro system (CMP303-R2)](https://www.youtube.com/watch?v=rUY-00yFlE4&ref=wellarchitected)  
 [AWS re:Invent 2019: Scaling up to your first 10 million users (ARC211-R)](https://www.youtube.com/watch?v=kKjm4ehYiMs&ref=wellarchitected)