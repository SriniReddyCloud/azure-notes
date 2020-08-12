# Virtual Network
- enable Azure resources to securely communicate with each other, the internet, and on-premises networks
- scoped to a region and a subscription
- can be connected together from different regions through peering
- a container for subnets (data tier subset, web tier subset)
- Limits
  - 1000 VNet per subscription per region
  - 500 peerings per subscription per region
  - 1 VPN gateway per VNet
  - 1 ExpressRoute gateway per VNet
- Configurations
  - Address Space: private IP range
  - Subnet: 5 addresses reserved for each subnet
  - DDoS: basic - free, standard - recommended for internet-facing
  - Service endpoints: secured channel for communicating with some azure services
  - Azure Firewall
- Communication with Internet
  - can communicate outbound to the internet by default
  - Inbound communication from internet can be done via a public IP or public load balancer
- Communication with other VNet
  - VNet Peering - over backbone
  - VPN Gateway - over internet
- Communication with on-prem network
  - VPN Gateway
  - ExpressRoute
  - Hub-spoke network topology
  - Azure Virtual WAN
- Communication with Azure resources and services
  - Azure services deployed into VNet (VM, AG/WAF, Redis, AKS, APIM, https://docs.microsoft.com/en-us/azure/virtual-network/virtual-network-for-azure-services)
  - Service endpoint
  - Private Endpoint
  - Private Link
- Monitors
  - Azure Monitor
  - Azure Network Watcher
    - Troubleshoot and visualize networks (gateway, routing, latency)
    - Performance monitor
    - Service connectivity monitor
    - logs
    - Traffic analytics
  - Azure Network Insights (Preview)
- Charging Model
  ![image](https://user-images.githubusercontent.com/28542935/89816919-5845ff80-db15-11ea-910b-4ccef64b06cc.png)
	
	
## Filter Network Traffic
### Network virtual appliances (NVA) - Azure Firewall
  - Deployed to VNet
  - HA and full cloud scalability
  - User defined route (UDR)
  - Fully Qualified Domain Name (FQDN) whitelisting
    - limit outbound to specified domains
  - NAT services
  - Network traffic filtering rules:
    - FQDN tags
    - Outbound SNAT support
    - Inbound DNAT support
    - Azure Monitor Logging
### Azure DDOS Protection
  - Types
    - Basic: always-on traffic monitoring and real-time mitigation of common network-level attacks
    - Standard: dedicated traffic monitoring and machine learning algorithms
  - Attacks
    - Volumetric Attacks
    - Protocol Attacks
    - Resource Layer Attacks
### Network Security Group (NSG)
  - filter network traffic by allowing / denying inbound network traffic
  - Rules
    - Source
    - Source port
    - Destination
    - Destination port
    - Protocol
  - Source types
    - IP address
    - Application Security Group (ASG)
    - Service Tag
      - Internet
      - VNet
      - LB, APIM, AG, AAD, SQL, ……
  - Destination types
    - IP address
    - ASG
    - VNet
  - Assignment
    - Applied to VM NIC
    - Can be assigned to a subnet, then applied to all VM NICs under the subnet
### Application Security Group
  - group virtual machines 
  - configure network security as a natural extension of an application's structure
  - define network security policies and reuse them at scale without manual maintenance of explicit IP addresses
  - Limited to its region
  - Set as destination in security rules
	
	
## Route network traffic
### Route Table
  - A route table contains a set of rules, called routes, that specifies how packets should be routed in a virtual network. 
  - Route tables are associated to subnets, and each packet leaving a subnet is handled based on the associated route table. 
  - Each route table can be associated to multiple subnets, but a subnet can only be associated to a single route table.
  - Packets are matched to routes using the destination. This can be an IP address, a virtual network gateway, a virtual appliance, or the internet. 
  - If a matching route can't be found, then the packet is dropped. 
  - By default, every subnet in a virtual network is associated with a set of built-in routes. These allow traffic between virtual machines in a virtual network; virtual machines and an address space as defined by a local network gateway; and virtual machines and the internet.
  - There are no additional charges for creating route tables in Microsoft Azure.
### Border gateway protocol (BGP) routes
  - If you connect your virtual network to your on-premises network using an Azure VPN Gateway or ExpressRoute connection, you can propagate your on-premises BGP routes to your virtual networks


## Service Endpoint
- Enable subnets within a VNet to be identifiable to an Azure service
- Access to an instance of the Azure service can be locked down to the subnets
- Traffic via MSFT backbone
- Configuration
	- Enable service endpoints for specific Azure services for the subnet
	- Restrict the Azure service access from public internet to the subnet


## VNet Peering
- Enable resources under different virtual networks communicate with each other
- Not over Internet
- Global VNet Peering: between regions via Microsoft Backbone
- VNet Peering isn't transitive: A - B - C doesn't mean A - C
- Configurations
	- Access: One-way vs two-way
	- Forwarded traffic
	- Gateway transit: to use VPN gateway in peered VNet 
- Not limited by regions
- Expensive
	- Within region: $0.01 per GB both directions
	- Between regions: egress traffic charges
- Performant
- Limits: 500 peerings per VNet


## VNet-to-VNet Gateway
- ![image](https://user-images.githubusercontent.com/28542935/89816913-567c3c00-db15-11ea-8a16-f47a33d45d4e.png)
- Cheaper option than Vnet Peering: free inbound
- Traffic over Internet
- Require a VPN Gateway as a device for each VNet
- The gateway uses specific subnet called the gateway subnet in each Vnet
- No NSG should be associated with the gateway subnets
- Each gateway requires a public IP address (dynamic)
- Each gateway can create multiple connections
- Connection is transitive


## Azure Private Endpoint
- a network interface that connects you privately and securely to a service powered by Azure Private Link
- Private Endpoint uses a private IP address from your VNet, effectively bringing the service into your Vnet
- Private Endpoint can share same subnet with Service Endpoint
- Services (Storage account, Cosmos DB) and Private link service


## Azure Private Link
- Enables multi-tenant PaaS service to have an IP in VNet representing service instance
- The service communicates via IP Address from the Vnet
- Services that support Private Link
	- Azure SQL
	- Azure storage
	- Cosmos DB
	- Key Vault
	- App Service
	- ……




