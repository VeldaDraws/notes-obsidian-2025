A highly available system is one that can withstand some measure of degradation while remaining available.
- Enables resiliency in a reactive architecture. A resilient workload can recover when it's stressed by load, attacks, or component failure.
- Has minimized downtime with minimal human intervention.
- Recovers from failure or roll over to a secondary source in an acceptable amount of degraded performance time.
## Elastic Load Balancing (ELB)
![[D319-AWS-Solutions-Arc/2_Images/1_OtherImages/icon_ELB.jpg|50]]
A managed load balancing service that distributes incoming application traffic across multiple EC2 instances, containers, IP addresses, and Lambda functions.
- Can be external-facing or internal-facing.
- Each load balancer receives a DNS name.
- Recognizes and responds to unhealthy instances.
Elastic Load Balancing offers 3 types of load balancers:
- Application Load Balancer:
	- OSI model Layer 7.
	- Advanced load balancing of HTTP and HTTPS traffic.
	- Flexible application management.
- Network Load Balancer:
	- OSI model Layer 4.
	- Ultra-high performance and static IP address for your application.
	- Load balancing of TCP, UDP, and TLS traffic.
- Classic Load Balancer:
	- Previous generation.
		- HTTP, HTTPS, TCP, SSL.
	- Operates at both the request level and connection level.
	- Load Balancing across multiple EC2 instances.
See also: [ELB Features Page on AWS](https://aws.amazon.com/elasticloadbalancing/features/)
### Building a highly available application
It's best practice to launch resources in multiple Availability Zones and use a load balancer to distribute traffic among those resources. Running your applications across multiple Availability Zones provides greater availability if there's a failure in a data center.
![[elb_diagram-example.jpg]]
In the basic pattern here, two web servers run on EC2 instances that are in different Availability Zones. The instances are positioned behind an Elastic Load Balancing load balancer that distributes traffic between them.
Most applications can be designed to support two Availability Zones per AWS Region. If you use data sources that only support primary or secondary failover, then your application might not benefit from the use of more Availability Zones.

## Amazon Route 53
![[icon_route53.jpg|50]]
Amazon Route 53 is a highly available and scalable cloud DNS service.
- Translates domain name into IP addresses
- Connects user requests to infrastructure that runs inside and outside of AWS.
- Can be configured to route traffic to healthy endpoints, or to monitor the health of your application and its endpoints.
- Offers registration for domain names.
- Has multiple routing options.
Route 53 effectively connects user requests to infrastructure that runs in AWS: such as EC2 instances, ELB load balancers, or S3 buckets.
Amazon Route 53 supports several types of routing policies, which determine how Amazon Route 53 responds to queries:
- Simple Routing (Round Robin): Distributes the number of requests as evenly as possible between all participating servers.
- Weighted Round Robin Routing: Enables you to assign weights to resource record sets to specify the frequency that different responses are served at.
- LBR: Latency-Based Routing: Use when you have resources in multiple AWS Regions and you want to route traffic to the Region that provides the best latency. Latency routing works by routing your customers to the AWS endpoint that provides the fastest experience based on actual performance measurements of the different AWS Regions where your application runs.
- Geolocation Routing: Enables you to choose the resources that serve your traffic based on the geographic location of your users (origin of DNS queries).
- Geo-proximity Routing: Enables you to route traffic based on the physical distance between your users and your resources, if you are using Route 53 Traffic Flow.
- Failover routing (DNS failover): Use when you want to configure active-passive failover.
- Multi-value answer routing: Use if you want to route traffic approximately randomly to multiple resources, such as web servers.
With DNS failover routing, Route 53 can help detect an outage of your website and redirect your users to alternate locations where your application is operating properly. When you enable this feature, Route 52 health-checking agents monitor each location or endpoint of your application to determine its availability.