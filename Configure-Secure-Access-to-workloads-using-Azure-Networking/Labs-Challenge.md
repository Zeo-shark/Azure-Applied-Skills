# Title: Configure Secure Access to workloads using Azure Networking

### Key Topics: 
Azure Firewall, Private DNS Zone, VNet Peering, NSG and ASGs.

## Tasks performed
- Create and configure virtual networks
- Configure network routing
- Create DNS zones and configure DNS settings
- Create and configure network security groups (NSGs)
- Create and configure Azure Firewall

## Questions And Solutions:

1. Initially, Azure Firewall will be used for Subnet1-1. Hosts on VNet1 will connect to a third-party internet app service named RelecloudDataService. RelecloudDataService is accessible at 131.107.3.210 on TCP port 9000.

This is your task:

You need to deploy Azure Firewall and allow access from Subnet1-1 to RelecloudDataService. Use a route table to ensure that all other access from Subnet1-1 to the public internet is blocked.

**Solution:** - Deploy Azure Firewall and create a firewall policy in the same resource group as VNet1. You can use the Azure portal or the Azure CLI to do this12.
Create a route table and associate it with Subnet1-1. You can use the Azure portal or the Azure CLI to do this34.
- Add a default route to the route table that points to the private IP address of the Azure Firewall. This will ensure that all outbound traffic from Subnet1-1 goes through the firewall34.
- Add an application rule to the firewall policy that allows access to RelecloudDataService. You can use the Azure portal or the Azure CLI to do this . The rule should have the following properties:
Name: Allow-RelecloudDataService
Priority: 100
Source type: IP
Source: 10.0.1.0/24 (the address range of Subnet1-1)
Protocol: Http
Port: 9000
Target FQDNs: 131.107.3.210
- Add a network rule to the firewall policy that allows access to external DNS servers. You can use the Azure portal or the Azure CLI to do this . The rule should have the following properties:
Name: Allow-DNS
Priority: 200
Source type: IP
Source: 10.0.1.0/24 (the address range of Subnet1-1)
Protocol: UDP
Destination ports: 53
Destination addresses: 168.63.129.16, 8.8.8.8 (the Azure-provided DNS server and a public DNS server)
- Test the firewall by trying to access RelecloudDataService and other internet sites from a VM in Subnet1-1. You should be able to access RelecloudDataService, but not other internet sites. You can use the ping or curl commands to test the connectivity.


2. We are developing an application named App1 that will be provisioned on virtual machines in the West Europe and North Europe Azure regions. Initially, App1 will be deployed to VM2 and VM3. Eventually, a new virtual machine named VM4 that will also host App1 will be deployed to the North Europe region.

This is your task:

You need to configure a subnet to support the deployment of VM4. The subnet must meet the following requirements:

Be in the North Europe region.
Use an IP address space of 10.3.1.0/24.
Ensure that the hosts on the new subnet can communicate with hosts on the same virtual network.
Ensure that the new virtual network is peered with VNet2.

**Solution:** On the Virtual networks page, select + Create.
- On the Basics tab of Create virtual network, enter or select the following information:
Subscription: Select your subscription.
Resource group: Select the resource group that contains VNet2.
Name: Enter a name for the new virtual network, such as VNet3.
Region: Select North Europe.
Address space: Enter 10.3.0.0/16 or another address space that does not overlap with VNet2.
Select Next to proceed to the IP Addresses tab.
- On the IP Addresses tab, select + Add subnet.
On the Add subnet screen, enter or select the following information:
Name: Enter a name for the new subnet, such as Subnet3-1.
Starting address: Enter 10.3.1.0 or another address within the address space of VNet3.
Subnet size: Select /24 (256 addresses) or another size that meets your needs.
Select Save and then select Review + create at the bottom of the screen.
- When validation passes, select Create to create the new virtual network and subnet.
- After the new virtual network and subnet are created, search for and select Virtual network peering.
- On the Virtual network peering page, select + Add.
On the Add peering screen, enter or select the following information:
Subscription: Select your subscription.
Virtual network: Select VNet2.
Name: Enter a name for the peering from VNet2 to VNet3, such as VNet2-to-VNet3.
Virtual network deployment model: Select Resource manager.
Subscription: Select your subscription.
Virtual network: Select VNet3.
Name: Enter a name for the peering from VNet3 to VNet2, such as VNet3-to-VNet2.
- Configure virtual network access settings: Select Enabled for both Allow virtual network access from VNet2 to VNet3 and Allow virtual network access from VNet3 to VNet2.
- Select Add to create the peering between the two virtual networks.
You can now deploy VM4 to Subnet3-1 and connect it to App1 on VM2 and VM3.

2. We want to limit inbound traffic to Subnet1-1.

This is your task:

You need to create an application security group that contains VM2 and VM3. Ensure that Subnet1-1 only allows inbound connections from members of the application security group over TCP port 1433.

**Solution:** You have now created an application security group that contains VM2 and VM3, and limited inbound traffic to Subnet1-1 to only allow connections from the application security group over TCP port 1433. You can verify the connectivity by using tools such as ping or telnet from VM2 or VM3 to Subnet1-1.

3. I am providing the details for the DNS configuration on the subnet.

This is your task:

Configure DNS for the new subnet. Here are your requirements:

Ensure that the hosts on the new subnet automatically register to an Azure Private DNS zone named contoso.com.
Ensure that the hosts on the new subnet can connect to VM2 on Subnet2-1 by using the fully qualified name (FQDN) of vm2.contoso.com.

**Solution:** 
You have now configured DNS for the new subnet. The hosts on the new subnet will automatically register to the contoso.com private DNS zone and be able to connect to VM2 by using the FQDN of vm2.contoso.com. You can verify the connectivity by using tools such as ping or nslookup from a VM in the new subnet.
