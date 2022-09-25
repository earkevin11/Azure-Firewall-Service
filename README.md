# Azure-Firewall-Service

# Why would we use the Azure Firewall Service?
- Azure Firewall looks at inbound/outbound traffic and understand if they are secure requests.
- Companies will use a Azure firewall to protect endpoints from attacks
- All companies have some firewall mechanism. It filters traffic. Some have a firewall appliance and are responsible for the appliance.
- Azure firewall service, a managed service, can be used instead of physical appliance and can be installed on the Azure Virtual Network.


# Features of Azure Firewall Service
- High availability
- Can deploy the service across two or more availability zones
- Can create network filtering rules

# Use Case: Access the VM by RDP into the Azure Firewall Service on its public IP
- Set up a vm and azure firewall service 
- Add a DNAT rule to allow RDP into vm
<p align="center">
  
<img src="https://user-images.githubusercontent.com/104326475/171281298-07af8ad3-a335-4288-ae36-273c9e2a49bd.png" height="80%" width="80%" alt="firewall service"/>

<p/>


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
  
<img src="https://user-images.githubusercontent.com/104326475/171256418-5737b235-652c-498d-970e-8e4fed3b807f.png" height="70%" width="70%" alt="firewall service"/>

<p/> 

# Add a DNAT rule within the Firewall Policy
- Navigate to Firewall Service > Firewall Policy > DNAT rule > Add a rule collection
- Source is the computer that will RDP into the Firewall Service.
- I blurred my personal laptop's IP address.
- Azure Firewall Service listens on port 4000
- Destination is the public IP of the Azure Firewall Service
- Translated Address is the demovm's private IP. Firewall Service will forward to request to that machine.
- Translated port is 3389 since it is RDP

<p align="center">
  
<img src="https://user-images.githubusercontent.com/104326475/171262923-91a9ab04-b0a9-46d1-9e0d-1a2356eea9ec.png" height="270%" width="270%" alt="firewall service"/>

<p/> 

# RDP into Azure Firewall Service

<p align="center">
  
<img src="https://user-images.githubusercontent.com/104326475/171262401-65ccdac9-870c-4467-af56-be500f29f498.png" height="170%" width="170%" alt="firewall service"/>

<p/> 


# Successful RDP 
<p align="center">
  
<img src="https://user-images.githubusercontent.com/104326475/171262439-497169d3-d57f-4d4c-ada8-18d68ab725b5.png" height="70%" width="70%" alt="firewall service"/>

<p/> 


# Create the route table

<p align="center">
  
<img src="https://user-images.githubusercontent.com/104326475/171265006-0925c196-8465-4d82-bb3e-ede30ab2bfc1.png" height="40%" width="40%" alt="firewall service"/>

<p/> 


# How to route traffic through the firewall?
- Use Route Table service
- Associate the route table to the subnet that contains demovm
<p align="center">
  
<img src="https://user-images.githubusercontent.com/104326475/171265240-82216d23-3656-4ba1-9834-2d86e988990c.png" height="170%" width="170%" alt="firewall service"/>

<p/>

- This will allow admins to control traffic outbound to the internet within demovm
- Any traffic that goes to the internet needs to go through the firewall appliance on its private IP
- 0.0.0.0/0 is the internet
- Next hop address is 10.0.1.4, which is the firewall appliance's private IP

<p align="center">
  
<img src="https://user-images.githubusercontent.com/104326475/171265639-ebe4e733-b770-4ce5-a38b-1a9fe87dfcf5.png" height="170%" width="170%" alt="firewall service"/>

<p/> 


- Try accessing the internet now within demovm
- Users will not be allowed because there isn't a application allow rule in the azure firewall service

<p align="center">
  
<img src="https://user-images.githubusercontent.com/104326475/171266451-1d93bc7f-66cf-4238-9c29-36d60604262b.png" height="170%" width="170%" alt="firewall service"/>

<p/> 


# Application Rules
- Use application rules when admins want to allow users to access fully qualified domain names
- Source is the privateip of the demovm since we are trying to access the internet from the demovm.
- HTTP, HTTPS because those are web pages that listen on port HTTP and HTTPS

<p align="center">
  
<img src="https://user-images.githubusercontent.com/104326475/171270684-2bfe0ae4-a32c-4e03-adcc-4d0e070adebb.png" height="250%" width="250%" alt="firewall service"/>

<p/> 

# Successful application rules to access google.com and microsoft.com
<p align="center">
  
<img src="https://user-images.githubusercontent.com/104326475/171271943-e4662fc3-3d54-4d5a-af97-e958e8b7bf49.png" height="250%" width="250%" alt="firewall service"/>

<p/> 


<p align="center">
  
<img src="https://user-images.githubusercontent.com/104326475/171271959-4e8ec153-d4f3-4534-9be7-0fdf8c7e21c4.png" height="250%" width="250%" alt="firewall service"/>

<p/> 
