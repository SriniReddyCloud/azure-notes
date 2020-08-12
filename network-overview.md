The name of a resource indicates what we seek, an address indicates where it is, and a route tells us how to get there”.  - John F. Shoch


# Networking Layers - Open Systems Interconnection (OSI)
1. Physical
2. Data link (MAC)
3. Network (IP)
4. Transport (TCP/UDP)
  - Transmission Control Protocol / Internet Protocol (TCP/IP)
    - Bigger packet
    - Connection needs to be set up first (3 handshakes)
    - In-order delivery
    - Congestion control
    - Error detection
    - I would tell you a funny TCP joke. Did you get it? Did you get it? Did you get it?
  - User Datagram Protocol (UDP) 
    - Smaller packet
    - No connection needed
    - More control over when data is sent
    - Primitive error detection
    - No in-order delivery
    - No congestion control
    - No compensation for lost packets (I would tell you a funny UDP joke but you may not get it)
5. Session
6. Presentation
7. Application (https)




# The Internet
- The Internet is a network of networks; it’s broken up into hundreds of thousands of smaller networks known as autonomous systems (AS)
- Autonomous System (AS)
  - An AS can be an Internet Service Providers, universities, government agencies, large corporate networks, including multiple locations (IP addresses). 
  - Each AS is represented by a unique number called an ASN
    - Internet Assigned Numbers Authority (IANA) assigns ASNs to Regional Internet Registries (RIRs), which then assigns them to ISPs and networks
    - About 64,000 ASNs in-use worldwide
  - Each AS controls a collection of connected routing prefixes, representing a range of IP addresses
- Boarder Gateway Protocol (BGP)
  - BGP is a routing protocol  to exchange routing and reachability information between AS
  - Each AS connects to neighboring AS’s with a TCP/IP connection for the purpose of sharing routing information.
  - BGP determines the best route based on a number of factors (speed, location, cost, business relations, …)
  - Route-sharing function of BGP relies on trust, and autonomous systems implicitly trust the routes that are shared with them.


- IP Address
- Public IP - Internal routable IP address range
  - Prefix
  - Assignments
    - virtual machines (not recommended)
    - load balancers
    - application gateway
    - VPN gateways
  - Associated with subscription and region 
  - Instance-level public IP (ILPIP): assigned to a virtual machine or role instance directly
  - Virtual IP address (VIP): assigned to a cloud service
  - Configurations:
    - SKU: must match SKU of the load balancer
    - IPv6: supported at load balancer level, which converts it to IPv4
    - Assignment:
      - Static: DNS for custom domain, firewall whitelisting, SSL cert
      - Dynamic
    - Idle timeout: keep connection open without keep-live request
    - DNS name label: free for azure default
  - PaaS services
    - Azure App Service
      - a public dynamic IP and DNS by default
      - Outbound IPs can be queried
      - Custom DNS and SSL can be added
      - ASE can have static IP
    - Azure SQL
      - A public dynamic IP and DNS by default
- Private IP


# Virtual Appliance
- Essentially a VM with pre-configured software and configuration
- Examples
  - Firewall
  - Load balancer


# DMZ
- Internet-facing segment of company intranet
- Firewall between DMZ and intranet
- ![image](https://user-images.githubusercontent.com/28542935/89816908-5419e200-db15-11ea-9a05-b2f2b89d81e7.png)


