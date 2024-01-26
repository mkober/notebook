In this scenario, you have two VPCs that have peering connections with each other. Note that a VPC peering connection does not support edge-to-edge routing. This means that if either VPC in a peering relationship has one of the following connections, you cannot extend the peering relationship to that connection:

– A VPN connection or an AWS Direct Connect connection to a corporate network

– An Internet connection through an Internet gateway

– An Internet connection in a private subnet through a NAT device

– A gateway VPC endpoint to an AWS service; for example, an endpoint to Amazon S3.

– (IPv6) A ClassicLink connection. You can enable IPv4 communication between a linked EC2-Classic instance and instances in a VPC on the other side of a VPC peering connection. However, IPv6 is not supported in EC2-Classic, so you cannot extend this connection for IPv6 communication.

![](https://media.tutorialsdojo.com/edge-to-edge-vpn-diagram.png)

For example, if VPC A and VPC B are peered, and VPC A has any of these connections, then instances in VPC B cannot use the connection to access resources on the other side of the connection. Similarly, resources on the other side of a connection cannot use the connection to access VPC B.

Hence, this implies that VPC-2 cannot extend the peering relationship between VPC-1 and the on-premises network. In other words, traffic originating from the corporate network cannot establish a direct connection to VPC-1 by routing it through VPC-2, whether using a VPN connection or an AWS Direct Connect connection. The VPC peering connection is a one-to-one relationship with directly peered entities (VPC-1 and the on-premises network), and it does not support transitive communication through intermediate VPCs like VPC-2, which is why the following options are incorrect: