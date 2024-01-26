Clipped from: [https://tutorialsdojo.com/aws-serverless-application-repository/](https://tutorialsdojo.com/aws-serverless-application-repository/)

- The AWS Serverless Application Repository is a managed repository for deploying and publishing serverless applications.
- You can also use pre-built applications instead of cloning, building, packaging, and publishing source code to AWS before deploying it.
- Each application includes an AWS SAM template that specifies the AWS resources that will be used.

## Publishing Applications

- Use an AWS SAM template to define your application.
- To publish a serverless app, you can use the following to upload your code:

- AWS Management Console
- AWS SAM CLI
- AWS SDKs

- When you publish an app, it is initially set to private and only accessible to the AWS account that created it.
- You can deploy and share your app by setting it to:

- Private

- Not shared with any other AWS accounts.
- Only accessible to the AWS account that created it.
- You have permission to deploy applications created with your AWS account.

- Privately Shared

- Shared to a specific set of AWS accounts.
- Accessible in the AWS Region in which they are created.
- You have permission to deploy applications shared with your AWS account.

- Publicly Shared

- Shared with everyone.
- Accessible to all AWS Regions.
- You have permission to deploy any publicly shared application.

- A link to the source code is included in publicly shared applications.
- If the public app is deployed to another Region, AWS SAR copies the app deployment artifacts to an [Amazon S3](https://tutorialsdojo.com/amazon-s3/) bucket in the destination Region.
- By sharing Lambda layers, you can deploy an instance of your layer to another AWS account.

## Deploying Applications

- To deploy an application, you must have permission to do so (see permissions above).
- Before deploying an app, AWS SAR also checks the application template for:

- [IAM](https://tutorialsdojo.com/aws-identity-and-access-management-iam/) roles
- AWS resource policies
- Nested applications specified by the template

- You can only search for and browse applications for which you have permission:

- Created using your AWS account
- Privately shared with your AWS account
- Publicly shared

- Use AWS Console or AWS CLI to deploy and update applications.

## AWS Serverless Application Repository Monitoring

- Create a trail in [AWS CloudTrail](https://tutorialsdojo.com/aws-cloudtrail/) to capture all API calls.
- Even if you haven’t configured a trail, you can still view the most recent events in the CloudTrail console’s Event history.

## AWS Serverless Application Repository Pricing

- You are charged for AWS resources used in the applications you deploy.

## AWS  Serverless Application Repository Cheat Sheet References:

[https://aws.amazon.com/serverless/serverlessrepo/](https://aws.amazon.com/serverless/serverlessrepo/)  
 [https://docs.aws.amazon.com/serverlessrepo/latest/devguide/what-is-serverlessrepo.html](https://docs.aws.amazon.com/serverlessrepo/latest/devguide/what-is-serverlessrepo.html)