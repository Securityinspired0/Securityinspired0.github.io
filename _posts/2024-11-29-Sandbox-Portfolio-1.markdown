---
layout: post
title: Portfolio 02 Sandboxed Network Lab Report
date: 2024-11-11
---

## INTRODUCTION

This report documents the setup and functionaly of a sandboxed network I created using VitualBox. The network consisits of three virtual machines (VMs) connected accross two subnets. The tree VMs in this setup are:
* Ubuntu Desktop
* Gateway-Router
* Ghost Application Server

The purpose of this network is to demonstrate a secure communication between the devices within the network and provide internet access through the Gateway-Router. This setup also includes the testing of different funcationalities such as browsing and pinging.

### NETWORK DIAMGRAM

The following diagram illustrate the sandbox network architecture

<figure>
    <img src ="/assets/img/network-diagram.png">
    <figcaption>Sandboxed Network Architecture</figcaption>
</figure>

This diagram represents the network configuration as follows:

* Ubuntu Desktop is connected to the network with a static IP address 192.168.2.1 and configured to use an internal network setting in VirtualBox.
* Gateway-Router serves as the main routing device in the network, facilitating communication between the two subnets and providing internet access. It is configured with three network adapters:
    * Adapter 1 is set to NAT mode, providing internet access to the internal network through the Gateway-Router.
    * Adapter 2 and 3 are set to use the "Internal Network" option, ensuring that communication is restricted to the local environment between VMs.
* Ghost Application Server is also connected to the internal network with a static IP address 192.168.102.2 and provides content management services to the Ubuntu Desktop.

The network is designed to ensure the following:

Ubuntu Desktop can communicate with the Web Server.
Ubuntu Desktop can access the internet through the Gateway-Router.
The Gateway-Router routes traffic between the two subnets (192.168.x.x and 192.168.xxx.x) and provides network address translation (NAT) for internet access.

## IP Address Table

<img src ="/assets/img/network-diagram.png">

## VM Configuration and Functionality

### Ubuntu Desktop Functionality 

* Successfully accessed the application server from the desktop using a browser.

<img src ="/assets/img/user-blog.png">

By default, when we access the Ghost server from the Ubuntu desktop, you should see the static website hosted by the Ghost application. However, I have decided to customize this setup to demonstrate how flexible and interconnected network configurations can be. Instead of the default Ghost-hosted website, accessing the server from the Ubuntu desktop now displays my locally hosted GitHub static website.

<img src ="/assets/img/static.png">

* Demonstrated internet access through the Gateway-Router by resolving a public domain 

<img src ="/assets/img/static.png">

### Gateway-Router Functionality

Enabled routing between Subnet 01 (192.168.x.x) and Subnet 02 (192.168.xxx.x).

Provided internet access to the ubuntu desktop and application server via the NAT adapter.

<figure>
    <img src ="/assets/img/ubuntu-gateway-ping.png">
    <figcaption>Ping results from Ubuntu Desktop to Application Server</figcaption>
</figure>

<figure>
    <img src ="/assets/img/gateway-ping.png">
    <figcaption>Gateway routing configuration.</figcaption>
</figure>

### Web Server Functionality

<figure>
    <img src ="/assets/img/gateway-ping.png">
    <figcaption>Application server logs showing requests from the desktop.</figcaption>
</figure>

## Gateway-Router Traffic Logging

To monitor network traffic, I configured logging on the Gateway-Router using tcpdump. The captured logs provided insight into forwarded packets between the subnets and requests to external networks. The following screenshot shows the captured logs:

<img src ="/assets/img/tcpdump-log.png">


## Lab Demonstration

### Screencast Link

A video demonstration showcasing the sandboxed network's setup and functionality can be accessed [here.](https://roehamptonprod-my.sharepoint.com/:v:/r/personal/adesanyo2_roehampton_ac_uk/Documents/Sandbox.mp4?csf=1&web=1&e=U3V2na&nav=eyJyZWZlcnJhbEluZm8iOnsicmVmZXJyYWxBcHAiOiJTdHJlYW1XZWJBcHAiLCJyZWZlcnJhbFZpZXciOiJTaGFyZURpYWxvZy1MaW5rIiwicmVmZXJyYWxBcHBQbGF0Zm9ybSI6IldlYiIsInJlZmVycmFsTW9kZSI6InZpZXcifX0%3D)


## Conclusion
The sandboxed network is functional as designed, with the Ubuntu Desktop able to communicate with the Web Server and access the internet via the Gateway-Router. This setup demonstrates basic network functionality such as DNS resolution, web browsing, and routing between subnets. The Gateway-Router effectively handles the routing between the internal network and the internet, allowing all devices to communicate as expected.


## References

* [VirtualBox Documentation](https://www.virtualbox.org/wiki/Documentation)
* [Ubuntu Official Site](https://help.ubuntu.com/community/CommunityHelpWiki)
* Chat GPT
* [Stackoverflow](https://stackoverflow.com/)
* [Nginx](https://nginx.org/en/docs/)
