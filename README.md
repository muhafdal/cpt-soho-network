# SOHO Network
## Version: 8.2.2
### XYZ company is a fast-growing business in Eastern Australia with more than 2 million customers globally. The company deals with the buying and selling of food items, which are primarily operated from the headquarters. The company intends to open a branch near the local village of Bonalbo. Therefore, the company requires young IT graduates to design the network for the branch. The network is intended to operate separately from the HQ network. Being a small network, the company has the following requirements for its implementation:
- One router and one switch to be used (all CISCO products).
- 3 departments (Admin/IT, Finance/HR and Customer service/Reception).
- Each department is required to be in different Vlans.
- Each department is required to have a wireless network for the users.
- Host devices in the network are required to obtain IPv4 address automatically.
- Devices in all the departments are required to communicate with each other.

Assume the ISP gave out a base network of 192.168.1.0, you as the young network engineer who has been hired, design and implement a network considering the above requirements.  
  
--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

Network Address: 192.168.1.0  
Subnets needed: 3  
  
### Number of Subnets:
- 2^x = Subnets needed  
- 2^x = 3  
- 2^1 = 2, this is less than 3, so we need to find a number greater than 2 but closer to 3  
- 2^2 = 4, this is greater than 3 but not too far from it  
- x = 2, so we have 2 as the number of ones in the last octet  

### Subnet Mask:
- 11111111.11111111.11111111.11000000 = /26
- 255.255.255.192 = decimal

### Number of Hosts:
- 2^y-2 = Number of Hosts (y is the number of zeros in the last octet)
- 2^6-2 = (Subtract 2 for IP network and broadcast network)
- 64-2 = 62

### Subnet Block:
- 256-last decimal of subnet mask = Subnet Block  
- 256-128 = 64  
- Subnet Number = 0, 64, 128   

### 1st Subnet
- Subnet Mask: 255.255.255.192
- Network Address: 192.168.1.0
- Min: 192.168.1.1 (network +1)
- Max: 192.168.1.62 (broadcast -1)
- Broadcast Address: 192.168.1.63 (0–63 range = 64 addresses)

### 2nd Subnet
- Subnet Mask: 255.255.255.192
- Network Address: 192.168.1.64 (previous subnet’s broadcast +1)
- Min: 192.168.1.65 (network +1)
- Max: 192.168.1.126 (broadcast -1)
- Broadcast Address: 192.168.1.127 (64–127 range = 64 addresses)

### 3nd Subnet
- Subnet Mask: 255.255.255.192
- Network Address: 192.168.1.128 (previous subnet’s broadcast +1)
- Min: 192.168.1.129 (network +1)
- Max: 192.168.1.190 (broadcast -1)
- Broadcast Address: 192.168.1.191 (128–191 range = 64 addresses)

### VLAN
Each VLAN gets 7 interfaces:  
- VLAN 10 Admin/IT: Interfaces 2-8
- VLAN 20 Finance/HR: Interfaces 9-15
- VLAN 30 Customer-Service/Reception: Interfaces 16-22

### Topology  
![1](https://github.com/user-attachments/assets/8c88b27d-ac9f-4387-91de-0d17b7d13993)  
### Set VLAN  
- vlan (number) - Creates a new VLAN with the specified number  
    Example: `vlan 10`creates VLAN 10  
- name (vlan name) - Assigns a name to the newly created VLAN  
    Example: `name Admin/IT` assigns the name "Admin/IT" to VLAN 10  
- int range f0/..-.. - Enters interface configuration mode for a range of interfaces  
    Example: `int range f0/2-8` configures interfaces FastEthernet 0/2 through 0/8  
- `switchport mode access` - Configures the interface to operate in access mode  
    This sets the port to carry traffic for only one VLAN  
- switchport access vlan (vlan number) - Assigns the interface to a specific VLAN in access mode  
    Example: `switchport access vlan 10` assigns the interface to VLAN 10  
- `int f0/1` - Enters the configuration mode for interface FastEthernet 0/1  
- `switchport mode trunk` - Configures the interface to operate in trunk mode  
    A trunk port can carry traffic for multiple VLANs, typically used between switches  

![2](https://github.com/user-attachments/assets/c1e6cba1-6f5b-4fe5-9bb0-5709dd2d9499)  
### Enable interfaces Gig0/0  
![3](https://github.com/user-attachments/assets/53645f5b-e9a7-41ca-9ae0-bbfb3ada7ca0)  
### Configure subinterfaces on the router for VLANs 10, 20, and 30  
![5](https://github.com/user-attachments/assets/5bf39612-b534-4710-bf1c-1ac5c7c2a4ed)  
### Configure the DHCP pool for all VLANs  
![6](https://github.com/user-attachments/assets/3d1ffaae-3d69-4c47-b9fe-49b3e2c47e02)  
### Set all PCs to DHCP, like this  
![7](https://github.com/user-attachments/assets/5ba31b48-8c59-408e-807a-733c4b0deeae)  
### Set all printers to DHCP, like this  
![8](https://github.com/user-attachments/assets/bb9b0ae0-3552-4f15-9969-65c1627f794b)  
![9](https://github.com/user-attachments/assets/aafe10f7-f3ff-417b-bb4c-5d03a0bdb650)  
### For the access point, set the SSID to be the same as the VLAN name. For example, the SSID for VLAN Admin/IT  
![10](https://github.com/user-attachments/assets/8e7d9d36-8d52-424f-8217-2cdb7227a9f3)  
### Set the wireless on all smartphones to connect to the SSID and password for each VLAN. For example, the SSID from the access point named 'Admin/IT'  
![11](https://github.com/user-attachments/assets/0164e10b-f38b-470b-86c5-e62c2b75aecf)  
### Remove the Fast Ethernet module from the laptop  
![12](https://github.com/user-attachments/assets/a47b8c51-f491-4856-afaa-6aebd3a970e9)  
![13](https://github.com/user-attachments/assets/5e7eeb98-d9f8-4789-816e-1827bcb4d185)  
and replace it with the WPC300N module for wireless  
![14](https://github.com/user-attachments/assets/e4ce0e8c-ba7c-4f34-837f-65f30222719a)  
### After that, set the wireless on all laptops to connect to the SSID and password for each VLAN. For example, the SSID from the access point named 'Admin/IT'  
![15](https://github.com/user-attachments/assets/f8185b9a-acc5-4fc9-8f00-116d2345370e)  
### If all configurations are correct, it should look like this
![Screenshot at 2024-11-17 22-08-18](https://github.com/user-attachments/assets/6dd28e3d-7cc6-487d-a877-536ccb589654)
### Check the connections for all departments  
![16](https://github.com/user-attachments/assets/1bb6cc59-3527-49e5-b4c8-36d9b23decf9)  
