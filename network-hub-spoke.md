# Hub-spoke network topology
- The hub is a virtual network in Azure that acts as a central point of connectivity to your on-premises network. The spokes are virtual networks that peer with the hub.
- Traffic flows between the on-premises datacenter and the hub through an ExpressRoute or VPN gateway connection. 
- For several spokes that need to connect with each other, you will run out of possible peering connections very quickly due to the limitation on number of virtual network peerings per virtual network.In this scenario, consider using user defined routes (UDRs) to force traffic destined to a spoke to be sent to Azure Firewall or an NVA acting as a router at the hub. This will allow the spokes to connect to each other.
- ![image](https://user-images.githubusercontent.com/28542935/89816926-5bd98680-db15-11ea-81b8-94971902762c.png)
- Benefits
  - Cost savings by centralizing services that can be shared by multiple workloads, such as network virtual appliances (NVAs) and DNS servers, in a single location.
  - Overcome subscriptions limits by peering virtual networks from different subscriptions to the central hub.
  - Separation of concerns between central IT (SecOps, InfraOps) and workloads (DevOps).


# Azure Virtual WAN
- brings many networking, security, and routing functionalities together to provide a single operational interface
  - ranch connectivity (via connectivity automation from Virtual WAN Partner devices such as SD-WAN or VPN CPE)
  - Site-to-site VPN connectivity
  - remote user VPN (Point-to-site) connectivity
  - private (ExpressRoute) connectivity
  - intra-cloud connectivity (transitive connectivity for virtual networks)
  - VPN ExpressRoute inter-connectivity
  - Routing
  - Azure Firewall
  - encryption for private connectivity
- Azure regions serve as hubs that you can choose to connect to. All hubs are connected in full mesh in a Standard Virtual WAN making it easy for the user to use the Microsoft backbone for any-to-any (any spoke) connectivity.
- SKU
  - Basic: S2S VPN only
  - Standard: S2S, P2S, ExpressRoute, Inter-hub and VNet-to-VNet transiting through virtual hub
- ![image](https://user-images.githubusercontent.com/28542935/89816932-5da34a00-db15-11ea-972a-417bab1f45a5.png)


