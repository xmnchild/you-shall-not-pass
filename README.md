# You shall not pass
For our Admin&Sys course, we needed to do a 2-week project. The aim was to create a secured network using 4 VMs that would communicate with each other through a gateway. 

## Introduction
The project is composed of 4 VMs. 
- The first one (VM1) is the **gateway**, based on _openBSD7.2_; this VM should have 4 different network interfaces, one in bridge mode and the others in an internal network. The IP addresses of the network interfaces must be static and the VM must be able to automatically deliver (DHCP) IP addresses on the internal networks(LANs). 
- VM2 would act as a **webserver** based on _FreeBsd12_ with one network card in internal network mode. For this VM, we will use nginx along with PHP7.4 and its modules. 
- VM3 and VM4 are both client VMs with graphical interfaces, so we chose to base them on _Debian11_. 

## Preliminaries
To start this project, we needed to schematize the network infrastructure before configuring all the VMs. To better understand the idea of this network, we used Draw.io, which offers excellent network infrastructure schemes. As for the task repartition and project management, we used Trello to better organize our ideas and how we needed to start and put them to work. We concluded that Léa was in charge of the gateway (VM1), Lucas would work on the web server (VM2), and we would go through the details together security-wise. 

## Glossary 
**openBSD** : openBSD is asecurity-focused, free and open-source, Unix-like operating system. OpenBSD emphasizes on portability, standardization, correctness, proactive security and integrated cryptography. OpenBSD is primarly used for _Network appliances_ and _servers_ configuration. Indeed, openBSD features a robust TCP/IP networking stack and can therefore be used as a router or a wireless access point. It also offers security enhancements and packet filter that makes it suitable for security purposes such as firewalls, intrusion-detection systems and VPN gateways. 

**FreeBSD** : FreeBSD is a free and open-source Unix-like operating sytem. FreeBSD has similarities with Linux but differs kernel wise. FreeBSD contains a significant collection of server-related software in the base system and the ports collection, allowing FreeBSD to be configures and used as a mail server, web server, firewall, FTP server, DNS server and a router, among other applications. 

**LAN** : Local area network is a computer network that interconnects computers within a limited area such as a residence, laboratory or office building. 

**DHCP** : Dynamic Host Configuration Protocol is a network management protocal used on Internet Protocol networks for automatically assigning IP addresses and other communication parameters to devices connected to the network using a client-server architecture. 

**Web server** : A web server is computer software and underlying hardware that accepts requests via HTTP (network protocol created to distribute web content) or its secure variant HTTPS. A user agent, commonly a web browser or web crawler, initiates communication by making a request for a web page or other resource using HTTP, and the server responds with the content of that resource or an error message. 

**Subnet** : A subnet is a division of an IP network (internet protocol suite), where an IP network is a set of communications protocols used on the Internet and other similar networks. It is commonly known as TCP/IP (Transmission Control Protocol/Internet Protocol). The act of dividing a network into at least two separate networks is called subnetting, and routers are devices that allow traffic exchange between subnetworks, serving as a physical boundary. IPv4 is the most common one. 

**Netmask** : A netmit "mask" ask is a 32-bit mask used to divide an IP address into subnets and specify the network's available hosts. In a netmask, two bits are always automatically assigned. Netmask defines how "large" a network is or if you're configuring a rule that requires an IP address and a netmask, the netmask will signify to what range of the Network the rule will apply to.

## VM1 - Configuration & Installation
To configure this VM, we downloaded the openBSD iso provided on the official openBSD website and started the process. openBSD installation is a bit tricky because you need to answer a ton of questions to go through the installation. However, we finally managed it and then started the network & DHCP configuration. 

To configure a static address on all the network interfaces, I needed to create a file for each of the network interface and enter the IP address i wanted to assign. In our case : 
- em1 LAN1 administration : 192.168.42.0 netmask 255.255.255.192
- em2 LAN2 server : 192.168.42.64 netmask 255.255.255.192
- em3 LAN3 employee : 192.168.42.128 netmask 255.255.255.192

However, we needed to find the right netmask so the broadcast address asked in the project criteria. You can calculate the netmask using several methods (some using binary calculations or even hosts range). In our case, I used a tool on the Internet to calculate the netmask depending on the broadcast address I want to obtain. The netmask 255.255.255.192 was the response of the many tools I used. 

## Roadmap
If you have ideas for releases in the future, it is a good idea to list them in the README.

## Contributing
State if you are open to contributions and what your requirements are for accepting them.

For people who want to make changes to your project, it's helpful to have some documentation on how to get started. Perhaps there is a script that they should run or some environment variables that they need to set. Make these steps explicit. These instructions could also be useful to your future self.

You can also document commands to lint the code or run tests. These steps help to ensure high code quality and reduce the likelihood that the changes inadvertently break something. Having instructions for running tests is especially helpful if it requires external setup, such as starting a Selenium server for testing in a browser.

## Authors and acknowledgment
Show your appreciation to those who have contributed to the project.

## License
For open source projects, say how it is licensed.

## Project status
If you have run out of energy or time for your project, put a note at the top of the README saying that development has slowed down or stopped completely. Someone may choose to fork your project or volunteer to step in as a maintainer or owner, allowing your project to keep going. You can also make an explicit request for maintainers.
