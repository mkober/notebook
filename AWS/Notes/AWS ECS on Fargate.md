**Amazon ECS on AWS Fargate** is a container orchestration solution that allows the company to execute containerized apps without handling the underlying infrastructure. It handles infrastructure scaling, patching, and provisioning, giving the company more time to focus on creating and deploying applications. This service enables companies to run containerized apps in a serverless environment, where they pay for the resources consumed, making it a cost-effective solution for applications with fluctuating workloads. With ECS on AWS Fargate, you can launch containers on demand, respond quickly to necessary changes, and have the flexibility to scale up or down as needed.

![](https://media.tutorialsdojo.com/public/Amazon_ECS_SL.png)

Amazon Aurora Serverless, on the other hand, is a fully managed, auto-scaling relational database engine that eliminates the need to manage infrastructure, providing the company with cost savings and scalability. It offers an excellent option for hosting databases for applications with unpredictable workloads or low usage patterns. Furthermore, Aurora Serverless scales the database up or down based on the workload, which helps to minimize costs during idle periods. With Aurora Serverless, companies can also achieve high availability, as the database automatically replicates data across multiple Availability Zones. Overall, the combination of Amazon ECS on AWS Fargate and Amazon Aurora Serverless provides companies with a cost-effective, scalable, and reliable infrastructure to run their applications and databases.


### IAM roles for ECS tasks
IAM roles for ECS tasks enabled you to secure your infrastructure by assigning an IAM role directly to the ECS task rather than to the EC2 container instance. This means you can have one task that uses a specific IAM role for access to S3 and one task that uses an IAM role to access DynamoDB.

IAM roles can be specified at the container and task level on EC2 launch type and the task level on Fargate launch type.

![](https://digitalcloud.training/wp-content/uploads/2020/05/Picture-1-13.jpg)