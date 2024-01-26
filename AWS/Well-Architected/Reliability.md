The Reliability pillar includes includes the ability of a workload to perform its intended function correctly and consistently when it’s expected to. this includes the ability to operate and test the workload through its total lifecycle. this paper provides in-depth, best practice guidance for implementing reliable workloads on aws.

The reliability pillar provides an overview of design principles, [best practices](https://wa.aws.amazon.com/wat.concept.best-practice.en.html "Proven ways of achieving successful outcomes."), and questions. You can find prescriptive guidance on implementation in the Reliability Pillar whitepaper.

## Design Principles

There are five design principles for reliability in the cloud:

- **Automatically recover from failure**: By monitoring a [workload](https://wa.aws.amazon.com/wat.concept.workload.en.html "The set of components that together deliver business value.") for key [performance](https://wa.aws.amazon.com/wat.pillar.performance.en.html "The ability to use computing resources efficiently to meet system requirements, and to maintain that efficiency as demand changes and technologies evolve.") indicators (KPIs), you can trigger automation when a threshold is breached. These KPIs should be a measure of business value, not of the technical aspects of the operation of the service. This allows for automatic notification and tracking of failures, and for automated recovery processes that work around or repair the failure. With more sophisticated automation, it’s possible to anticipate and remediate failures before they occur.
    
- **Test recovery procedures**: In an on-premises environment, testing is often conducted to prove that the [workload](https://wa.aws.amazon.com/wat.concept.workload.en.html "The set of components that together deliver business value.") works in a particular scenario. Testing is not typically used to validate recovery strategies. In the cloud, you can test how your [workload](https://wa.aws.amazon.com/wat.concept.workload.en.html "The set of components that together deliver business value.") fails, and you can validate your recovery procedures. You can use automation to simulate different failures or to recreate scenarios that led to failures before. This approach exposes failure pathways that you can test and fix before a real failure scenario occurs, thus reducing risk.
    
- **Scale horizontally to increase aggregate workload availability**: Replace one large resource with multiple small resources to reduce the impact of a single failure on the overall [workload](https://wa.aws.amazon.com/wat.concept.workload.en.html "The set of components that together deliver business value."). Distribute requests across multiple, smaller resources to ensure that they don’t share a common point of failure.
    
- **Stop guessing capacity**: A common cause of failure in on-premises [workloads](https://wa.aws.amazon.com/wat.concept.workload.en.html "The set of components that together deliver business value.") is resource saturation, when the demands placed on a [workload](https://wa.aws.amazon.com/wat.concept.workload.en.html "The set of components that together deliver business value.") exceed the capacity of that [workload](https://wa.aws.amazon.com/wat.concept.workload.en.html "The set of components that together deliver business value.") (this is often the objective of denial of service attacks). In the cloud, you can monitor demand and [workload](https://wa.aws.amazon.com/wat.concept.workload.en.html "The set of components that together deliver business value.") utilization, and automate the addition or removal of resources to maintain the optimal level to satisfy demand without over- or under-provisioning. There are still limits, but some quotas can be controlled and others can be managed (see Manage Service Quotas and Constraints).
    
- **Manage change in automation**: Changes to your infrastructure should be made using automation. The changes that need to be managed include changes to the automation, which then can be tracked and reviewed.
    

## Definition

There are four best practice areas for reliability in the cloud:

- [Foundations](https://wa.aws.amazon.com/wat.pillar.reliability.en.html#rel.foundations)
- [Workload Architecture](https://wa.aws.amazon.com/wat.pillar.reliability.en.html#rel.architecture)
- [Change Management](https://wa.aws.amazon.com/wat.pillar.reliability.en.html#rel.change)
- [Failure Management](https://wa.aws.amazon.com/wat.pillar.reliability.en.html#rel.failure)

To achieve reliability you must start with the foundations — an environment where service quotas and network topology accommodate the [workload](https://wa.aws.amazon.com/wat.concept.workload.en.html "The set of components that together deliver business value."). The [workload](https://wa.aws.amazon.com/wat.concept.workload.en.html "The set of components that together deliver business value.") [architecture](https://wa.aws.amazon.com/wat.concept.architecture.en.html "How components interact and communicate.") of the distributed system must be designed to prevent and mitigate failures. The [workload](https://wa.aws.amazon.com/wat.concept.workload.en.html "The set of components that together deliver business value.") must handle changes in demand or requirements, and it must be designed to detect failure and automatically heal itself.

## Best Practices

### Foundations

Foundational requirements are those whose scope extends beyond a single [workload](https://wa.aws.amazon.com/wat.concept.workload.en.html "The set of components that together deliver business value.") or project. Before architecting any system, foundational requirements that influence [reliability](https://wa.aws.amazon.com/wat.concept.c-reliability.en.html "A measure of your workload's ability to provide functionality when desired by the user.") should be in place. For example, you must have sufficient network bandwidth to your data center.

With AWS, most of these foundational requirements are already incorporated or can be addressed as needed. The cloud is designed to be nearly limitless, so it’s the responsibility of AWS to satisfy the requirement for sufficient networking and compute capacity, leaving you free to change resource size and allocations on demand.

The following questions focus on these considerations for reliability.

|   |
|---|
|[**REL 1:** How do you manage service quotas and constraints?](https://wa.aws.amazon.com/wat.question.REL_1.en.html)|
|[**REL 2:** How do you plan your network topology?](https://wa.aws.amazon.com/wat.question.REL_2.en.html)|

For cloud-based [workload](https://wa.aws.amazon.com/wat.concept.workload.en.html "The set of components that together deliver business value.") [architectures](https://wa.aws.amazon.com/wat.concept.architecture.en.html "How components interact and communicate."), there are service quotas (which are also referred to as [service limits](https://wa.aws.amazon.com/wat.concept.service-limits.en.html "Services have limitations to protect the consumer as well as the provider; physical locations have limitations built into their construction.")). These quotas exist to prevent accidentally provisioning more resources than you need and to limit request rates on API [operations](https://wa.aws.amazon.com/wat.pillar.operationalExcellence.en.html "The ability to support development and run workloads effectively, gain insight into their operations, and to continuously improve supporting processes and procedures to deliver business value.") to protect services from abuse. [Workloads](https://wa.aws.amazon.com/wat.concept.workload.en.html "The set of components that together deliver business value.") often exist in multiple environments. You must monitor and manage these quotas for all [workload](https://wa.aws.amazon.com/wat.concept.workload.en.html "The set of components that together deliver business value.") environments. These include multiple cloud environments (both publicly accessible and private) and may include your existing data center infrastructure. Plans must include network considerations, such as intrasystem and intersystem connectivity, public IP address management, private IP address management, and domain name resolution.

### Workload Architecture

A reliable [workload](https://wa.aws.amazon.com/wat.concept.workload.en.html "The set of components that together deliver business value.") starts with upfront design decisions for both software and infrastructure. Your [architecture](https://wa.aws.amazon.com/wat.concept.architecture.en.html "How components interact and communicate.") choices will impact your [workload](https://wa.aws.amazon.com/wat.concept.workload.en.html "The set of components that together deliver business value.") behavior across all five Well-Architected pillars. For [reliability](https://wa.aws.amazon.com/wat.concept.c-reliability.en.html "A measure of your workload's ability to provide functionality when desired by the user."), there are specific patterns you must follow.

With AWS, [workload](https://wa.aws.amazon.com/wat.concept.workload.en.html "The set of components that together deliver business value.") developers have their choice of languages and technologies to use. AWS SDKs take the complexity out of coding by providing language-specific APIs for AWS services. These SDKs, plus the choice of languages, allow developers to implement the [reliability](https://wa.aws.amazon.com/wat.concept.c-reliability.en.html "A measure of your workload's ability to provide functionality when desired by the user.") [best practices](https://wa.aws.amazon.com/wat.concept.best-practice.en.html "Proven ways of achieving successful outcomes.") listed here. Developers can also read about and learn from how Amazon builds and operates software in [The Amazon Builders' Library](https://aws.amazon.com/builders-library/?ref=wellarchitected-ws) .

The following questions focus on these considerations for reliability.

|   |
|---|
|[**REL 3:** How do you design your workload service architecture?](https://wa.aws.amazon.com/wat.question.REL_3.en.html)|
|[**REL 4:** How do you design interactions in a distributed system to prevent failures?](https://wa.aws.amazon.com/wat.question.REL_4.en.html)|
|[**REL 5:** How do you design interactions in a distributed system to mitigate or withstand failures?](https://wa.aws.amazon.com/wat.question.REL_5.en.html)|

Distributed systems rely on communications networks to interconnect [components](https://wa.aws.amazon.com/wat.concept.component.en.html "The code, configuration and AWS Resources that deliver against a business requirement."), such as servers or services. Your [workload](https://wa.aws.amazon.com/wat.concept.workload.en.html "The set of components that together deliver business value.") must operate reliably despite data loss or [latency](https://wa.aws.amazon.com/wat.concept.latency.en.html "A measurement of the amount of time between an action and the result, often between a request and a response.") in these networks. [Components](https://wa.aws.amazon.com/wat.concept.component.en.html "The code, configuration and AWS Resources that deliver against a business requirement.") of the distributed system must operate in a way that does not negatively impact other [components](https://wa.aws.amazon.com/wat.concept.component.en.html "The code, configuration and AWS Resources that deliver against a business requirement.") or the [workload](https://wa.aws.amazon.com/wat.concept.workload.en.html "The set of components that together deliver business value.").

### Change Management

Changes to your [workload](https://wa.aws.amazon.com/wat.concept.workload.en.html "The set of components that together deliver business value.") or its environment must be anticipated and accommodated to achieve reliable operation of the [workload](https://wa.aws.amazon.com/wat.concept.workload.en.html "The set of components that together deliver business value."). Changes include those imposed on your [workload](https://wa.aws.amazon.com/wat.concept.workload.en.html "The set of components that together deliver business value."), such as spikes in demand, as well as those from within, such as feature deployments and [security](https://wa.aws.amazon.com/wat.pillar.security.en.html "The ability to protect data, systems, and assets to take advantage of cloud technologies to improve your security.") patches.

Using AWS, you can monitor the behavior of a [workload](https://wa.aws.amazon.com/wat.concept.workload.en.html "The set of components that together deliver business value.") and automate the response to KPIs. For example, your [workload](https://wa.aws.amazon.com/wat.concept.workload.en.html "The set of components that together deliver business value.") can add additional servers as a [workload](https://wa.aws.amazon.com/wat.concept.workload.en.html "The set of components that together deliver business value.") gains more users. You can control who has permission to make [workload](https://wa.aws.amazon.com/wat.concept.workload.en.html "The set of components that together deliver business value.") changes and audit the history of these changes.

The following questions focus on these considerations for reliability.

|   |
|---|
|[**REL 6:** How do you monitor workload resources?](https://wa.aws.amazon.com/wat.question.REL_6.en.html)|
|[**REL 7:** How do you design your workload to adapt to changes in demand?](https://wa.aws.amazon.com/wat.question.REL_7.en.html)|
|[**REL 8:** How do you implement change?](https://wa.aws.amazon.com/wat.question.REL_8.en.html)|

When you architect a [workload](https://wa.aws.amazon.com/wat.concept.workload.en.html "The set of components that together deliver business value.") to automatically add and remove resources in response to changes in demand, this not only increases [reliability](https://wa.aws.amazon.com/wat.concept.c-reliability.en.html "A measure of your workload's ability to provide functionality when desired by the user.") but also ensures that business success doesn't become a burden. With monitoring in place, your team will be automatically alerted when KPIs deviate from expected norms. Automatic logging of changes to your environment allows you to audit and quickly identify actions that might have impacted [reliability](https://wa.aws.amazon.com/wat.concept.c-reliability.en.html "A measure of your workload's ability to provide functionality when desired by the user."). Controls on change management ensure that you can enforce the rules that deliver the [reliability](https://wa.aws.amazon.com/wat.concept.c-reliability.en.html "A measure of your workload's ability to provide functionality when desired by the user.") you need.

### Failure Management

In any system of reasonable complexity, it is expected that failures will occur. [Reliability](https://wa.aws.amazon.com/wat.concept.c-reliability.en.html "A measure of your workload's ability to provide functionality when desired by the user.") requires that your [workload](https://wa.aws.amazon.com/wat.concept.workload.en.html "The set of components that together deliver business value.") be aware of failures as they occur and take action to avoid impact on [availability](https://wa.aws.amazon.com/wat.concept.availability.en.html "A measurement of a system's ability to provide its designed functionality."). [Workloads](https://wa.aws.amazon.com/wat.concept.workload.en.html "The set of components that together deliver business value.") must be able to both withstand failures and automatically repair issues.

With AWS, you can take advantage of automation to react to monitoring data. For example, when a particular metric crosses a threshold, you can trigger an automated action to remedy the [problem](https://wa.aws.amazon.com/wat.concept.problem.en.html "An event that requires intervention and either recurs or cannot currently be resolved."). Also, rather than trying to diagnose and fix a failed resource that is part of your production environment, you can replace it with a new one and carry out the analysis on the failed resource out of band. Since the cloud enables you to stand up temporary versions of a whole system at low [cost](https://wa.aws.amazon.com/wat.pillar.costOptimization.en.html "The ability to run systems to deliver business value at the lowest price point."), you can use automated testing to verify full recovery processes.

The following questions focus on these considerations for reliability.

|   |
|---|
|[**REL 9:** How do you back up data?](https://wa.aws.amazon.com/wat.question.REL_9.en.html)|
|[**REL 10:** How do you use fault isolation to protect your workload?](https://wa.aws.amazon.com/wat.question.REL_10.en.html)|
|[**REL 11:** How do you design your workload to withstand component failures?](https://wa.aws.amazon.com/wat.question.REL_11.en.html)|
|[**REL 12:** How do you test reliability?](https://wa.aws.amazon.com/wat.question.REL_12.en.html)|
|[**REL 13:** How do you plan for disaster recovery (DR)?](https://wa.aws.amazon.com/wat.question.REL_13.en.html)|

Regularly back up your data and test your backup files to ensure that you can recover from both logical and physical errors. A key to managing failure is the frequent and automated testing of [workloads](https://wa.aws.amazon.com/wat.concept.workload.en.html "The set of components that together deliver business value.") to cause failure, and then observe how they recover. Do this on a regular schedule and ensure that such testing is also triggered after significant [workload](https://wa.aws.amazon.com/wat.concept.workload.en.html "The set of components that together deliver business value.") changes. Actively track KPIs, such as the recovery time objective (RTO) and recovery point objective (RPO), to assess a [workload](https://wa.aws.amazon.com/wat.concept.workload.en.html "The set of components that together deliver business value.")'s [resiliency](https://wa.aws.amazon.com/wat.concept.resiliency.en.html "The ability for a system to recover from a failure induced by load, attacks, and failures.") (especially under failure-testing scenarios). Tracking KPIs will help you identify and mitigate single points of failure. The objective is to thoroughly test your [workload](https://wa.aws.amazon.com/wat.concept.workload.en.html "The set of components that together deliver business value.")-recovery processes so that you are confident that you can recover all your data and continue to serve your customers, even in the face of sustained [problems](https://wa.aws.amazon.com/wat.concept.problem.en.html "An event that requires intervention and either recurs or cannot currently be resolved."). Your recovery processes should be as well exercised as your normal production processes.

## Resources

Refer to the following resources to learn more about our best practices for Reliability.

 [Reliability Pillar: AWS Well-Architected](https://d1.awsstatic.com/whitepapers/architecture/AWS-Reliability-Pillar.pdf?ref=wellarchitected)  
 [AWS Well-Architected Reliability Labs](https://wellarchitectedlabs.com/Reliability/?ref=wellarchitected)  
 [The Amazon Builders' Library: How Amazon builds and operates software](https://aws.amazon.com/builders-library/?ref=wellarchitected)  
 [AWS Documentation](https://docs.aws.amazon.com/index.html?ref=wellarchitected)  
 [AWS Global Infrastructure](https://aws.amazon.com/about-aws/global-infrastructure?ref=wellarchitected)  
 [AWS Auto Scaling: How Scaling Plans Work](https://docs.aws.amazon.com/autoscaling/plans/userguide/how-it-works.html?ref=wellarchitected)  
 [Implementing Microservices on AWS](https://docs.aws.amazon.com/whitepapers/latest/microservices-on-aws/introduction.html?ref=wellarchitected)  
 [What Is AWS Backup?](https://docs.aws.amazon.com/aws-backup/latest/devguide/whatisbackup.html?ref=wellarchitected)