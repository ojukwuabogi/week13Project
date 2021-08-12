# Week13Project
 
Project 1: ELK Stack Deployment

The files and Folders in this repository were used to configure the ELK Stack Deployment for Project 1.

This document contains the following details:
•	Description of the Topology
•	Ansible Play book names
•	Beats in Use
•	Machines Being Monitored
•	How to Use the Ansible Build


 Description of the Network Topology

The main purpose of this network Diagram is to reflect the topology of the Azure deployment of my ELK. There are 4 virtual machines a load balancer and peered networks.
The load balancer is used to filter traffic and to make sure there is redundancy if either of the web servers are down that is web1 and web2. 
Web1 and web2 are running DVWA and so there is redundancy if one was to go down.
There is also the ELK server which is configured to monitor web1 web2 and the jumpbox.
On the Elk server, Filebeat is installed and used to monitor for Log files or log events
     Metricbeat is also installed on the ELK server. It is used to hold incoming data and them transfer them to Elastisearch or logstach for           further analysis. The integration of the ELK server allows for easy monitoring of vulnerabilities in system files or configuration files 
    
The list below shows the name Function IP address and Operating system of the VM in my Cloud Network



Name	                  Function	  IP address	Operating system
Jumpbox Provisioner	    Gateway	  10.0.0.4	     Linux
Web1	                   Webserver	10.0.0.5	     Linux
Web2                    	Webserver	10.0.0.6	    Linux
ELK-Server	              Webserver	10.1.0.4	     Linux



Only the _Jump box Provisioner VM has and Personal laptop can accept connections from the  Internet. Access to this machine is only allowed from the following IP addresses 71.17.51.161.
The machines inside the network can only be accessed through the Jump box Provisioner


ELK Configuration

I used Ansible to automate configuration of the Virtual Machines. No configuration was performed manually, which saved a lot of time.
      


Using the Playbook
There were 5 playbook used in this deployment
GTelkpay.yml
Metribeat-GTplaybook.yml
Metribeat-configuration.yml
filebeat-GTplaybook.yml
filebeat-configuration.yml

These playbooks were scripted in order to bring up ELK-Server , Metribeat and Filebeat

In order to use the playbook, you will need to have an Ansible running on the Docker and the Docker configured. 
To edit ansible
nano /etc/ansible//(name of playbook)..yml then add/edit file
To run the ansible

ansible-playbook /etc/ansible/(name of playbook).yml then add/edit file

    To get into ELK-Server  to make sure it is working, the url and ports are listed below?
http://40.122.211.230:5601/app/kibana





Project 1 Interview Activity
Domain: Cloud Security
 
**Question 1: Cloud Access Control**

How would you control access to a cloud network?
1.	Restate the Problem
•	You can control access to the Cloud network by setting up Acces control Lists that only allow trusted Traffic and blocking everything else as best as you can.

2.	Provide a Concrete Example Scenario

•	In Project 1, did you deploy an on-premises or cloud network?
            in this project I deployed a cloud network
•	Did you have to configure access controls to this network?
         Yes, In this project I configured access control.
•	What kinds of access controls did you configure, and why were they necessary?
In this environment I created a security group and assigned an inbound security rule allowing access through  ssh to port  22 from the Red Team virtual network. This was necessary for access the VM’s (web1 and Web2) gain access to ELK-Server  through port 22.

•	How do these details relate to the interview question?
Organizations lock their environment to external and some internal vulnerabilities , most organizations need to make sure that there are access is limited to a need to know and or need to access basis , so sensitive information do not get accessed due to poor controls in play. 


3.	Explain the Solution Requirements

•	In Project 1, what kinds of access controls did you have to   implement? Consider
Network Security Group was deployed on the ELK Virtual Network and all the Web virtual Machines. There were security rules that specifically allowed or denied traffic within the firewall/VM with specific ports.

•	What did each access control achieve, and why was this restriction  necessary for the project?
●		Network Security Groups were used to create rules that allow or deny inbound network traffic. This was necessary so that only controlled and allowed traffic and specified ports were to traverse the Network

●		The firewalls were configured on each vm to only allow the specific traffic to move through the allowed ports . The Firewall rules used the source IP destination IP and Ports to lock down the network.


●	Transmission Control Protocol (TCP)  defining the traffic that was to go through these ports that were open. This was for access to DVWA,



4.	Explain the Solution Details

•	Which rules do you set for each NSG in the network?
 
There were rules on the Network security groups to allow traffic through the load balancer using source and destination ports and the http port 


I configured  a rule to allow ssh from my personal IP to the virtual networks by setting the source IP address to 71.17.51.161 and the destination to virtual networks. 

I configured  internal ssh (port 22)from the jumpbox by setting the source IP address to 10.0.0.4 and the destination to the virtual Network. 

I configured a rule to allow Elk-Server to be accessed by my Laptop by setting the source IP address to 71.17.51.161, the destination to the virtual network. The port was 5601 and protocol was set to any.



•	How does access to the jump box work?
To Access the jump box you ssh to the jump box with its private
•	How does access from the jump box to the web servers work?
It works by using ssh  and a private key with the webserver’s private address.

5.	Identify Advantages/Disadvantages of the Solution

•	Does your solution scale?
                       Yes the cloud solution is very scalable
•	Is there a better solution than a jump box?
Jump box is effective but this approach can also expose organizations to various risks. If a malicious user breaches the perimeter, they could traverse through the organization’s networks and resources with relative ease. zero trust security, in which all network traffic is untrusted by default is an even better option
-	What are the disadvantages of implementing a VPN that kept you from doing it this time?
●	They require an in-depth understanding of public network security issues and proper deployment options.
●	Availability and performance depends on factors largely outside of their control.
●	VPNs require accommodation of protocols other than IP and existing internal network technology.

- What are the advantages of a VPN?
●	A VPN protects private data
●	They potentially give remote and international locations in particular better reach and service quality.
●	VPNs can help avoid data-throttling
 
•	When is it appropriate to use a VPN?
It is appropriate to use VPN when you want to separate your traffic from the internet traffic that is you do not want to expose your network through the internet

