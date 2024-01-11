# Active Directory Home Lab Project Report

## Introduction
In the ever-evolving landscape of network architecture and cybersecurity, the implementation of a robust home lab serves as a testament to the practical application of knowledge and skills. This project outlines the meticulous design and execution of a network infrastructure, leveraging a dual-NIC setup, Active Directory, and various security measures. From the intricacies of domain naming conventions to the seamless integration of PowerShell automation, this initiative encapsulates the fusion of theory and hands-on experience. Through this documentation, we delve into the intricacies of each stage, highlighting the ingenuity behind the decisions made in network configuration, user management, and the establishment of a secure, interconnected environment.

## Network Architecture
This home lab will have two different NICs (Network Interface Cards), one dedicated to the internet using NAT (Network Address Translation), and the other for the internal virtual machine network for the client machines. I have assigned a class C range to the internal network's IP address for simplicity, which is 192.168.0.1. For the DNS server, I have set it to 127.0.0.1, a loopback address that will reroute itself as the DNS. The network architecture is illustrated in Figure 1.

*Figure 1: Home lab network architecture*

![Home lab network architecture](https://i.imgur.com/WJ4o2T1.png)

## Domain Naming Convention
I used 'mydomain.sa' as the domain name for simplicity, with '.sa' representing the country where I currently reside.

## Active Directory Installation

*Figure 2: Successfully installed Active Directory*

![Figure 2: Successfully installed Active Directory](https://i.imgur.com/Y1O6nGY.png)

## User Account Management
I created the first user with the username 'yalshaibani.' For enhanced security, it's advisable not to use the full name for user log-on. Another option could have been 'y.alshaibani.' The user also has admin rights, as shown in Figure 3.

*Figure 3: Created the first user with admin rights*

![Figure 3: Created the first user with admin rights](https://i.imgur.com/uv8CR7D.png)

## Remote Access Server/Network Address Translation (RAS/NAT)
The next step is to install RAS/NAT, enabling clients to be on a private virtual network while still having internet access through the domain controller. Once configured, clients will have internet access (Figure 4).

*Figure 4: Configured RAS/NAT for Internet access.*

![Figure 4: Configured RAS/NAT for internet access](https://i.imgur.com/i3GLNkw.png)

## DHCP Server Setup
I set up the DHCP server on our domain controller to automatically assign IP addresses to our Windows 10 clients, selecting the range 192.168.0.10 to 192.168.0.100. This allows for 91 dynamic IP addresses to be assigned by the DHCP server.

*Figure 5: Setting up the IP address range for DHCP.*

![Figure 5: Setting up the DHCP server](https://i.imgur.com/TxZvSMo.png)

For the lease duration, I decided to go with an 8-day lease period because it is the standard. What that means is that this IP address will be given to the client for 8 days before it refreshes, one must consider how much time a client should have that unique IP address. For example, if I were setting up a cafe where customers would use the public wifi for about an hour, it makes sense to set the lease duration for 2 hours because there are only so many IP addresses that can be given out. The default gateway should be the IP address of the router, in this case, it is 192.168.0.1.

*Figure 6: Successfully set up the DHCP server.*

![Figure 6: Successfully set up the DHCP server](https://i.imgur.com/Oonamgx.png)

## PowerShell Script for User Creation
Using a PowerShell script, I automated the creation of users in Active Directory instead of manual creation. This PowerShell script works by gathering names from a .txt file and then creating corresponding user accounts. Credit goes to Josh Madakor for providing [this script on GitHub](https://github.com/joshmadakor1/AD_PS). While not recommended for a production environment, it serves as a good example for a lab (Figure 7).

*Figure 7: +1000 users have been added to the Active Directory.*

![Figure 7: 1000+ users added to Active Directory](https://i.imgur.com/IR6OFyv.png)

## Windows 10 Virtual Machine Creation
The last step is to create a Windows 10 virtual machine for our clients. The client network is connected to the internal network, receiving a DHCP address from the domain controller (Figure 8).

*Figure 8: CLIENT1 IP configuration.*

![Figure 8: CLIENT1 IP configuration](https://i.imgur.com/aIN7NK5.png)

The entire network infrastructure is operational, with connectivity to the default gateway (domain controller). Pings are properly forwarded to Google, and replies are received.

*Figure 9: CLIENT1 is in the domain controller's DHCP list.*

![Figure 9: CLIENT1 in the domain controller's DHCP list](https://i.imgur.com/gSU5bow.png)

## User Authentication
Signing in using one of the 1000 user's usernames with the provided password, as shown in Figure 10. This simulates a corporate network where employee credentials are on the domain.

*Figure 10: Signed in as Ashlie Abrev.*

![Figure 10: Signed in as Ashlie Abrev](https://i.imgur.com/YGewApR.png)

## Conclusion
In conclusion, this home lab project stands as a comprehensive showcase of network engineering, security implementation, and automated user management. The articulated design choices, such as the utilization of Network Address Translation (NAT), DHCP server setup, and PowerShell scripting, contribute to the project's efficacy. The successful integration of RAS/NAT, DHCP, and Active Directory, illustrated in the accompanying figures, attests to the project's operational success. Furthermore, the confirmation of network infrastructure functionality and user authentication solidifies the practicality and relevance of the implemented solutions. This endeavor not only reflects proficiency in network administration but also serves as a valuable reference for future endeavors in the dynamic realm of network architecture and cybersecurity.

