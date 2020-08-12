# Azure NAT Gateway
- NAT - Network address translation
- All outbound connectivity will be sourced from the static public IP addresses to the Internet

![image](https://user-images.githubusercontent.com/28542935/89816959-64ca5800-db15-11ea-80fc-2b2a662c3e70.png)



# Azure DNS
- DNS
  - A
    - The A record maps a name to one or more IP addresses when the IP are known and stable.
  - CNAME 
    - The CNAME record maps a name to another name. It should only be used when there are no other records on that name.
    - The DNS resolves the system’s domain name to its IP address, but sometimes more than one domain name resolves to the same IP address, and this is where the CNAME is useful.
- Public and private DNS zone hosting service
- Can't buy a domain name - App Service Domain or 3rd party
- Support common records (A, AAAA, CNAME, MX, NS, PTR, SOA, SRV, TXT)
- Each DNS query is answered by the closest available DNS server to provide fast performance and high availability
- Private zones enable VNet to participate either as 
  - Registration Vnet
    - 1 per Private Zone
    - Publish records
  - Resolution Vnet
    - 10 per Private Zone
    - Resolve records


# Custom Domain
- TLS/SSL settings -> private key cerficates -> upload pfx and type password
- custom domain -> create new domain and assign SSL certificate
- EY Process: 
- 1 - get the certificate
- 2 - confirm it has a DNS record for the domain (didn't know at EY had a WAF for that so you must do all the EY stuff - sorry, I don't even have access to SNow so I can't help much there)
- 3 - install it in the webapp
- 4 - create the custom domain
- 5 - assign the certificate to that domain 



# Azure CDN
- distributed network of servers that deliver web content to users
- store cached content 
	
	
	
	

