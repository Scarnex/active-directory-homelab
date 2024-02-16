# Active Directory Home Lab Project Report

## Introduction
In the ever-changing world of computer networks and keeping things secure, I set up my own home lab to show how what I've learned can be useful in real life. This project is all about planning and doing the hands-on work for my VM network. I used a double network card setup, added Active Directory, and put in different security measures. From figuring out names for different parts of the network to making things work automatically with PowerShell, every step in this project mixes what I've learned with practical experience. 

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
To sum up, this home lab project is a complete display of network engineering, security setup, and making user management easier with automation. The choices I made in designing, like using Network Address Translation (NAT), setting up a DHCP server, and using PowerShell scripts, really make the project work well. The success of combining RAS/NAT, DHCP, and Active Directory, shown in the pictures, proves that the project works smoothly. This project not only shows how to handle networks well but also can help anyone learn about network architecture and cybersecurity. I enjoyed working on this project, and I'm eager to embark on more personal projects in the future.
