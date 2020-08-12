# Virtual Network Gateway
- To send encrypted traffic between 
  - VNet and on-premises over public internet
  - VNet and another VNet over MSFT backbone network
- VPN device
  - VNet: composed of 2+ hidden VMs deployed to a gateway subnet
  - On-prem: compatible gateway device
- 1 VNet can only have one gateway
- Use IPsec / IKE to encrypt the traffic
- Gateway Subnet
  - Gateway requires its own subnet, can't share with other device
  - Address space set to /27 to support S2S and ExpressRoute co-existence
  - Do not use NSG 
- Gateway Type
  - VPN Gateway
  - ExpressRoute Gateway
- VPN Types:
  - Policy-based VPN devices 
    - use the combinations of prefixes from both networks to define how traffic is encrypted/decrypted through IPsec tunnels. 
    - It is typically built on firewall devices that perform packet filtering. 
    - IPsec tunnel encryption and decryption are added to the packet filtering and processing engine.
  - Route-based VPN devices
    - use any-to-any (wildcard) traffic selectors, and let routing/forwarding tables direct traffic to different IPsec tunnels. 
    - It is typically built on router platforms where each IPsec tunnel is modeled as a network interface or VTI (virtual tunnel interface).
- SKUs
  - Bandwidth
  - Number of tunnels and connections
  - Free on inbound traffic
  - Gen 1 can't upgrade to Gen 2
- Active-active mode
- BGP ASN
- Forced tunneling
  - Traffic not destined for a known connected network is sent out via the Internet
  - Forced tunneling routes all traffic to a specific route by
    - User defined routes (UDR)
    - Boarder Gateway Protocol (BGP)
  - Only possible with route-based gateway


# VPN connection Topologies
## Point-to-site (P2S)
  - From a personal computer to an Azure VNet
  - Travel over Internet
  - End-to-end encrypted
  - VPN software installed on computer
## Site-to-site (S2S)
  - VNet-to-on-prem
    - Physical on-prem VPN device (https://docs.microsoft.com/en-us/azure/vpn-gateway/vpn-gateway-about-vpn-devices)
    - On-prem public IP Address
    - Availability: redundancy, active-to-active
  - VNet-to-VNet
    - can be in different regions or subscriptions (vs. VNet peering)
    - Can be in different deployment models (classic vs resource manager)
  - Multi-site
    - S2S with multiple on-premises sites
    - Must use route-based VPN type
## ExpressRoute
  - Layer 3 connection
  - Travel over private connection through a communication provider
    - Provider bridges the "last-mile" connectivity between on-prem network to Microsoft edge ("meet-me locations)
  - No encryption 
  - One virtual circuit
  - Fast and expensive
  - Premium supports Office/Dynamics
## ExpressRoute Direct
  - Layer 1 connection
  - Travel over private connection through Microsoft backbone
  - No encryption 
  - Multiple virtual circuits
  - Faster: 10 Gbps, 100 Gbps


# Route Filter
- When Microsoft peering is configured on your ExpressRoute circuit, the Microsoft edge routers establish a pair of BGP sessions with the edge routers (yours or your connectivity provider's). No routes are advertised to your network. To enable route advertisements to your network, you must associate a route filter.
- A route filter lets you identify services you want to consume through your ExpressRoute circuit's Microsoft peering. It is essentially a list of all the BGP community values you want to allow. Once a route filter resource is defined and attached to an ExpressRoute circuit, all prefixes that map to the BGP community values are advertised to your network.


