The Cost Optimization pillar includes the ability to run systems to deliver business value at the lowest price point.

The cost optimization pillar provides an overview of design principles, [best practices](https://wa.aws.amazon.com/wat.concept.best-practice.en.html "Proven ways of achieving successful outcomes."), and questions. You can find prescriptive guidance on implementation in the Cost Optimization Pillar whitepaper .

## Design Principles

There are five design principles for cost optimization in the cloud:

- **Implement Cloud Financial Management**: To achieve financial success and accelerate business value realization in the cloud, you need to invest in Cloud Financial Management /Cost Optimization. Your organization needs to dedicate time and resources to build capability in this new domain of technology and usage management. Similar to your [Security](https://wa.aws.amazon.com/wat.pillar.security.en.html "The ability to protect data, systems, and assets to take advantage of cloud technologies to improve your security.") or [Operational Excellence](https://wa.aws.amazon.com/wat.pillar.operationalExcellence.en.html "The ability to support development and run workloads effectively, gain insight into their operations, and to continuously improve supporting processes and procedures to deliver business value.") capability, you need to build capability through knowledge building, programs, resources, and processes to become a cost-efficient organization.
    
- **Adopt a consumption model**: Pay only for the computing resources that you require and increase or decrease usage depending on business requirements, not by using elaborate forecasting. For example, development and test environments are typically only used for eight hours a day during the work week. You can stop these resources when they are not in use for a potential cost savings of 75% (40 hours versus 168 hours).
    
- **Measure overall efficiency**: Measure the business output of the [workload](https://wa.aws.amazon.com/wat.concept.workload.en.html "The set of components that together deliver business value.") and the costs associated with delivering it. Use this measure to know the gains you make from increasing output and reducing costs.
    
- **Stop spending money on undifferentiated heavy lifting**: AWS does the heavy lifting of data center [operations](https://wa.aws.amazon.com/wat.pillar.operationalExcellence.en.html "The ability to support development and run workloads effectively, gain insight into their operations, and to continuously improve supporting processes and procedures to deliver business value.") like racking, stacking, and powering servers. It also removes the operational burden of managing operating systems and applications with managed services. This allows you to focus on your customers and business projects rather than on IT infrastructure.
    
- **Analyze and attribute expenditure**: The cloud makes it easier to accurately identify the usage and cost of systems, which then allows transparent attribution of IT costs to individual [workload](https://wa.aws.amazon.com/wat.concept.workload.en.html "The set of components that together deliver business value.") owners. This helps measure return on investment (ROI) and gives [workload](https://wa.aws.amazon.com/wat.concept.workload.en.html "The set of components that together deliver business value.") owners an opportunity to optimize their resources and reduce costs.
    

## Definition

There are five best practice areas for cost optimization in the cloud:

- [Practice Cloud Financial Management](https://wa.aws.amazon.com/wat.pillar.costOptimization.en.html#cost.cfm)
- [Expenditure and usage awareness](https://wa.aws.amazon.com/wat.pillar.costOptimization.en.html#cost.awarness)
- [Cost-effective resources](https://wa.aws.amazon.com/wat.pillar.costOptimization.en.html#cost.resources)
- [Manage demand and supply resources](https://wa.aws.amazon.com/wat.pillar.costOptimization.en.html#cost.demandsupply)
- [Optimize over time](https://wa.aws.amazon.com/wat.pillar.costOptimization.en.html#cost.optimize)

As with the other pillars within the Well-Architected Framework, there are trade-offs to consider, for example, whether to optimize for speed-to-market or for cost. In some cases, it’s best to optimize for speed—going to market quickly, shipping new features, or simply meeting a deadline—rather than investing in up-front cost optimization. Design decisions are sometimes directed by haste rather than data, and the temptation always exists to overcompensate “just in case” rather than spend time benchmarking for the most cost-optimal deployment. This might lead to over-provisioned and under-optimized deployments. However, this is a reasonable choice when you need to “lift and shift” resources from your on-premises environment to the cloud and then optimize afterwards. Investing the right amount of effort in a cost optimization strategy up front allows you to realize the economic benefits of the cloud more readily by ensuring a consistent adherence to [best practices](https://wa.aws.amazon.com/wat.concept.best-practice.en.html "Proven ways of achieving successful outcomes.") and avoiding unnecessary over provisioning. The following sections provide techniques and [best practices](https://wa.aws.amazon.com/wat.concept.best-practice.en.html "Proven ways of achieving successful outcomes.") for both the initial and ongoing implementation of Cloud Financial Management and cost optimization of your [workloads](https://wa.aws.amazon.com/wat.concept.workload.en.html "The set of components that together deliver business value.").

## Best Practices

### Practice Cloud Financial Management

With the adoption of cloud, technology teams innovate faster due to shortened approval, procurement, and infrastructure deployment cycles. A new approach to financial management in the cloud is required to realize business value and financial success. This approach is Cloud Financial Management, and builds capability across your organization by implementing organizational wide knowledge building, programs, resources, and processes.

Many organizations are composed of many different units with different priorities. The ability to align your organization to an agreed set of financial objectives, and provide your organization the mechanisms to meet them, will create a more efficient organization. A capable organization will innovate and build faster, be more agile and adjust to any internal or external factors.

In AWS you can use [Cost](https://wa.aws.amazon.com/wat.pillar.costOptimization.en.html "The ability to run systems to deliver business value at the lowest price point.") Explorer, and optionally Amazon Athena and Amazon QuickSight with the [Cost](https://wa.aws.amazon.com/wat.pillar.costOptimization.en.html "The ability to run systems to deliver business value at the lowest price point.") and Usage Report (CUR), to provide [cost](https://wa.aws.amazon.com/wat.pillar.costOptimization.en.html "The ability to run systems to deliver business value at the lowest price point.") and usage awareness throughout your organization. AWS Budgets provides proactive notifications for [cost](https://wa.aws.amazon.com/wat.pillar.costOptimization.en.html "The ability to run systems to deliver business value at the lowest price point.") and usage. The AWS blogs provide information on new services and features to ensure you keep up to date with new service releases.

The following questions focus on these considerations for cost optimization.

|   |
|---|
|[**COST 1:** How do you implement cloud financial management?](https://wa.aws.amazon.com/wat.question.COST_1.en.html)|

When building a [cost optimization](https://wa.aws.amazon.com/wat.pillar.costOptimization.en.html "The ability to run systems to deliver business value at the lowest price point.") function, use members and supplement the team with experts in CFM and CO. Existing team members will understand how the organization currently functions and how to rapidly implement improvements. Also consider including people with supplementary or specialist skill sets, such as analytics and project management.

When implementing [cost](https://wa.aws.amazon.com/wat.pillar.costOptimization.en.html "The ability to run systems to deliver business value at the lowest price point.") awareness in your organization, improve or build on existing programs and processes. It is much faster to add to what exists than to build new processes and programs. This will result in achieving outcomes much faster.

### Expenditure and usage awareness

The increased flexibility and agility that the cloud enables encourages innovation and fast-paced development and deployment. It eliminates the manual processes and time associated with provisioning on-premises infrastructure, including identifying hardware specifications, negotiating price quotations, managing purchase orders, scheduling shipments, and then deploying the resources. However, the ease of use and virtually unlimited on-demand capacity requires a new way of thinking about expenditures.

Many businesses are composed of multiple systems run by various teams. The capability to attribute resource [costs](https://wa.aws.amazon.com/wat.pillar.costOptimization.en.html "The ability to run systems to deliver business value at the lowest price point.") to the individual organization or product owners drives efficient usage behavior and helps reduce waste. Accurate [cost](https://wa.aws.amazon.com/wat.pillar.costOptimization.en.html "The ability to run systems to deliver business value at the lowest price point.") attribution allows you to know which products are truly profitable, and allows you to make more informed decisions about where to allocate budget.

In AWS, you create an account structure with AWS Organizations or AWS Control Tower, which provides separation and assists in allocation of your [costs](https://wa.aws.amazon.com/wat.pillar.costOptimization.en.html "The ability to run systems to deliver business value at the lowest price point.") and usage. You can also use resource [tagging](https://wa.aws.amazon.com/wat.concept.tag.en.html "Assign metadata to AWS resources to categorize and organize.") to apply business and organization information to your usage and [cost](https://wa.aws.amazon.com/wat.pillar.costOptimization.en.html "The ability to run systems to deliver business value at the lowest price point."). Use AWS [Cost](https://wa.aws.amazon.com/wat.pillar.costOptimization.en.html "The ability to run systems to deliver business value at the lowest price point.") Explorer for visibility into your [cost](https://wa.aws.amazon.com/wat.pillar.costOptimization.en.html "The ability to run systems to deliver business value at the lowest price point.") and usage, or create customized dashboards and analytics with Amazon Athena and Amazon QuickSight. Controlling your [cost](https://wa.aws.amazon.com/wat.pillar.costOptimization.en.html "The ability to run systems to deliver business value at the lowest price point.") and usage is done by notifications through AWS Budgets, and controls using AWS Identity and Access Management (IAM), and Service Quotas.

The following questions focus on these considerations for cost optimization.

|   |
|---|
|[**COST 2:** How do you govern usage?](https://wa.aws.amazon.com/wat.question.COST_2.en.html)|
|[**COST 3:** How do you monitor your cost and usage?](https://wa.aws.amazon.com/wat.question.COST_3.en.html)|
|[**COST 4:** How do you decommission resources?](https://wa.aws.amazon.com/wat.question.COST_4.en.html)|

You can use [cost allocation tags](https://wa.aws.amazon.com/wat.concept.costalloctag.en.html "Organize your resource costs on your cost allocation report") to categorize and track your AWS usage and [costs](https://wa.aws.amazon.com/wat.pillar.costOptimization.en.html "The ability to run systems to deliver business value at the lowest price point."). When you apply tags to your AWS resources (such as [EC2 instances](https://wa.aws.amazon.com/wat.concept.ec2-instance.en.html "A compute instance in the Amazon EC2 service. Other AWS services use the term EC2 instance to distinguish these instances from other types of instances they support.") or S3 buckets), AWS generates a [cost](https://wa.aws.amazon.com/wat.pillar.costOptimization.en.html "The ability to run systems to deliver business value at the lowest price point.") and usage report with your usage and your tags. You can apply tags that represent organization categories (such as [cost](https://wa.aws.amazon.com/wat.pillar.costOptimization.en.html "The ability to run systems to deliver business value at the lowest price point.") centers, [workload](https://wa.aws.amazon.com/wat.concept.workload.en.html "The set of components that together deliver business value.") names, or owners) to organize your [costs](https://wa.aws.amazon.com/wat.pillar.costOptimization.en.html "The ability to run systems to deliver business value at the lowest price point.") across multiple services.

Ensure you use the right level of detail and granularity in [cost](https://wa.aws.amazon.com/wat.pillar.costOptimization.en.html "The ability to run systems to deliver business value at the lowest price point.") and usage reporting and monitoring. For high level insights and trends, use daily granularity with AWS [Cost](https://wa.aws.amazon.com/wat.pillar.costOptimization.en.html "The ability to run systems to deliver business value at the lowest price point.") Explorer. For deeper analysis and inspection use hourly granularity in AWS [Cost](https://wa.aws.amazon.com/wat.pillar.costOptimization.en.html "The ability to run systems to deliver business value at the lowest price point.") Explorer, or Amazon Athena and Amazon QuickSight with the [Cost](https://wa.aws.amazon.com/wat.pillar.costOptimization.en.html "The ability to run systems to deliver business value at the lowest price point.") and Usage Report (CUR) at an hourly granularity.

Combining tagged resources with entity lifecycle tracking (employees, projects) makes it possible to identify orphaned resources or projects that are no longer generating value to the organization and should be decommissioned. You can set up billing alerts to notify you of predicted overspending.

### Cost-effective resources

Using the appropriate instances and resources for your [workload](https://wa.aws.amazon.com/wat.concept.workload.en.html "The set of components that together deliver business value.") is key to [cost](https://wa.aws.amazon.com/wat.pillar.costOptimization.en.html "The ability to run systems to deliver business value at the lowest price point.") savings. For example, a reporting process might take five hours to run on a smaller server but one hour to run on a larger server that is twice as expensive. Both servers give you the same outcome, but the smaller server incurs more [cost](https://wa.aws.amazon.com/wat.pillar.costOptimization.en.html "The ability to run systems to deliver business value at the lowest price point.") over time.

A well-architected [workload](https://wa.aws.amazon.com/wat.concept.workload.en.html "The set of components that together deliver business value.") uses the most [cost](https://wa.aws.amazon.com/wat.pillar.costOptimization.en.html "The ability to run systems to deliver business value at the lowest price point.")-effective resources, which can have a significant and positive economic impact. You also have the opportunity to use managed services to reduce [costs](https://wa.aws.amazon.com/wat.pillar.costOptimization.en.html "The ability to run systems to deliver business value at the lowest price point."). For example, rather than maintaining servers to deliver email, you can use a service that charges on a per-message basis.

AWS offers a variety of flexible and [cost](https://wa.aws.amazon.com/wat.pillar.costOptimization.en.html "The ability to run systems to deliver business value at the lowest price point.")-effective pricing options to acquire instances from Amazon EC2 and other services in a way that best fits your needs. _On-Demand Instances_ allow you to pay for compute capacity by the hour, with no minimum commitments required. _Savings Plans and Reserved Instances_ offer savings of up to 75% off On-Demand pricing. With Spot Instances, you can leverage unused Amazon EC2 capacity and offer savings of up to 90% off On-Demand pricing. _Spot Instances_ are appropriate where the system can tolerate using a fleet of servers where individual servers can come and go dynamically, such as stateless web servers, batch processing, or when using HPC and big data.

Appropriate service selection can also reduce usage and [costs](https://wa.aws.amazon.com/wat.pillar.costOptimization.en.html "The ability to run systems to deliver business value at the lowest price point."); such as CloudFront to minimize data transfer, or completely eliminate [costs](https://wa.aws.amazon.com/wat.pillar.costOptimization.en.html "The ability to run systems to deliver business value at the lowest price point."), such as utilizing Amazon Aurora on RDS to remove expensive database licensing [costs](https://wa.aws.amazon.com/wat.pillar.costOptimization.en.html "The ability to run systems to deliver business value at the lowest price point.").

The following questions focus on these considerations for cost optimization.

|   |
|---|
|[**COST 5:** How do you evaluate cost when you select services?](https://wa.aws.amazon.com/wat.question.COST_5.en.html)|
|[**COST 6:** How do you meet cost targets when you select resource type, size and number?](https://wa.aws.amazon.com/wat.question.COST_6.en.html)|
|[**COST 7:** How do you use pricing models to reduce cost?](https://wa.aws.amazon.com/wat.question.COST_7.en.html)|
|[**COST 8:** How do you plan for data transfer charges?](https://wa.aws.amazon.com/wat.question.COST_8.en.html)|

By factoring in [cost](https://wa.aws.amazon.com/wat.pillar.costOptimization.en.html "The ability to run systems to deliver business value at the lowest price point.") during service selection, and using tools such as [Cost](https://wa.aws.amazon.com/wat.pillar.costOptimization.en.html "The ability to run systems to deliver business value at the lowest price point.") Explorer and AWS Trusted Advisor to regularly review your AWS usage, you can actively monitor your utilization and adjust your deployments accordingly.

### Manage demand and supply resources

When you move to the cloud, you pay only for what you need. You can supply resources to match the [workload](https://wa.aws.amazon.com/wat.concept.workload.en.html "The set of components that together deliver business value.") demand at the time they’re needed, this eliminates the need for [costly](https://wa.aws.amazon.com/wat.pillar.costOptimization.en.html "The ability to run systems to deliver business value at the lowest price point.") and wasteful over provisioning. You can also modify the demand, using a throttle, buffer, or queue to smooth the demand and serve it with less resources resulting in a lower [cost](https://wa.aws.amazon.com/wat.pillar.costOptimization.en.html "The ability to run systems to deliver business value at the lowest price point."), or process it at a later time with a batch service.

In AWS, you can automatically provision resources to match the [workload](https://wa.aws.amazon.com/wat.concept.workload.en.html "The set of components that together deliver business value.") demand. Auto Scaling using demand or time-based approaches allow you to add and remove resources as needed. If you can anticipate changes in demand, you can save more money and ensure your resources match your [workload](https://wa.aws.amazon.com/wat.concept.workload.en.html "The set of components that together deliver business value.") needs. You can use Amazon API Gateway to implement throttling, or Amazon SQS to implementing a queue in your [workload](https://wa.aws.amazon.com/wat.concept.workload.en.html "The set of components that together deliver business value."). These will both allow you to modify the demand on your [workload](https://wa.aws.amazon.com/wat.concept.workload.en.html "The set of components that together deliver business value.") [components](https://wa.aws.amazon.com/wat.concept.component.en.html "The code, configuration and AWS Resources that deliver against a business requirement.").

The following questions focus on these considerations for cost optimization.

|   |
|---|
|[**COST 9:** How do you manage demand, and supply resources?](https://wa.aws.amazon.com/wat.question.COST_9.en.html)|

When designing to modify demand and supply resources, actively think about the patterns of usage, the time it takes to provision new resources, and the predictability of the demand pattern. When managing demand, ensure you have a correctly sized queue or buffer, and that you are responding to [workload](https://wa.aws.amazon.com/wat.concept.workload.en.html "The set of components that together deliver business value.") demand in the required amount of time.

### Optimize over time

As AWS releases new services and features, it's a [best practice](https://wa.aws.amazon.com/wat.concept.best-practice.en.html "Proven ways of achieving successful outcomes.") to review your existing architectural decisions to ensure they continue to be the most [cost](https://wa.aws.amazon.com/wat.pillar.costOptimization.en.html "The ability to run systems to deliver business value at the lowest price point.") effective. As your requirements change, be aggressive in decommissioning resources, entire services, and systems that you no longer require.

Implementing new features or resource types can optimize your [workload](https://wa.aws.amazon.com/wat.concept.workload.en.html "The set of components that together deliver business value.") incrementally, while minimizing the effort required to implement the change. This provides continual improvements in efficiency over time and ensures you remain on the most updated technology to reduce operating [costs](https://wa.aws.amazon.com/wat.pillar.costOptimization.en.html "The ability to run systems to deliver business value at the lowest price point."). You can also replace or add new [components](https://wa.aws.amazon.com/wat.concept.component.en.html "The code, configuration and AWS Resources that deliver against a business requirement.") to the [workload](https://wa.aws.amazon.com/wat.concept.workload.en.html "The set of components that together deliver business value.") with new services. This can provide significant increases in efficiency, so it's essential to regularly review your [workload](https://wa.aws.amazon.com/wat.concept.workload.en.html "The set of components that together deliver business value."), and implement new services and features.

The following questions focus on these considerations for cost optimization.

|   |
|---|
|[**COST 10:** How do you evaluate new services?](https://wa.aws.amazon.com/wat.question.COST_10.en.html)|
|[**COST 11:** How do you evaluate the cost of effort?](https://wa.aws.amazon.com/wat.question.COST_11.en.html)|

When regularly reviewing your deployments, assess how newer services can help save you money. For example, Amazon Aurora on RDS can reduce [costs](https://wa.aws.amazon.com/wat.pillar.costOptimization.en.html "The ability to run systems to deliver business value at the lowest price point.") for [relational databases](https://wa.aws.amazon.com/wat.concept.relational.en.html "A relational database is a collection of data items with pre-defined relationships between them."). Using serverless such as Lambda can remove the need to operate and manage instances to run code.

## Resources

Refer to the following resources to learn more about our best practices for Cost Optimization.

 [Cost Optimization Pillar](https://d1.awsstatic.com/whitepapers/architecture/AWS-Cost-Optimization-Pillar.pdf?ref=wellarchitected)  
 [AWS Well-Architected Cost Optimization Labs](https://wellarchitectedlabs.com/Cost/?ref=wellarchitected)  
 [Well-Architected Tool](https://console.aws.amazon.com/wellarchitected/?ref=wellarchitected)  
 [AWS Cost Management Blog](https://aws.amazon.com/blogs/aws-cost-management/?ref=wellarchitected)  
 [AWS Billing and Cost Management](https://docs.aws.amazon.com/awsaccountbilling/latest/aboutv2/billing-what-is.html?ref=wellarchitected)  
 [AWS Tagging Strategies](https://aws.amazon.com/answers/account-management/aws-tagging-strategies/?ref=wellarchitected)  
 [Getting Started with Amazon EC2 Spot Instances](https://aws.amazon.com/ec2/spot/getting-started/?ref=wellarchitected#bestpractices)  
 [AWS Documentation](https://docs.aws.amazon.com/index.html?ref=wellarchitected)