# Configuring-NSG-and-ASG-for-Web-and-Management-Servers
## Description
This project illustrates how organizations implement virtual networking infrastructure and verify its functionality. Specifically, I created servers into two groups: Web Servers and Management Servers. Each server group resides within its own Application Security Group, allowing RDP access only to the Management Servers and not the Web Servers. Virtual Machine was use for the configuration of both server to access the AGS. The Web Servers are configured to display the IIS web page accessible from the internet. Network Security Group (NSG) rules are employed to manage network access. This lab is designed to simulate a business environment setup, utilizing tools such as the Microsoft Azure portal for configuration and Microsoft Server 2019 for testing the web server.

## Languages and Utilities Used
  + Microsoft Server 2019
## Environments Used
  + Azure Portal
  + Virtual Machines
## Program walk-through

[![Untitled-Diagram-drawio-1.png](https://i.postimg.cc/htqDYk8L/Untitled-Diagram-drawio-1.png)](https://postimg.cc/3dnQ4bcN)

The first step for this task was to log into my Azure account. Then, I created a resource group for the resources. Next, I created a virtual network named "vicvirtualnetwork" with an IPv4 address space of 10.0.0.0/16. I then edited the subnet blade to verify the default subnet address range of 10.0.0.0/24 and created it

[![Screenshot-2024-07-18-133227.png](https://i.postimg.cc/brxVQWhv/Screenshot-2024-07-18-133227.png)](https://postimg.cc/K3Y5b94X)


Next, I created two Application Security Groups (ASGs): one for the web servers and another for the management servers. The ASGs which is designed to simplify network security management for virtual machines (VMs) by grouping them based on their application requirements. The ASG for the web servers includes all VMs functioning as web servers, allowing for the application of network security rules specific to web traffic, such as permitting HTTP/HTTPS traffic from the internet. The ASG for the management servers includes all VMs functioning as management servers, enabling the application of network security rules specific to management traffic, such as allowing RDP access from specific IPs, for examole an administrator computer

[![Screenshot-2024-07-18-133609.png](https://i.postimg.cc/yN2L2s6d/Screenshot-2024-07-18-133609.png)](https://postimg.cc/SX7LM0MF)


[![Screenshot-2024-07-18-133227.png](https://i.postimg.cc/brxVQWhv/Screenshot-2024-07-18-133227.png)](https://postimg.cc/K3Y5b94X)


Next, I created a Network Security Group (NSG) to associate with the subnet. The NSG acts like a virtual firewall for your VMs, controlling both inbound and outbound traffic. It defines rules to allow or deny traffic based on factors like source and destination IP addresses, ports, and protocols. In this case, I configured the NSG to only allow inbound traffic for both the web and management servers. Specifically, the NSG has rules to permit Remote Desktop Protocol (RDP) traffic to the management servers and rules to allow incoming web traffic (HTTP and HTTPS) to the web servers. This configuration is essential for users to access the websites hosted on the web servers


[![Screenshot-2024-07-18-134122.png](https://i.postimg.cc/zGBpBVVv/Screenshot-2024-07-18-134122.png)](https://postimg.cc/RNkwpC1x)


[![Screenshot-2024-07-18-134436.png](https://i.postimg.cc/MTym4BrP/Screenshot-2024-07-18-134436.png)](https://postimg.cc/zbGhHyNK)

Below are all the resources that have been created

[![Screenshot-2024-07-18-134320.png](https://i.postimg.cc/DyfPj8Q6/Screenshot-2024-07-18-134320.png)](https://postimg.cc/Lh7Ph4bg)

I configured inbound NSG security rules to allow all traffic to the web servers and RDP access to the servers. In the "Add inbound security rule" blade, I specified settings to allow TCP ports 80 and 443 for the `myAsgWebServers` application security group. Additionally, I specified settings to allow the RDP port (TCP 3389) for the `myAsgMgmtServers` application security group.

[![Screenshot-2024-07-18-135227.png](https://i.postimg.cc/28Xh0TSj/Screenshot-2024-07-18-135227.png)](https://postimg.cc/vcf4BrnC)

[![Screenshot-2024-07-18-135620.png](https://i.postimg.cc/0yTmsQSL/Screenshot-2024-07-18-135620.png)](https://postimg.cc/K1547mJN)

[![Screenshot-2024-07-18-135814.png](https://i.postimg.cc/P5wp2j7K/Screenshot-2024-07-18-135814.png)](https://postimg.cc/21CSSPrB)

After deploying the virtual network, setting up network security with inbound security rules, and creating the two application security groups, I created virtual machines for both servers. Each virtual machine's network interface was associated with the corresponding application security group. The network interface for the `myVMWeb` virtual machine was associated with the `myAsgWebServers` ASG, and the network interface for the `myVMMgmt` virtual machine was associated with the `myAsgMgmtServers` ASG

[![Screenshot-2024-07-18-150845.png](https://i.postimg.cc/bJQ4Ts08/Screenshot-2024-07-18-150845.png)](https://postimg.cc/2bSHjjXX)

[![Screenshot-2024-07-18-151059.png](https://i.postimg.cc/kGqzhqwS/Screenshot-2024-07-18-151059.png)](https://postimg.cc/njS3X8yV)

[![Screenshot-2024-07-18-144345.png](https://i.postimg.cc/9MMcgPMV/Screenshot-2024-07-18-144345.png)](https://postimg.cc/PLgGPwYF)

Test the network traffic filtering

I tested the network traffic filters to ensure I could successfully RDP into the `myVMMgmt` virtual machine and verified that the Remote Desktop connection was successful. At this point, I confirmed that I can connect via Remote Desktop to `myVMMgmt` and accessed the internet to verify that `myVMWeb` is reachable via HTTP/HTTPS, successfully displaying the default IIS web page

[![Screenshot-2024-07-18-151334.png](https://i.postimg.cc/BQw72TWH/Screenshot-2024-07-18-151334.png)](https://postimg.cc/mtCSsFgg)

[![Screenshot-2024-07-18-154505.png](https://i.postimg.cc/3rttHXxV/Screenshot-2024-07-18-154505.png)](https://postimg.cc/0rJYYJm0)

[![Screenshot-2024-07-18-154334.png](https://i.postimg.cc/htfwYC82/Screenshot-2024-07-18-154334.png)](https://postimg.cc/RWxX6LDt)
