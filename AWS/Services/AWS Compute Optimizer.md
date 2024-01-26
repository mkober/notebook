**AWS Compute Optimizer** recommends optimal AWS resources for your workloads to reduce costs and improve performance by using machine learning to analyze historical utilization metrics. Overprovisioning resources can lead to unnecessary infrastructure costs, and underprovisioning resources can lead to poor application performance. Compute Optimizer generates recommendations for the following resources:

 - Amazon Elastic Compute Cloud (Amazon EC2) instances

 - Amazon EC2 Auto Scaling groups

 - Amazon Elastic Block Store (Amazon EBS) volumes

 - AWS Lambda functions

You must opt-in to have Compute Optimizer analyze your AWS resources. The service supports standalone AWS accounts, member accounts of an organization, and the management account of an organization. After you opt-in, Compute Optimizer begins analyzing the specifications and the utilization metrics of your resources from Amazon CloudWatch for the last 14 days.  For example, for Amazon EC2 instances, Compute Optimizer analyzes the vCPUs, memory, storage, and other specifications.

![](https://media.tutorialsdojo.com/saa_compute_optimizer_recommendations.png)