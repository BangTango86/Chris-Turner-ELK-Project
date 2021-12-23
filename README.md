
## Automated ELK Stack Deployment
The files in this repository were used to configure the network depicted below.
 ![Chris_Turner_ELK_Project_Diagram](https://user-images.githubusercontent.com/90289282/147292784-8b351882-958f-4a37-8c10-15eb6d9b1a38.png)




Click [Here](https://github.com/BangTango86/Chris-Turner-ELK-Project/blob/main/Diagrams/Chris_Turner_ELK_Project_Diagram.png) to go to my diagarm.


These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the configuration .yml files may be used to install only certain pieces of it, such as Filebeat.

Click [Here](https://github.com/BangTango86/Chris-Turner-ELK-Project/blob/main/Linux/filebeat-playbook.yml) to view filebeat-playbook.yml

Click [Here](https://github.com/BangTango86/Chris-Turner-ELK-Project/blob/main/Linux/metricbeat-playbook.yml) to view metricbeat-playbook.yml


This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build

### Description of the Topology
The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.
Load balancing ensures that the application will be highly available and responsive, in addition to restricting unauthorized access to the network.

Load Balancers protect the system against denial of service attacks (DDoS) because the load balancer analyzes all traffic coming in and determines which server to send the traffic to. This prevents one server from getting overloaded with traffic because the load balancer allows traffic to be distributed evenly among the servers that are connected to it.  Load balancers often have a health probe that periodically checks that the connected machines are working properly before sending traffic. If it isn't, the load balancer will divert traffic from the malfunctioning server until the issue is resolved. 

A jump box limits the access that the public has to your virtual network because in order to access the other virtual machines inside the network, an individual needs the private IPs of the webservers in order to connect to them. A jumpbox allows greater control over access to a virtual network and its contents.


Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the logs, system files and traffic.

Filebeat generates and organizes log files.  Then looks for changes in the files and when they occured.

Metricbeat records metrics from the Operating system and services running on the server. By using Logstash or Elasticsearch, you can visualize the metrics and statistics that Metricbeat generates from the OS and running services.


The configuration details of each machine may be found below.

| Name     | Function               | IP           | OS    |
|----------|------------------------|--------------|-------|
| JumpBox  | Gateway Docker/Ansible | 40.86.81.155 | Linux |
| ELK VM   | ELK Stack Server       | 52.159.90.6  | Linux |
| Web-1 VM | Webserver              | 10.1.0.5     | Linux |
| Web-2 VM | Webserver              | 10.1.0.6     | Linux |

_Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.


### Access Policies
The machines on the internal network are not exposed to the public Internet. 
Only the JumpBox machine can accept connections from the Internet. Access to this machine is only allowed from the following IP address.  

162.220.68.136

Machines within the network can only be accessed by the JumpBoxProvisioner VM.

Which machine did you allow to access your ELK VM?  The JumpBoxProvisioner VM 
What was its IP address? 40.86.81.155

A summary of the access policies in place can be found in the table below.

| Name        | Publicly Accessible | Port | Allowed IP Addresses |
|-------------|---------------------|------|----------------------|
| JumpBox     | Yes                 |      | 162.220.68.136       |
| ELK VM      | Yes                 | 5601 | 162.220.68.136       |
| Web-1 VM    | No                  |      | 10.0.0.4             |
| Web-2 VM    | No                  |      | 10.0.0.4             |
| Red-Team-LB | Yes                 | 80   | 162.220.68.136       |



### Elk Configuration
Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...

By using an Ansible playbook I was able to automate the configuration and installation of the ELK Stack Server.  The playbook eliminates the possability of human error during installation.  It also makes the procedure easily replicatable across the network to save time and money.

The playbook implements the following tasks:
- _TODO: In 3-5 bullets, explain the steps of the ELK installation play. E.g., install Docker; download image; etc._
- ...
- ...
The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.
![TODO: Update the path with the name of your screenshot of docker ps output](Images/docker_ps_output.png)
### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- _TODO: List the IP addresses of the machines you are monitoring_
We have installed the following Beats on these machines:
- _TODO: Specify which Beats you successfully installed_
These Beats allow us to collect the following information from each machine:
- _TODO: In 1-2 sentences, explain what kind of data each beat collects, and provide 1 example of what you expect to see. E.g., `Winlogbeat` collects Windows logs, which we use to track user logon events, etc._
### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 
SSH into the control node and follow the steps below:
- Copy the _____ file to _____.
- Update the _____ file to include...
- Run the playbook, and navigate to ____ to check that the installation worked as expected.
_TODO: Answer the following questions to fill in the blanks:_
- _Which file is the playbook? Where do you copy it?_
- _Which file do you update to make Ansible run the playbook on a specific machine? How do I specify which machine to install the ELK server on versus which to install Filebeat on?_
- _Which URL do you navigate to in order to check that the ELK server is running?
_As a **Bonus**, provide the specific commands the user will need to run to download the playbook, update the files, etc._
