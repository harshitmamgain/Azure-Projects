# Implementing Virtual Networking with DNS resolution

In this Project, I have implemented Virtual Networking solution for Virtual Machine's on Azure. In this I have configured a Virtual Network, Deployed the VMs to the Virtual Network, Configured Private and Public IPs for the VMs, configured Network Security Groups and finally configured Azure DNS for internal and external name resolution.

# Project Details
 - The services that were used during the course of this Projects are as follows:
     - Powershell 
     - Virtual Networks
     - Network Security Group
     - Private DNS Zones
     - DNS Zones
- Please refer to the DOCX file for a detailed report and screen captures.  

# Steps

- Created a Virtual Network, placed this VNET in a resource group and assigned an IPv4 addresses to this Virtual Network (10.40.0.0/20). 

- Deployed a ARM Template using Powershell.

- Assigned Public IPs (Basic SKU and Dynamic Assignment) to the Network Interface Cards of the two VMs and Static Internal IP Assignment.

- Created a Network Security Group policy to allow inbound traffic from anywhere to the VMs for RDP connection on Port 3389.

- Using the 'Private DNS Zone' Azure service created Private DNS for internal name resolution. 

- Using 'DNS Zone' Azure Service created a Public DNS Zone for external name resolution. 
 

# Conclusion

I have succesfully implemented Internal Name Resoultion and External Name resolution for the Machines on the Virtual network to make it easier to remember domain names instead of hard to remember the Internal and External IP addresses. To add further to this project, this DNS resolution can be useful in load distribution and faster access using caching.
