
## Automated ELK Stack Deployment
The files in this repository were used to configure the network depicted below.
 ![Chris_Turner_ELK_Project_Diagram](https://user-images.githubusercontent.com/90289282/147292784-8b351882-958f-4a37-8c10-15eb6d9b1a38.png)




Click [Here](https://github.com/BangTango86/Chris-Turner-ELK-Project/blob/main/Diagrams/Chris_Turner_ELK_Project_Diagram.png) to view my diagarm.


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
1. Install docker.io
2. Install python3-pip
3. Install Python Docker module
4. Increase the virtual memory of the ELK VM to 262144
5. D/L and launch a docker ELK container
6. Enable service docker on boot

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![Succesful_ELK](https://user-images.githubusercontent.com/90289282/147300724-4f56c54f-237c-4d50-8d89-d200002356f9.png)


Click [Here](https://github.com/BangTango86/Chris-Turner-ELK-Project/blob/main/Diagrams/Succesful_ELK.png) to view my screenshot

### Target Machines & Beats
This ELK server is configured to monitor the following machines:

List the IP addresses of the machines you are monitoring Web-1 @ 10.0.0.4 and Web-2 @ 10.0.0.5

I have installed the following Beats on these machines: Filebeat and Metricbeat

These Beats allow us to collect the following information from each machine:

Filebeat is a log data collection tool.  It monitors log files and locations that you specify.  Filebeat forwards these logs Elasticsearch or Logstash for indexing and the output can be viewed with an application like Kibana.

Metricbeat is an OS and services metrics and statistics collection tool.  It takes the collected information and sends it to applications like Elasticsearch or Logstash.  The output can be viewed in Kibana or other similar applications.

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 
SSH into the control node and follow the steps below:

Copy the filebeat-config.yml file to /etc/ansible/files.

Click [Here](https://github.com/BangTango86/Chris-Turner-ELK-Project/blob/main/Linux/filebeat-config.yml) for to view file

Update the filebeat-config.yml file to include
Line 1105 host IP (change to ELK VM private IP):9200
user name "elastic"
password "changeme"
Line 1805 setup.Kibana
"(ELK VM private IP):5601"

Run the filebeat playbook, and navigate to http://(ELK public IP):5601/app/kibana Click on "Check Data" to check that the installation worked as expected.

Which file is the playbook? filebeat-playbook.yml

Click [Here](https://github.com/BangTango86/Chris-Turner-ELK-Project/blob/main/Linux/filebeat-playbook.yml) to view filebeat-playbook.yml

Where do you copy it?

Place it in  /etc/ansible/

Which file do you update to make Ansible run the playbook on a specific machine? 

filebeat-config.yml As mentioned above.


How do I specify which machine to install the ELK server on versus which to install Filebeat on?

Copy the host file into /etc/ansible.  Nano into the host file.  Under "webservers" place your Web-1 and Web-2 VM IP's.  Then add your ELK VM IP under "elk".  Now, nano into the playbook files and near the top you can specifiy which "host" you want the playbook to run on.  Either "webservers" or "elk".


Which URL do you navigate to in order to check that the ELK server is running?

http://(ELK vm public IP):5601/app/kibana



_As a **Bonus**, provide the specific commands the user will need to run to download the playbook, update the files, etc._
