![[VPC-region.jpg|450]]
# Introduction To VPCs
A VPC (Virtual Private Cloud) is a logically isolated virtual network
- AWS VPC is tightly coupled with AWS EC2, and most VPC cli commands are under `aws ec2`
ENI (Elastic Network Interfaces) is used within a VPC to attach to different compute types.
#### Creating a VPC
When you create an Amazon VPC, you must choose three main factors:
- Name of the VPC
- Region where the VPC will live; A VPC spans all the availability zones within the selected Region
- IP range for the VPC in CIDR notation. Each VPC can have up to 5 CIDRs.
#### Creating a subnet
After you create your VPC, you must create subnets inside the network. In AWS, subnets are used to provide high availability and connectivity options for your resources.
###### Creating a public subnet:
- Create an IGW
- Create a Route table.
- Add a route to the route table that directs 0.0.0.0/0 traffic to the IGW.
- Associate the route table with a subnet, which thus becomes a public subnet.
#### Reserved IPs
See also: [[06-01_IP-Notation-Refresh]]
Example of reserved IPs in an IP range of 10.0.0.0/22. The VPC includes 1024 total addresses, then divided into 4 equal-sized subnets, each having 256 total addresses and 251 available addresses.
- 10.0.0.0 - Network Address
- 10.0.0.1 - VPC local router
- 10.0.0.2 - DNS server
- 10.0.0.3 - Future use
- 10.0.3.255 - Network broadcast address
![[VPC-with-subnets.jpg|450]]
# Core Components of VPC
![[vpc-01.jpg]]
### Key Features of VPC
- VPCs are Region-specific. **They do not span Regions**.
- You can use VPC Peering to connect VPCs across-regions.
- Every region comes with a default VPC.
- You can have **200 subnets per VPC**.
- Default **5 VPC per region**, per account.
- Up to 5 IPv4 CIDR Blocks
- Up to 5 IPv6 CIDR Blocks
- Most Components Cost nothing:
	- VPCs, route tables, NACLs, Internet Gateways, Security Groups and Subnets, VPC Peering.
- Some things do cost money
	- VPC Endpoints, Gateway, Elastic IPs
- DNS hostnames option.
![[vpc-02.jpg]]
![[vpc-03.jpg]]
## Route Tables
- Determines where to route traffic within a VPC.
- 📝You cannot delete the main route table.
	- You cannot set a gateway route table as the main route table.
	- You can replace the main route table with a custom subnet route table.
	- You can add, remove, and modify route in the main route table.
	- You can explicitly associate a subset with the main route table, even if it's already implicitly associated.
- Each subnet in your VPC must be associated with a route table.
- A subnet can only be associated with one route table at a time, but you can associate multiple subnets with the same route table.
Custom Route Tables
- The main route table is used implicitly by subnets that do not have an explicit route table association. If you associate a subnet with a custom route table, the subnet will use it instead of the main route table. Each custom route table that you create will have the local router already inside it, allowing communication to flow between all resources and subnets inside the VPC.
Further Reading: [VPC Route Tables](https://docs.aws.amazon.com/vpc/latest/userguide/VPC_Route_Tables.html)
![[route-table.jpg]]
### NACLs (Network Access Control Lists)
- Acts as a ***stateless*** (any allowed inbound traffic is also allowed outbound) virtual firewall for compute within a VPC.
- All VPCs automatically get a default NACL
	- Deny all by default
- Subnets are associated with NACLs.
	- Subnets can only belong to a single NACL
- Each NACL contains a set of rules that can allow or deny traffic into (inbound) and out of (outbound) subnets.
- Rule number order determines the order of evaluation.
	- Recommended to have 10 or 100 increments
	- Highest rule can be 32766
- You can block a single IP address (which isn't possible with Security Groups)
- Use case: Malicious actor has a specific IP address, then block.
### Security Groups (SG)
- Acts as a ***stateful*** virtual firewall for compute within a VPC. Operates at the instance level with allow rules.
- All inbound traffic is blocked by default unless a rule specifically allows it.
- All outbound traffic from the instance is allowed by default.
- Provide security at the instance (EC2), protocol, and port access level.
- Multiple Instances across multiple subnets can belong to a Security Group.
	- ![[sg-subnets.jpg]]
Limits:
- Up to 10,000 SGs in a Region (default: 2,500)
- 60 inbound rules and 60 outbound rules per security group
- 16 SGs per ENI. Default is 5.
Use Case:
![[sg-usecase.jpg]]
### VPC Peering
See also:
- [[07_Network-Connections#VPC Peering]]
### VPC Endpoints
See also:
- [[07_Network-Connections#VPC Endpoints]]
#### Interface Endpoint
- See also [[07_Network-Connections#VPC Endpoints]]
#### Internet Gateway (IGW)
- A gateway that connects your VPC out to the internet
- Virtually a modem, in a sense. Unlike your modem at home, an IGW is highly available and scalable.
![[igw-overview.jpg]]
###### NAT Gateway
- Allows private instances to connect to services outside the VPC.
- have to run within a public subnet
![[nat.jpg]]
##### Virtual Private Gateway
- A gateway that connects your VPC to a private external network.
- Acts as anchor on the AWS side of the connection, on the other side of the connection, you will need to connect a customer gateway to the other private network. When you have both gateways, you can then establish a VPN.
- Related Notes: [[07_Network-Connections#AWS Site-to-Site VPN]]
### AWS Direct Connect
- To establish a secure physical connection between your on-premises data center and your Amazon VPC, you can use AWS Direct Connect. With AWS Direct Connect, your internal network is linked to an AWS Direct Connect location over a standard Ethernet fiber-optic cable.
See also:
- [[07_Network-Connections#AWS Direct Connect (DX)]]
- User Guide: [What is AWS Direct Connect?](https://docs.aws.amazon.com/directconnect/latest/UserGuide/Welcome.html)
## Default VPC
![[default-VPC.jpg]]
- AWS has a default VPC in every region so you can immediately deploy instances.
	- Further Reading: Docs: [Default VPCs](https://docs.aws.amazon.com/vpc/latest/userguide/default-vpc.html)
	- Amazon creates the following resources on your behalf:
		- VPC with a size /16 CIDR block
		- size /20 default subnet
		- default security group associated with your default VPC
		- default NACL and associates with your default VPC
		- Associate default DHCP options set for your AWS account with your default VPC
![[vpc-default-diagram-from-user-guide.jpg]]
# Bastion / Jumpbox
![[bastion.jpg]]
# Related Notes
##### AWS Direct Connect:
- [[07_Network-Connections#AWS Direct Connect (DX)]]
- User Guide: [What is AWS Direct Connect?](https://docs.aws.amazon.com/directconnect/latest/UserGuide/Welcome.html)
##### VPC Peering:
- [[07_Network-Connections#VPC Peering]]
- [VPC Peering Docs/Whitepaper](https://docs.aws.amazon.com/whitepapers/latest/aws-vpc-connectivity-options/vpc-peering.html)
##### VPC Endpoints:
- [[07_Network-Connections#VPC Endpoints]]
- User Guide: [AWS PrivateLink](https://docs.aws.amazon.com/vpc/latest/userguide/endpoint-services-overview.html)
- Docs: [AWS PrivateLink Concepts](https://docs.aws.amazon.com/vpc/latest/privatelink/concepts.html)
##### VPN
- [[07_Network-Connections#AWS Site-to-Site VPN]]