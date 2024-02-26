

Clipped from: [https://aws.amazon.com/blogs/mt/best-practices-for-organizational-units-with-aws-organizations/?sc_channel=EL&sc_campaign=Demo_Deep_Dive_2021_vid&sc_medium=YouTube&sc_content=Video9786&sc_detail=MANAGEMENT_GOVERNANCE&sc_country=US](https://aws.amazon.com/blogs/mt/best-practices-for-organizational-units-with-aws-organizations/?sc_channel=EL&sc_campaign=Demo_Deep_Dive_2021_vid&sc_medium=YouTube&sc_content=Video9786&sc_detail=MANAGEMENT_GOVERNANCE&sc_country=US)

AWS customers look to move quickly and securely when launching new business innovations. The multi-account environment provides guidance to help customers plan their AWS environment. This framework is designed to meet security needs, while maintaining the ability to scale and adapt their environments with changing business demands. The basis of a well-architected multi-account AWS environment is [AWS Organizations](https://aws.amazon.com/organizations/), an AWS service that enables you to centrally manage and govern multiple accounts.

This post dives deep into the recommended architecture of AWS best practices when building your organization. It will explain and illustrate the recommended OU structure and provide specific implementation examples. If you’re interested in a high-level overview of these concepts, we recommend that you review the [Establishing your best practice AWS environment](https://aws.amazon.com/organizations/getting-started/best-practices/) page. If you’d like to learn more about the services that will assist you in operating your multi-account environment, refer to the [Managing the multi-account environment using AWS Organizations and AWS Control Tower](https://aws.amazon.com/blogs/mt/managing-the-multi-account-environment-using-aws-organizations-and-aws-control-tower/) blog. We also recommend you review [Organizing your AWS environment using multiple accounts,](https://docs.aws.amazon.com/whitepapers/latest/organizing-your-aws-environment/organizing-your-aws-environment.html) which provides comprehensive guidance for designing and operating your multi-account environment.

## Why should I set up a multi-account AWS environment?

AWS enables you to experiment, innovate, and scale more quickly, all while providing a flexible and secure cloud environment. As customers build and deploy workloads, they often use multiple accounts to isolate their resources because they provide natural boundaries for security, access, and billing. For example, users outside of your account do not have access to your resources by default. Similarly, the cost of AWS resources that you consume is allocated only to your account. While you may begin your AWS journey with a single account, AWS recommends that you set up multiple accounts, as your workloads grow in size and complexity. Using a multi-account environment is a best practice that offers several benefits:

- Rapid innovation with various requirements: Accounts can be allocated to teams, workloads, or products. Separate accounts can provide custom environments and accommodate the differing security needs for each team.
- Simplified billing: The use of multiple accounts simplifies how you allocate AWS costs. You can use them to identify which projects or services are responsible for AWS charges.
- Flexible security controls: You can create grouping mechanisms to ensure certain accounts meet compliance requirements, such as HIPAA or PCI DSS.
- Easily adapt to business processes: The use of multiple accounts allows you to set up your IT infrastructure in a way that reflects the needs of your business processes or requirements.

Ultimately, a multi-account AWS environment enables you to use the cloud to move faster and build differentiated products and services, while providing mechanisms to do so in a secure, scalable, and resilient manner. But how should you build your multi-account AWS environment? You may have questions, such as what account structure to use, what policies and guardrails to implement, or how to set up your environment for auditing.

In this post, we walk you through the elements of building a secure and productive multi-account AWS environment, often referred to as a “landing zone,” as recommended by AWS. This represents the best practices that can be used to build an initial framework, while still allowing for flexibility as your AWS workloads increase over time.

## Best practices for setting up your multi-account AWS environment

Before getting started, let’s get familiar with a few terms. An organizational unit (OU) is a logical grouping of accounts in your organization, created using AWS Organizations. OUs enable you to organize your accounts into a hierarchy and make it easier for you to apply management controls. AWS Organizations policies are what you use to apply such controls. A Service Control Policy (SCP) is a policy that defines the AWS service actions, such as Amazon EC2 **run instance**, that accounts in your organization can perform.

When building this structure, a key principle is to reduce the operational overhead of managing the structure. To achieve this, we minimized the depth of the overall hierarchy and where policies are applied. For example, Service Control Policies (SCPs) are primarily applied at the OU level, to ease troubleshooting, instead of at the account level. Any exceptions to this approach are noted below.

First, consider what account groupings or OUs you should create. OUs allow you to organize accounts based on function, apply common policies, and organize your AWS accounts so that it’s easier to share centrally managed resources across similar AWS accounts. Your OUs should be based on function or a common set of controls, rather than mirroring your company’s reporting structure.

### Prod and Software Development Life Cycle (SDLC)

Before we dive into the foundational OU, let’s consider how the software development lifecycle can be achieved. Given that most companies have different policy requirements for production workloads, some OUs can have nested OUs for non-production (SDLC) and production (prod). Accounts in the SDLC OU host non-production, that is, dev, test, and pre-prod. They should not have production dependencies from other accounts. Accounts in the Prod OU, as the name suggests, hosts the production workloads. For applications and services not developed by the customer, the SDLC accounts can model the staging environment. For example, an off-the-shelf product can be hosted in the dev environment, under the SDLC OU, and a prod account under the “prod” OU, in the Workloads OU.

While it’s likely that customers can create a single SDLC OU to host all the stages of development in accounts, if there are variations in OU policies between the lifecycles, the SDLC OU can replace multiple OUs such as the Dev OU and PreProd OU. Regardless, a separate Prod OU should generally exist to host production workloads.

Apply policies at the OU level, to govern the Prod and SDLC environments, per your requirements. In general, applying policies at the OU level rather than the individual account level is recommended, as it simplifies policy management and any potential troubleshooting.

### Foundational OUs

AWS recommends that you start with security and infrastructure in mind. Most businesses have centralized teams that serve the entire organization for those needs. As such, we recommend creating a set of foundational OUs for these specific functions, split into Infrastructure and Security OUs.

![Security and Infrastructure Organizational Units](https://d2908q01vomqb2.cloudfront.net/972a67c48192728a34979d9a35164c1295401b71/2020/07/08/Foundational_OU_1-285x300.png)

### OU: Infrastructure

Infrastructure: Used for shared infrastructure services, such as networking and IT services. Create accounts for each type of infrastructure service you require.

Example: A Customer has three shared infrastructure and networking services, providing access to the corporate networks, a hosted messaging service using RabbitMQ (message bus service), and a general shared infrastructure account. The OU and accounts structure would look like this:

![](https://d2908q01vomqb2.cloudfront.net/972a67c48192728a34979d9a35164c1295401b71/2020/07/29/infrastructure_OU.png)

### OU: Security

The security OU is used for hosting security-related access and services. The Security OU, its child OUs, and the associated AWS accounts, should be owned and managed by your Security organization.

### Recommended accounts

**Log Archive**: An AWS account that acts as a consolidation point for security-oriented AWS access and audit logs gathered from all of the AWS accounts in your environment.

**Security ReadOnlyAccess** (humans): The purpose of this AWS account is to enable your security team members to access other AWS accounts in your AWS environment with read-only permissions in support of auditing, exploratory security testing, and investigations. For example, in the early stages of investigating a suspected security incident, your security team members would first access this AWS account and use a read-only IAM cross-account role, then access other AWS accounts to review and monitor the state of resources.

**Security Breakglass** (humans): An AWS account that would rarely be used, but available to members of your security team during security incidents. This account would enable extensive write access to your AWS accounts. At the outset of an incident, special authorization would be required for a security team member to gain access. Once an incident has been resolved, the temporary access would be revoked. All access would be logged in detail.

**Security Tooling** (minimal humans): One or more AWS accounts to host broadly applicable security-oriented workloads and services, tools, and supporting data. Common examples of tools and services configured in this account include an [Amazon GuardDuty](https://aws.amazon.com/guardduty/) master account, [AWS Security Hub](https://aws.amazon.com/security-hub) master account, [Amazon Detective](https://aws.amazon.com/detective/) master account, and third party cloud security monitoring services and tools. Human access to these AWS accounts for administration purposes should be minimized, in favor of using Infrastructure as Code (IaC) and other automated techniques. Where there’s a need for direct human administration, authorized administrators require sufficient write access. Beyond administrative access, additional human access will likely be needed, so that security team members can interact with and potentially configure features of the security services.

###### ![Security OU with SDLC and Production nested OUs.](https://d2908q01vomqb2.cloudfront.net/972a67c48192728a34979d9a35164c1295401b71/2020/07/21/Security.png)

Once the central services are in place, we recommend creating OUs that directly relate to building or running your products or services. Many AWS customers build the OUs listed below after establishing the foundation.

### OU: Sandbox

This OU is for AWS accounts of individual technologists, in which they can learn and dive deep into AWS services. It is recommended that accounts within this Sandbox are detached from the customer’s internal networks. Access to the internet is required to access AWS services, but it is recommended that this be limited. Also consider a fixed spending limit for these accounts, for example $100 per month, which is reported to leadership, to track outliers and excessive usage.

Example, a customer provides Sandbox accounts for all its employees:

###### ![Sandbox OU with individual developer accounts](https://d2908q01vomqb2.cloudfront.net/972a67c48192728a34979d9a35164c1295401b71/2020/07/14/Sandbox.png)

### OU: Workloads

These are the OUs where the AWS accounts for the software lifecycle are created. It is recommended that workload accounts are created to isolate software services, rather than mapping to the customer’s teams, to make the deployed application more resilient to organizational change. Transferring access to a set of accounts from one team to another is easy, while moving software services from one account to another is a much larger task.

Accounts in the SDLC/non-prod OUs are intended for staging software services, and should have no dependency on other OUs.

Accounts in other additional OUs should depend only on the workloads/prod OU accounts.

Example: A customer has three different business units, Manufacturing, Consumer Services and Marketing, all of which share governance and operational models. Consumer Services has a public beta, which the OUs do not have. In this case it is recommended to have the following structure:

###### ![Workloads OU, with SDLC and Prod nested OUs](https://d2908q01vomqb2.cloudfront.net/972a67c48192728a34979d9a35164c1295401b71/2020/07/14/Workloads.png)

At this point in the process, the foundational and business-oriented OUs have been established, and you can start your cloud journey. This is the starting framework:

![Security, Infrastructure, Sandbox, and Workload OU's.](https://d2908q01vomqb2.cloudfront.net/972a67c48192728a34979d9a35164c1295401b71/2020/07/17/Foundational_Sandbox_WorkloadOU_500px.jpg)

We recommend adding additional business-oriented OUs for maintenance and continued expansion, depending on your specific needs. These are some common themes based on practices from existing AWS customers:

### OU: PolicyStaging

When making policy or structural changes to an AWS Organization it is important to verify your changes before applying them broadly. To verify changes, an administrator needs the ability to build and apply changes they want to make, in a non production-impacting way. The organizational unit “OU:PolicyStaging” is a non-production OU, which gives an organization administrator a place to test a proposed OU setup, to verify results of applying a policy.

It’s recommended that child OUs and accounts be created to test the changes. Once the changes are understood and verified, a rollout strategy can be employed to slowly apply changes to the broader organization. It’s recommended to start rollout at the minimum possible level, on an account in the intended location. Promote changes in your OU structure as you gain confidence. Making changes in this way will minimize your possible blast radius.

Example: The Policy team is managing the policies for security, infrastructure, workloads, code, and deployment. To stage these they have the following structure:

###### ![PolicyStaging OU with Security, Infrastructure, Workloads, and Deployment OUs](https://d2908q01vomqb2.cloudfront.net/972a67c48192728a34979d9a35164c1295401b71/2020/07/14/PolicyStaging.png)

### OU: Suspended

Contains AWS accounts that have been closed and are waiting to be deleted from the organization. Attach a [Service Control Policy](https://docs.aws.amazon.com/organizations/latest/userguide/orgs_manage_policies_type-auth.html) (SCP) to this OU that denies all actions. Ensure that the accounts are [tagged](https://docs.aws.amazon.com/organizations/latest/userguide/orgs_tagging.html) with details for traceability, if they need to be restored.

Former employee-owned accounts and accounts being retired should be moved to “suspended.” Accounts should be tagged with details, such as where they came from, in case there is a need to restore and for traceability reasons.

Accounts that are closed for 90 days are subject to permanent deletion, after which the account and its resources can’t be recovered. Closed accounts are visible in your organization, with the “suspended” state. After an account is permanently deleted, it’s no longer visible in your organization.

For additional details on closing accounts, visit the [closing an AWS account documentation](https://docs.aws.amazon.com/organizations/latest/userguide/orgs_manage_accounts_close.html).

### OU: IndividualBusinessUsers

A limited access OU that contains AWS accounts for business users who are not technologists. These users may create business productivity-related applications, for example, set up an S3 bucket to share reports or share files with a partner.

### OU: Exceptions

There are instances where a business use case warrants an exception from security or auditing conditions defined under OU:Workloads. When one of these cases is identified, an exception may be granted. In those cases, the accounts will be given a customized security stance. Accounts under the OU:Exceptions have SCPs applied directly to the account instead of the OU, due to the custom nature of their use cases. Owners of these accounts can also expect to have higher scrutiny from detect and react systems in place ([Amazon CloudWatch](http://aws.amazon.com/cloudwatch) Events, [AWS Config](https://aws.amazon.com/config/) Rules, etc.), due to the customized preventative controls.

For example, top-secret projects are a special case which may fall under the Exceptions OU. Ultimately, this depends on what SCPs are defined for compliance and security, and if new products can launch within the guidelines defined by associated SCPs. If the security desired around the new initiative is so tight that people feel it warrants a new separate organization, there is added risk and cost in migrating back into the main organization in the future.

### OU: Transitional

The Transitional OU is intended as a temporary holding area for existing accounts and workloads that you move to your organization before you formally integrate them into your more standardized areas of your AWS environment structure. You may need to move accounts due to an company acquisition, or taking over the accounts previously serviced by a third party. This OU gives you a temporary place to assign accounts that may not fit into your OU structure.

### OU: Deployments

Contains AWS accounts meant for CI/CD deployments. You can create this OU if you have a different governance and operational model for CI/CD deployments, as compared to accounts in the Workloads OUs (Prod and SDLC). Distribution of CI/CD helps reduce the organizational dependency on a shared CI/CD environment operated by a central team. For each set of SDLC/Prod AWS accounts for an application in the Workloads OU, create an account for CI/CD under Deployments OU.

The CI/CD Deployment pipelines could be either AWS CodeX services or self-hosted services. It is recommended to distribute CI/CD in a way that matches the operational model of the software service it builds and deploys.

Accounts in the non-production OU are intended for staging the CI/CD service, and should have no dependencies from other OUs.

Example: A customer has three different business units. Manufacturing, which has industrial IoT services, and is self-governing with its own operational model; Consumer Services; and Marketing, which share governance and operational models. In this case, it is recommended to have the following OUs and accounts:

![Deployments OU with an SLDC and Prod nested OUs](https://d2908q01vomqb2.cloudfront.net/972a67c48192728a34979d9a35164c1295401b71/2020/07/15/Deployments_1-1.png)

It’s recommended that CI/CD Deployment OU is separated into a different hierarchy and AWS accounts, as the governance and operational models differ between the two.

For each service being built out, accounts matching the development lifecycle are created under the Teams OU. The production stage would be under OU:Workloads/OU:Prod. All other stages of the development lifecycle would be under the OU:Workloads/OU:SDLC.

For each service (that is, set of SDLC accounts), there would be a corresponding account for deployment. This account would sit under OU:Deployments. For example, if a service called foo has dev, beta, QA, production, its overall environment would be configured as follows:

![Beta, QA and Dev accounts under Workloads OU, Production account under Deployments OU](https://d2908q01vomqb2.cloudfront.net/972a67c48192728a34979d9a35164c1295401b71/2020/07/17/Deployments_2.png)

Now we’ve established our additional OUs and accounts.

![Additional OU's: Sandbox, Workloads, Policy Staging, Suspended, Individual Business Users, Exceptions, and Deployments](https://d1.awsstatic.com/product-marketing/organizations/Product-Page-Diagram_Organizational.66fa1fae2c9602db87a766680b9682c11772ee01.png)

## Conclusion

A well-architected multi-account strategy helps you innovate faster in AWS, while helping you meet your security and scalability needs. The framework described in this blog post represents AWS best practices that you should use as a starting point for your AWS journey.

![Full view of recommended Organizational Unit structure](https://d1.awsstatic.com/product-marketing/organizations/Product-Page-Diagram_Organizational-Foundational-Units.d709f66bf4c45ed1af01360f3d39adecc1a99fb4.png)

To get started with building your own environment, refer to the [AWS Organizations Getting Started Guide](https://aws.amazon.com/organizations/getting-started/). Alternatively, you can use [AWS Control Tower](https://aws.amazon.com/controltower/) to help you quickly set up a secure initial AWS environment in a few clicks.

### About the Author

![](https://d2908q01vomqb2.cloudfront.net/22d200f8670dbdb3e253a90eee5098477c95c23d/2018/11/15/Sam-Elmalak-bio.jpg)

Sam Elmalak is a WW Tech Leader at AWS and a member of the AWS security community. In addition to helping customers solve their technical issues, he helps customers navigate organizational complexity and address cultural challenges. Sam is passionate about enabling teams to apply technology to address business challenges and unmet needs. He’s largely an optimist and a believer in people’s abilities to thrive and achieve amazing things.