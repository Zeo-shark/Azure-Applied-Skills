# Secure storage for Azure Files and Azure Blob Storage

## Tasks performed
- Create and configure a storage account
- Create and configure Blob Storage
- Create and configure Azure Files
- Configure encryption
- Configure networking for storage

## Core Topics: 
Azure Storage Accounts, Azure Blob, Azure Files

Tasks performed
Create and configure a storage account
Create and configure Blob Storage
Create and configure Azure Files
Configure encryption
Configure networking for storage

Provision a storage account named app1sa38017922. If an Azure datacenter fails, app1sa38017922 must fail over to a datacenter in the same zone. In the event of a regional failure, app1sa38017922 must fail over to a different region.
The data in app1sa38017922 must be encrypted by using the app1-key key that has been provisioned already and by using a system-assigned managed identity.
app1sa38017922 requires a blob container named images. The container must allow private access only.
The App1-ManagedId user-assigned managed identity must be able to read blobs in app1sa38017922. App1-ManagedId must be prevented from modifying existing blobs or creating new blobs.
app1sa38017922 requires a file share named share1 that will be used by app1sa38017922 to archive daily reports. The file share must be created in the same storage account used by other App1 data. The file share must minimize costs for data storage.
Thanks,

Task 2:
We are building a custom application named App2. App2 will be deployed to virtual machines located in VNET1/Subnet1.

This is your task:

You need to configure an Azure Storage account for long-term storage of backup and audit log data of App2. The storage account must meet the following requirements:

Provision a storage account named app2sa38017922 that uses locally-redundant storage (LRS) and contains two containers named backups and auditlogs.
Blobs in the backups container must be moved to the least expensive storage tier 90 days after the blobs are created. Blobs in other containers must not be moved.
Data in the auditlogs container cannot be modified or deleted by any users, including administrators, for 10 years after they are created.
Blob storage in app2sa38017922 must be accessible by using a private IP address from VNET1/Subnet1.

Task 3:
We have existing storage accounts named data38017922 and replica38017922.

This is your task:

You need to configure the storage accounts to meet the following requirements:

In data38017922 create a new blob container named container4 that has an encryption scope with infrastructure encryption enabled.
Configure data38017922/container1 to replicate to replica38017922/container1.
Configure network security of replica38017922 to ensure that a public host with an IP address of 131.107.4.18 can access replica38017922. Access from Azure virtual networks and other public hosts must be blocked.


