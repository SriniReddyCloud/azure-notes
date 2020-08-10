# Azure Virtual Machine
## Virtual Machine Architecture
![image](https://user-images.githubusercontent.com/28542935/89816803-2e8cd880-db15-11ea-93a6-5f83b93d9b5e.png)

## Instance Types
- G Series: general purposed
- Ls Series: storage optimized
  - local NVMe Storage
  - High disk throughput and IO
  - Ideal for big data, databases, data warehouses
  
![image](https://user-images.githubusercontent.com/28542935/89816823-377daa00-db15-11ea-8214-9a4dc8aab8a2.png)

## Disks
### Virtual hard disks (VHD)
VMs use disks to store OS, apps, and data
- OS disk
  - must have
  - C drive
  - Azure Storage
  - Read and write caching by default
  - Can chose SKUs
  - Ephemeral OS disk - Short-term temporary
- Temp disk 
	- Must
  - D drive
  - short-term storage
  - Not in Azure Storage, Local to the VM node
  - Read caching can be enabled
  - data may be lost when VM is redeployed
  - A series VM - HDD, others - SSD
- Data disk
  - Optional
  - E drive, F drive, …
  - store app data
  - Azure Storage
  - No caching by default
    - If host SQL server, disk for data files can have read caching, disk for log file no caching
  - Can chose SKUs

### Disk Types
- Unmanaged disks - NEVER use this
- Managed disks
- Availability sets with managed disks
  ![image](https://user-images.githubusercontent.com/28542935/89816848-419fa880-db15-11ea-8353-a06d5c2ff335.png)
  
### Disk Infrastructure
- stored in an Azure Storage Account - Page Blobs
- For standard managed disks: always max size - storage only charges data written on disk

### Disk Performance / SKUs
- Standard HDD disks
- Standard SSD disks
- Premium SSD disks
  - higher and certain IOPS per disk
  - Only LRS replication
  - Charge on disk size
  - Only support specific VM series
- A VM can use mix of disks

### Disk Snapshot
- Read-only copy of a managed disk
- Charged on data written
- Standard snapshot can create premium disk
- Azure resource - supports RBAC, SAS

### Disk Image
- VM -> Capture
- Contains a VM configurations and disks
- VM can be depoyed from an image
- VM must be generalized if OS is windows
- Azure resource - supports RBAC, SAS

### Disk Encryption
- Storage level encryption
  - Microsoft managed key by default
  - BYOK
    - Require Disk Encryption Set
    - Can't change back
    - AKV has to be in the same region
  - Exported disks are not encrypted
- OS level encryption: Azure Disk Encryption (ADE)
  - Windows: BitLocker 
  - Linux: DM-Crypt - ADE will format data disks
  - Integrate with AKV to store keys - BYOK
  - Exported disks are encrypted
  - Backup VMs are also encrypted
  - Powershell cmdlet: Set-AzureRmVMDiskEncryptionExtension
  - Reboot the VM and take 15 mins
![image](https://user-images.githubusercontent.com/28542935/89816856-43696c00-db15-11ea-88ba-8a234b2f6914.png)

## Networking
- A VM must live inside a VNet 
- Inbound port rules
  - By default, access to the virtual machine is restricted to sources in the same virtual network, and traffic from Azure load balancing solutions. 
  - network interface card (NIC): not recommended, network security should be managed by NSG in the associated subnet
  
## High Availability
- Can't change after VM is created
- Do NOT provide load balancing
### - Availability Set
  - A logical group of discrete VMs
  - Each VM can have its own properties (name, IP, size, …)
  - Spread across Fault domains (1-3) and Update domain (1-20)
  - Free 
### - Availability Zone
  - Available in few regions: Central US
  - 3 separate physical datacenters in the region
- SLAs
  - Single instance with premium storage for all operating disks and data disks: 99.9%
  - 2 or more instances in same Availability Set: 99.95%
  - 2 or more instances in 2 or more Availability Zones: 99.99%
  
## Proximity Placement Group
- A proximity placement group is a logical grouping used to make sure that Azure compute resources are physically located close to each other
- useful for workloads where low latency is a requirement

## Monitor
- Diagnostic Settings: enable guest-level monitoring
  - Collect data for counters: CPU, memory, disk, network, (ASP.NET, SQL Server)
  - Event logs: IIS, .NET
  - Stored in storage account with retention periods configurable
- Metrics: automatically collected

## Operations
- Stop: OS is shut down (charge doesn't stop)
- Allocation: VM is deployed to a node
- Deallocation: VM is not deployed to a node
- Patching - Update Management
- Anti-malware
- Backup 

## Cost Saving
### - Azure Spot Instance
  - Discounted rate for spare VMs in Azure
  - Will get evicted (stopped/deallocated) if the VMs are needed
### - Reserved Instance
  - Discounted rate for reservation for multiple years
  - Shared across different sizes of VMs in flexibility group
