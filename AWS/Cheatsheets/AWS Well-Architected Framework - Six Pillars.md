Clipped from: [https://tutorialsdojo.com/aws-well-architected-framework-six-pillars/](https://tutorialsdojo.com/aws-well-architected-framework-six-pillars/)

## What is the AWS Well-Architected Framework?

The AWS Well-Architected Framework is basically a body of knowledge that describes the various design principles, key concepts, design and architectural best practices that can help companies design and run highly efficient workloads in the AWS platform. This framework ensures that the company’s cloud architecture is in accordance with the AWS best practices. It also comes with related AWS features, services and tools that you can utilize to measure the overall efficiency of your design. The AWS Well-Architected Framework will empower you to improve your existing IT infrastructure in terms of your overall operations, security, reliability, efficiency, cost optimization, and sustainability.

Having well-architected systems greatly increases the plausibility of business success, which is why AWS created the AWS Well-Architected Framework. This framework is composed of six pillars that help you understand the pros and cons of the decisions you make while building cloud architectures and systems on the AWS platform. You will learn the architectural best practices for designing and operating reliable, efficient, cost-effective and secure systems in the cloud by using the framework. This framework also provides a way to consistently measure your architectures against best practices and identify areas for improvement.

## How do you use the AWS Well-Architected Framework?

In its raw form, the AWS Well-Architected Framework is simply a body of knowledge that is compiled in a single PDF document or included in the online AWS documentation. It contains specific best practices, design patterns, and other concepts that you can use to review your existing cloud architecture. The AWS Well-Architected Framework contains key architectural questions that can help you verify and measure the quality of your systems. 

Say, for example, you are developing an online solution that handles sensitive financial information. Your system has passed all the integration tests and is finally ready for production deployment any time soon. However, you still want to ensure that your cloud infrastructure in AWS is indeed secure as part of your corporate security compliance.

You can check the security pillar of the AWS Well-Architected Framework that focuses on protecting your data, files, and overall systems. This includes key topics on data integrity, managing user permissions, and establishing controls to detect security incidents.

In essence, you can improve your cloud designs by simply answering the evaluation questions and following the best practices provided by this framework. These questions will shed light on your existing or new architecture in the AWS Cloud. It has questions like:

- “How do you protect your data at rest?”
- “How do you protect your data in transit?”
- “How do you manage identities for people and machines?”
- …and so on and so forth.

Your answer to these questions can show if your cloud architecture is secure or not. If you responded “I don’t know” in the “How do you protect your data at rest?” question, then that means your architecture is not secure and has a high number of security vulnerabilities. This signifies that you don’t employ encryption and tokenization schemes in your system.

The same goes for the “How do you protect your data in transit?” query. If you answer that you do not protect your data in transit, then that indicates your architecture has no firewall rules, network authentication, secure key management, and other mechanisms to keep your sensitive data safe as it traverses through different systems and networks. With this realization, you can now resolve the deficiencies in your system by following the prescriptive guidance provided by the AWS Well-Architected Framework.

## What are the AWS Well-Architected Framework Pillars?

![[Pasted image 20231024165328.png]]
### 1. Operational Excellence

- The ability to run and monitor systems to deliver business value and to continually improve supporting processes and procedures.
- There are four best practice areas and tools for operational excellence in the cloud:

- Organization – AWS Cloud Compliance, [AWS Trusted Advisor](https://tutorialsdojo.com/aws-trusted-advisor/), [AWS Organizations](https://tutorialsdojo.com/aws-organizations/)
- Prepare – [AWS Config](https://tutorialsdojo.com/aws-config/)
- Operate – [Amazon CloudWatch](https://tutorialsdojo.com/amazon-cloudwatch/)
- Evolve – Amazon Elasticsearch Service

- Key AWS service:

- [AWS CloudFormation](https://tutorialsdojo.com/aws-cloudformation/) for creating templates. (See AWS Management Tools Cheat Sheet)

### 2. Security

### 3. Reliability

- The ability of a system to recover from infrastructure or service disruptions, dynamically acquire computing resources to meet demand, and mitigate disruptions such as misconfigurations or transient network issues.
- There are four best practice areas and tools for reliability in the cloud:

- Foundations – IAM, Amazon VPC, AWS Trusted Advisor, AWS Shield
- Change Management – AWS CloudTrail, AWS Config, Auto Scaling, Amazon CloudWatch
- Failure Management – AWS CloudFormation, Amazon S3, AWS KMS, Amazon Glacier
- Workload Architecture –  AWS SDK, [AWS Lambda](https://tutorialsdojo.com/aws-lambda/)

- Key AWS service:

- Amazon CloudWatch

### 4. Performance Efficiency

- The ability to use computing resources efficiently to meet system requirements, and to maintain that efficiency as demand changes and technologies evolve.
- There are four best practice areas for performance efficiency in the cloud:

- Selection – Auto Scaling for Compute, Amazon EBS and S3 for Storage, Amazon RDS and DynamoDB for Database, Route53, VPC, and AWS Direct Connect for Network
- Review – AWS Blog and What’s New section of the website
- Monitoring –  Amazon CloudWatch
- Tradeoffs – Amazon Elasticache, Amazon CloudFront, [AWS Snowball](https://tutorialsdojo.com/aws-snowball/), Amazon RDS read replicas.

- Key AWS service:

- Amazon CloudWatch

### 5. Cost Optimization

- The ability to avoid or eliminate unneeded cost or suboptimal resources.
- There are five best practice areas and tools for cost optimization in the cloud:

- Cloud Financial Management – [Amazon QuickSight](https://tutorialsdojo.com/amazon-quicksight/), AWS Cost and Usage Report (CUR)
- Cost-Effective Resources – Cost Explorer, Amazon CloudWatch and Trusted Advisor, Amazon Aurora for RDS, [AWS Direct Connect](https://tutorialsdojo.com/aws-direct-connect/) with Amazon CloudFront
- Matching supply and demand – Auto Scaling
- Expenditure Awareness –  AWS Cost Explorer, AWS Budgets
- Optimizing Over Time – AWS News Blog and the What’s New section on the AWS website, AWS Trusted Advisor

- Key AWS service:

- Cost Explorer

### 6. Sustainability

- The ability to increase efficiency across all components of a workload by maximizing the benefits from the provisioned resources.
- There are six best practice areas for sustainability in the cloud:

- Region Selection – [AWS Global Infrastructure](https://tutorialsdojo.com/aws-global-infrastructure/)
- User Behavior Patterns – Auto Scaling, Elastic Load Balancing
- Software and Architecture Patterns – AWS Design Principles
- Data Patterns – Amazon EBS,  [Amazon EFS](https://tutorialsdojo.com/amazon-efs/), Amazon FSx, Amazon S3
- Hardware Patterns – [Amazon EC2](https://tutorialsdojo.com/amazon-elastic-compute-cloud-amazon-ec2/), AWS Elastic Beanstalk
- Development and Deployment Process – AWS CloudFormation

- Key AWS service:

- Amazon EC2 Auto Scaling

## Related AWS Certified Cloud Practitioner CLF-C01 Resources:

Are you preparing for your AWS Certified Cloud Practitioner CLF-C01 Exam?

Get Actual AWS Hands-On Labs, Full 65-Question Timed Practice Test, Flashcards plus many more with our highly-visual [AWS Certified Cloud Practitioner CLF-C01 Video course](https://portal.tutorialsdojo.com/courses/aws-certified-cloud-practitioner-clf-c01-video-course/) — all for a price of lunch!

## Reference:

[https://d1.awsstatic.com/whitepapers/architecture/AWS_Well-Architected_Framework.pdf](https://d1.awsstatic.com/whitepapers/architecture/AWS_Well-Architected_Framework.pdf)