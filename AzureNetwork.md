# :sunny: VDC vs Network
The key to unlock the advantages of VDC is a centralized hub and spoke network topology with a mix of Azure services and features:

- Azure Virtual Network,
- Network security groups,
- Virtual network peering,
- User-defined routes, 
- Azure Identity with role-based access control (RBAC) 
- optionally Azure Firewall, Azure DNS, Azure Front Door, and Azure Virtual WAN.

# When designing a VDC implementation, there are several pivotal issues to consider:
1.Identity and directory service :
  - key aspect of all datacenters
  - The goals of this process should be to increase security and productivity while decreasing cost, downtime, and repetitive manual tasks.
  - Notes : Azure Active Directory is a comprehensive, highly available identity and access management cloud solution that combines core directory services, advanced identity governance, and application access management
2. Security infrastructure
 - segregation of traffic in a VDC implementation's specific virtual network segment.
 - VNet isolation, access control lists (ACLs), load balancers, IP filters, and traffic flow policies.
 - (NAT) separates internal network traffic from external traffic.
 Notes : Azure Fabric  And  Azyre Hypervisor
3. Connectivity to the cloud
  -  Internet, but also to on-premises networks and datacenters.
  - Azure Firwall  OR  VNA 
  - User Defined routes
  - NSG
  -  Azure Site-to-Site VPN  && Azure Virtual WAN (Dashbords) && Express Route
  Notes : DDOS
  4. Connectivity within the cloud
    - VNET
    - VNET Peering (same Azure region or even across regions)

# Topology
## Hub and Spoke
- Hub and spoke is a model for designing the network topology for a virtual datacenter implementation.
- A hub is the central network zone that controls and inspects ingress or egress traffic between different zones: internet, on-premises, and the spokes
- reduces the potential for misconfiguration and exposure.
- The role of each spoke can be to host different types of workloads

## Subscription limits and multiple hubs
- https://docs.microsoft.com/en-us/azure/azure-subscription-service-limits
- The architecture can scale up further by extending the model from a single hub-spokes to a cluster of hub and spokes
- Multiple hubs in one or more Azure regions can be interconnected using VNet Peering, ExpressRoute, Virtual WAN, or site-to-site VPN.
- Peering : spokes can connect to other spokes in the same hub or different hubs ==> avoid transiting through the hub, Security !
Notes :  increases the cost and management effort of the system. 
Notes :  An architecture with two levels of hubs introduces complex routing that removes the benefits of a simple hub-spoke relationship.
Notes :  one of the core principles of the VDC concept is repeatability and simplicity

# Components
	##The virtual datacenter is made up of four basic component types: 
	-	Infrastructure,
	-	Perimeter Networks,
	- 	Workloads,
	- 	Monitoring.




