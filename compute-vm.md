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
