# Active Directory Home Lab Project Report

## Introduction

This home lab includes two dedicated Network Interface Cards (NICs): one for internet access using NAT (Network Address Translation) and the other for the internal virtual machine network. The internal network's IP address is assigned within the class C range for simplicity, set to 192.168.0.1.

![Figure 1: Home lab network architecture](![Screenshot 2024-01-02 115327](https://github.com/Scarnex/active-directory-homelab/assets/79904643/632bf5e4-dca7-401e-a914-590288bd1ed2)
)

I've used "mydomain.sa" as the domain name for simplicity, with ".sa" representing the country of residence.

## Active Directory Installation

![Figure 2: Successfully installed Active Directory](link_to_image)

The first user, "yalshaibani," was created with admin rights to enhance security. Consideration was given to using a non-full name format like "y.alshaibani."

![Figure 3: Created the first user with admin rights](link_to_image)

## RAS/NAT Configuration

To allow clients to be on a private virtual network with internet access through the domain controller, RAS/NAT (Remote Access Server/Network Address Translation) was installed.

![Figure 4: Configured RAS/NAT for internet access](link_to_image)

## DHCP Server Setup

For automatic IP address assignment to Windows 10 clients, the DHCP server on the domain controller was configured with an IP address range of 192.168.0.10 to 192.168.0.100, providing 91 dynamic IP addresses.

![Figure 5: Setting up the DHCP server](link_to_image)

A standard 8-day lease period was chosen, considering the typical usage duration for clients. The default gateway is set to the router's IP address, 192.168.0.1.

![Figure 6: Successfully set up the DHCP server](link_to_image)

## PowerShell Script for User Creation

A PowerShell script, provided by Josh Madakor on GitHub, was used to automate the creation of users in Active Directory. This method is not recommended for production environments but serves as a useful example for a lab.

![Figure 7: 1000+ users added to Active Directory](link_to_image)

## Windows 10 Virtual Machine Creation

The last step involved creating a Windows 10 virtual machine for clients, connected to the internal network and obtaining a DHCP address from the domain controller.

![Figure 8: CLIENT1 IP configuration](link_to_image)

## Network Connectivity

The entire network infrastructure was tested successfully, demonstrating connectivity to the default gateway (domain controller). The domain controller effectively forwarded pings to Google and received replies.

![Figure 9: CLIENT1 in the domain controller's DHCP list](link_to_image)

Signing in as one of the 1000+ users, I demonstrated the login process using credentials similar to a corporate network.

![Figure 10: Signed in as Ashlie Abrev](link_to_image)
