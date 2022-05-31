# Azure-Firewall-Service

# Why would we use the Azure Firewall Service?
- Azure Firewall looks at inbound/outbound traffic and understand if they are secure requests.
- Companies will use a Azure firewall to protect endpoints from attacks
- All companies have some firewall mechanism. It filters traffic. Some have a firewall appliance and are responsible for the appliance.
- Azure firewall service, a managed service. can be used instead of physical appliance and can be installed on the Azure Virtual Network.


# Features of Azure Firewall Service
- High availability
- Can deploy the service across two or more availability zones
- Can create network filtering rules

# Azure Firewall Service must have its own subnet. 
- There must be enough IP address ranges for the subnets.
- Name must be AzureFirewallSubnet
- It will have a public IP and a private IP
- VMs will communicate with the Azure Firewall Service via its Private IP

# Create a VM with no public IP and a subnet for the Azure Firewall Service
<p align="center">
  
<img src="https://user-images.githubusercontent.com/104326475/171255033-034c69f9-b170-4558-b0b1-1730f2f96d9a.png" height="200%" width="200%" alt="firewall service"/>

<p/>

# Creating the Azure Firewall Service
- Ensure that the Azure Firewall Service is within the same virtual network and region.
- Also add a public IP to the Azure Firewall Service
<p align="center">
  
<img src="https://user-images.githubusercontent.com/104326475/171256418-5737b235-652c-498d-970e-8e4fed3b807f.png" height="100%" width="100%" alt="firewall service"/>

<p/>

