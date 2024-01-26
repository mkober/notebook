Clipped from: [https://tutorialsdojo.com/aws-wavelength/](https://tutorialsdojo.com/aws-wavelength/)



- A service that allows developers to create applications with ultra-low latencies for mobile devices and end users.
- Wavelength Zones can be used to extend an [Amazon VPC](https://tutorialsdojo.com/amazon-vpc/) in order to run ultra-low latency applications that use the same AWS services, APIs, tools, and functionalities.

## Features

- Wavelength Zones support a wide range of compute instances for general purpose, gaming, and machine learning inference.
- Supports persistent block storage to provide a snapshot, encryption, and restore capabilities without any performance impact.
- Connectivity to 5G networks using VPC and Carrier Gateway.
- Various AWS management and monitoring tools to run and manage workloads in Wavelength Zones.
- Use cases:

- Create and distribute augmented/virtual reality (AR/VR) apps, as well as HD live video streaming.
- Use AI and ML-powered video and image analytics at the edge to accelerate 5G applications in medical diagnostics, retail, and smart manufacturing settings.
- With near-real-time communication between automobiles and the cloud, you’ll be able to create advanced driver assistance, autonomous driving, and in-vehicle entertainment experiences.

## AWS Wavelength Concepts

- Wavelength is the AWS infrastructure used to run workloads that require ultra-low latencies over mobile networks.
- Wavelength Zone (WZ) 

- A logical extension of the Region. It is where the Wavelength infrastructure is deployed and is managed by the Region’s control plane.
- Use WZs for application components that require ultra-low latency, enhanced bandwidth, or improved service quality across 5G mobile networks.
- To give the most scalable, robust, and cost-effective alternatives for components, AWS recommends that you design the edge applications in a hub and spoke model with the Region.
- For latency-sensitive applications, you need to have multiple WZs.
- To discover the closest WZ endpoint, you must register the EC2 instance with a discovery service such as AWS Cloud Map.
- For data and app replication, AWS recommends you use an AZ in a different Region as a failover zone.
- Apps running on 4G/LTE mobile phones and devices connected to 4G/LTE networks can also connect to Wavelength Zones’ application servers.

- An application that you run on an AWS resource in a WZ is called Wavelength Application.
- Carrier Gateway

- Provides connectivity between WZ and telecommunication carrier.
- Enables inbound traffic from a carrier network in a specific location, as well as outbound traffic to the carrier network and the internet. 
- Supports IPv4 traffic.
- Only available for VPCs with WZ subnets.
- To assign a network interface, use a carrier IP address from the network border group.

- You can create AWS compute, storage services, and carrier gateways in WZs.
- You’ll also need VPC, Subnet, and Network Border Group to be able to leverage the 5G edge computing infrastructure of AWS Wavelength.
- To manage your resources and WZs, you can use the following interfaces:

- AWS Management Console
- AWS CLI
- AWS SDKs

## AWS Wavelength Pricing

- Prices for AWS resources in WZs will differ from those in the parent region.
- In WZs, EC2 instances are only available on demand.
- Wavelength Zones can be used with your Instance Savings Plan.

## Amazon Wavelength Cheat Sheet References:

[https://aws.amazon.com/wavelength/](https://aws.amazon.com/wavelength/) [https://docs.aws.amazon.com/wavelength/latest/developerguide/what-is-wavelength.html](https://docs.aws.amazon.com/wavelength/latest/developerguide/what-is-wavelength.html)