# Azure Load Balancing Options
![image](https://user-images.githubusercontent.com/28542935/89816943-609e3a80-db15-11ea-8c95-cb1e3fc83e4b.png)


# Azure Load Balancer
- Layer 4 (TCP/UDP) load balancing
- Scale applications and create high availability for services
  - low latency and high throughput
  - scale up to millions of flows for all TCP and UDP applications
  - Hash-based distribution between multiple targets
  - port forward traffic to a specific port
  - provide outbound connectivity
- External vs Internal
  - public/external load balancer maps public IP address and port number of incoming traffic to private IP address and port number of the VM, and vice versa for the response traffic from the VM
  - internal load balancer directs traffic only to resources inside a virtual network or that use VPM to access Azure infrastructure
- Configurations
  - Frontend IP
  - Backend pools
  - Health probes
  - Load balancing rules


# Azure Application Gateway
- Layer 7 load balancing
- Terminate client connection and forward requests to target
- Support HTTP, HTTPS, HTTP/2 and websockets protocols for web solutions
- Round cabin load balancing na dURL-based ontent routing
- Cookie-based session affinity
- Web Application Firewall (WAF)
- Configurations
  - Vnet: Application Gateway must be by itself in a virtual network subnet
  - Availability zone
  - Backend pools: 
    - IP address 
    - VM and VMSS 
    - Azure App Services
  - HTTP Settings
  - Frontend IP: Public IP must be standard SKU and static
  - Listener
  - Rule
![image](https://user-images.githubusercontent.com/28542935/89816955-63009480-db15-11ea-97bc-59db15f364cc.png)
- How an application gateway accepts a request
  - Before a client sends a request to an application gateway, it resolves the domain name of the application gateway by using a Domain Name System (DNS) server. Azure controls the DNS entry because all application gateways are in the azure.com domain.
  - The Azure DNS returns the IP address to the client, which is the frontend IP address of the application gateway.
  - The application gateway accepts incoming traffic on one or more listeners. A listener is a logical entity that checks for connection requests. It's configured with a frontend IP address, protocol, and port number for connections from clients to the application gateway.
  - If a web application firewall (WAF) is in use, the application gateway checks the request headers and the body, if present, against WAF rules. This action determines if the request is valid request or a security threat. If the request is valid, it's routed to the backend. If the request isn't valid and WAF is in Prevention mode, it's blocked as a security threat. If it's in Detection mode, the request is evaluated and logged, but still forwarded to the backend server.
  - Azure Application Gateway can be used as an internal application load balancer or as an internet-facing application load balancer. An internet-facing application gateway uses public IP addresses. The DNS name of an internet-facing application gateway is publicly resolvable to its public IP address. As a result, internet-facing application gateways can route client requests to the internet.
  - Internal application gateways use only private IP addresses. If you are using a Custom or Private DNS zone, the domain name should be internally resolvable to the private IP address of the Application Gateway. Therefore, internal load-balancers can only route requests from clients with access to a virtual network for the application gateway.

- How an application gateway routes a request
  - If a request is valid and not blocked by WAF, the application gateway evaluates the request routing rule that's associated with the listener. This action determines which backend pool to route the request to.
  - Based on the request routing rule, the application gateway determines whether to route all requests on the listener to a specific backend pool, route requests to different backend pools based on the URL path, or redirect requests to another port or external site.
  - When the application gateway selects the backend pool, it sends the request to one of the healthy backend servers in the pool (y.y.y.y). The health of the server is determined by a health probe. If the backend pool contains multiple servers, the application gateway uses a round-robin algorithm to route the requests between healthy servers. This load balances the requests on the servers.
  - After the application gateway determines the backend server, it opens a new TCP session with the backend server based on HTTP settings. HTTP settings specify the protocol, port, and other routing-related settings that are required to establish a new session with the backend server.
  - The port and protocol used in HTTP settings determine whether the traffic between the application gateway and backend servers is encrypted (thus accomplishing end-to-end TLS) or is unencrypted.
  - When an application gateway sends the original request to the backend server, it honors any custom configuration made in the HTTP settings related to overriding the hostname, path, and protocol. This action maintains cookie-based session affinity, connection draining, host-name selection from the backend, and so on.

- Azure virtual network and dedicated subnet
  - An application gateway is a dedicated deployment in your virtual network. Within your virtual network, a dedicated subnet is required for the application gateway. You can have multiple instances of a given application gateway deployment in a subnet. You can also deploy other application gateways in the subnet. But you can't deploy any other resource in the application gateway subnet.
  - Application Gateway uses one private IP address per instance, plus another private IP address if a private front-end IP is configured.
  - Azure also reserves five IP addresses in each subnet for internal use: the first four and the last IP addresses. For example, consider 15 application gateway instances with no private front-end IP. You need at least 20 IP addresses for this subnet: five for internal use and 15 for the application gateway instances. So, you need a /27 subnet size or larger.
  - Consider a subnet that has 27 application gateway instances and an IP address for a private front-end IP. In this case, you need 33 IP addresses: 27 for the application gateway instances, one for the private front end, and five for internal use. So, you need a /26 subnet size or larger.
  - We recommend that you use a subnet size of at least /28. This size gives you 11 usable IP addresses. If your application load requires more than 10 Application Gateway instances, consider a /27 or /26 subnet size.


# Azure Traffic Manager
- DNS-based traffic layer 4 load balancer
  - Traffic Manager uses DNS to direct client requests to the most appropriate service endpoint based on a traffic-routing method and the health of the endpoints. 
- Targets
  - VMs
  - PaaS Services
  - Other Traffic manager instances
  - On-prem
- Routing methods
  - Performance: location of user (DNS server)
  - Weighted: round-robin with weightings
  - Priority: primary and failover targets
  - Geographic: keep within a geo region (only 1 endpoint can be specified)
- Endpoint health monitoring
![image](https://user-images.githubusercontent.com/28542935/89816962-65fb8500-db15-11ea-94dd-9e8e2803a760.png)


# Azure Front Door
- Azure Front Door is a Global Application Delivery Network (ADN) as a service
- Layer 7 load balancing
- Vs Application Gateway: 
  - AG is regional service
  - Front Door can't load balance between VMs/containers
  - Commonly used together

