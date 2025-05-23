# VPC Peering
[VPC Peering Docs/Whitepaper](https://docs.aws.amazon.com/whitepapers/latest/aws-vpc-connectivity-options/vpc-peering.html)
![[complex-vpc-peering-example.jpg]]
Isolating your workloads in VPCs is generally a good practice, but it can highly desirable to have connectivity between your VPCs for situations when you need to transfer data between them.
You can create a VPC peering connection between your own VPCs, with a VPC in another AWS account, or with a VPC in a different AWS Region. Inter-Region VPC peering provides a simple and cost-effective way to share resources between Regions or replicate data for geographic redundancy. Data that is transferred across inter-Region VPC peering connections is charged at the standard inter-Region data transfer rates.
Traffic remains in the private IP address space. All inter-Region traffic is encrypted with no single point of failure or bandwidth bottleneck.
#### VPC Peering Features:
- One-to-one networking connection between two VPCs
- No gateways, VPN connections, and separate network appliances needed.
- Highly available connections
- No single point of failure or bandwidth bottleneck
- Traffic always stays on the global AWS backbone.
#### Establishing VPC peering
- To establish a VPC peering connection, the owner of the requester VPC (local VPC) sends a request to the owner of the VPC peer.
- To enable traffic, you must add a route to one or more of your VPC's route tables. This route must point to the IP address range of the VPC peer.
- You might also need to update the security group rules that are associated with your instance so that traffic to and from the peer VPC is not restricted.
#### VPC peering connection restrictions
- Use private IP addresses
- Can be established between different AWS accounts.
- *Cannot have overlapping CIDR blocks*.
- Can have only one peering resource between any two VPCs.
- Do not support transitive peering relationships.
##### Considerations
- When you connect multiple VPCs, consider:
	- Only connecting essential VPCs
	- Make sure your solution can scale when needed
#### Summary
- Connecting VPCs to other VPCs
	- Using private IP addresses.
	- Instances on peered VPCs behave just like they are on the same network.
	- Connect VPCs across same or different AWS accounts and regions
	- Peering uses a Star Configuration: 1 Central VPC - 4 other VPCs
	- No transitive peering
		- needs a one-to-one connect to immediate VPC
	- No overlapping CIDR Blocks
![[vpc-peering.jpg]]
# AWS Site-to-Site VPN
![[icon-site2site.jpg\|50]] 
AWS Site-to-Site is a highly available solution that enables you to securely connect your on-premises network or branch office site to your VPC.
- Uses IPsec communications to create VPN tunnels.
- Provides two encrypted tunnels per VPN connection.
- Charged per VPN connection-hour.

AWS Site-to-Site VPN supports 2 types of routing:
- Static Routing
	- If your VPN device does not support BGP.
	- Supports 50 non-propagated routes per route table by default, up to a maximum of 1000 non-propagated routes.
- Dynamic Routing
	- If your VPN device supports BGP.
	- Supports maximum of 100 propagated routes per route table.

| Static Routing                                                                 | Dynamic Routing                                                        |
| ------------------------------------------------------------------------------ | ---------------------------------------------------------------------- |
| - Requires you to specify all routes (IP prefixes)                             | - Uses the BGP to advertise its routes to the virtual private gateway. |
| - Specify static routing if your customer gateway device does not support BGP. | - Specify dynamic routing if your customer gateway device supports BGP |
##### Limitations
- IPv6 traffic is not supported for VPN connections on a virtual private gateway.
- An AWS VPN connection does not support Path MTU Discovery.
#### Connecting Multiple VPNs using [AWS VPN CloudHub](https://docs.aws.amazon.com/vpn/latest/s2svpn/VPN_CloudHub.html)
![[multi-vpn.jpg|450]]
- Billed the connection rate for each hour that each VPN is connected to the virtual private gateway.
- Operates on hub-and-spoke model to enable multiple sites to access your VPC or to securely access each other. You can use it with or without a VPC.
- Further reading:
	- [AWS Site-to-Site VPN single and multi examples](https://docs.aws.amazon.com/vpn/latest/s2svpn/Examples.html)
##### Site-to-Site VPN Further Reading: 
- PDF: [AWS s2s VPN](https://docs.aws.amazon.com/pdfs/whitepapers/latest/aws-vpc-connectivity-options/aws-vpc-connectivity-options.pdf#aws-site-to-site-vpn)
# AWS Direct Connect (DX)
![[icon-direct_connect.jpg|50]]
AWS Direct Connect, (aka DX) provides you with a dedicated private network connection capacity of up to either 1 Gbps or 10 Gbps.
- Reduces data transfer costs
- Improves application performance with predictable metrics.
Use cases:
- Hybrid environments
- Transferring large datasets (HPC applications)
	- Network transfers will not compete for internet bandwidth at your data center.
	- Reduces network congestion and degraded performance.
	- Possible reduction in network fees to ISP.
- Network performance predictability
- Security and compliance.
	- Enterprise security or regulatory policies sometimes require that applications hosted on the AWS Cloud can be accessed through private network circuits only.
##### Further Reading:
- [AWS Direct Connect locations](https://aws.amazon.com/directconnect/locations/)
- [What is AWS Direct Connect](https://docs.aws.amazon.com/directconnect/latest/UserGuide/Welcome.html)
# AWS Transit Gateway
![[icon-transit-gateway.jpg|50]]
AWS Transit gateway is a service that enables you to connect your VPCs and on-premises networks to a single gateway.
- Fully-managed, highly available, flexible routing service
- Acts as a hub for all traffic to flow between your networks
- Up to 5,000 VPCs and on-premise environments with a single gateway.
- Uses hub-and-spoke model.
#### [Creating a Transit Gateway](https://docs.aws.amazon.com/vpc/latest/tgw/tgw-getting-started.html): Overview
1. Create the Transit Gateway.
2. Attach your VPCs to your Transit Gateway.
3. Add routes between the transit gateway and your VPCs.
4. Test the Transit Gateway.
5.  (Optional) Delete the Transit Gateway.
# VPC Endpoints
![[icon-vpc-endpoint.jpg|50]]
- Enables you to privately connect your VPC to supported AWS services and to VPC endpoint services that are powered by AWS PrivateLink
- Enable traffic between your VPC and the other service without leaving the Amazon network
- Does not require an IGW, VPN, NAT devices or firewall proxies.
- Horizontally scalable, redundant, and highly available.
See also: 
- User Guide: [AWS PrivateLink](https://docs.aws.amazon.com/vpc/latest/userguide/endpoint-services-overview.html)
#### Two types of VPC Endpoints
![[vpc-endpoints.jpg]]
- [Interface Endpoints](https://docs.aws.amazon.com/vpc/latest/privatelink/concepts.html)
	- An elastic network interface with a private IP address that serves as an entry point for traffic destined to a supported service.
	- Small cost of approximately $0.01 / hour or GB
		- Powered by [AWS PrivateLink](https://aws.amazon.com/privatelink/pricing/)
- Gateway Endpoints
	- Free.
	- A gateway that you specify as a target for a route in your route table for traffic destined to a supported AWS service.
- Privately connect to AWS support services - Traffic between your VPC and other services do not leave the AWS network.
- Horizontally scaled, redundant, and highly available VPC component.
#### Setting up an [Interface Endpoint](https://docs.aws.amazon.com/vpc/latest/privatelink/create-interface-endpoint.html#create-interface-endpoint)
1. Specify AWS Service, endpoint service or AWS Marketplace service you want to connect to.
2. Choose the VPC where you want to create the interface endpoint.
	- You may specify more than one subnet in different AZs.
3. Choose a subnet in your VPC that will use the interface endpoint. When you create an interface endpoint for a service in your VPC, an endpoint network interface is created in the selected subnet.
4. (Optional) [Enable private DNS for the endpoint](https://docs.aws.amazon.com/vpc/latest/privatelink/create-interface-endpoint.html#vpce-private-dns).
5. Specify the security groups to associate with the network interface.
![[privatelink.jpg]]
#### VPC Endpoint CheatSheet (freeCodeCamp)
![[vpc-endpoint-cheatsheet.jpg]]