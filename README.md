## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.


![AWS ELK_STACK_Deployment](https://user-images.githubusercontent.com/85464020/135786249-e7557f36-03d7-47db-9a56-a45223263936.png)


These files have been tested and used to generate a live ELK deployment on AWS. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the ansible file may be used to install only certain pieces of it, such as Filebeat.

  Project-Elk-Stack/Ansible/

This document contains the following details:
- Description of the Topologu
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of Kibana

Load balancing ensures that the application will be highly available to customer, in addition to restricting attacks to the network.
If a server is not working or needs to be updated, services will still continue.  The advantage of using a jump box in this network is that only the jump box can access our virtual network via SSH.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the _____ and system _____.
- Filebeat monitors the log files or locations specified, collects log events, and sends this info to either Elastisearch or Logstash for further ediding
- Metricbeat is a user friendly, efficient, and reliable metric shipper for monitoring our system and the processes that are running on it.

The configuration details of each machine may be found below:


| Name           | Function   | IP Address   | Operating System |
|----------------|------------|--------------|------------------|
| JumpBox        | Gateway    | 172.31.1.45  | Linux            |
| Webserver      | Server     | 172.31.5.79  | Linux            |
| Webserver2     | Server     | 172.31.36.208| Linux            |
| ELKSERVER      | Monitoring | 172.31.36.69 | Ubuntu           |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the JumpBox machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
3.137.171.248

Machines within the network can only be accessed by the secure JumpBox
The twom machines linked to our ELK server are Webserver (172.31.5.790 and Webserver2 (172.31.36.208)

A summary of the access policies in place can be found in the table below.

| Name      | Publicly Accessible | Allowed IP Addresses         |
|-----------|---------------------|------------------------------|
| Jump Box  | Yes                 | 3.137.171.248 and 172.31.1.45|
| Webserver | No                  | 172.31.5.79                  |
| Webserver2| No                  | 172.31.36.208                |
| ELKSERVER | No                  | 172.31.36.69                 |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because it saved a lot of time and manpower implementing the machine step by step; which would have taken hours.  In addition we can revent easily overlooked vulnerabilities by automating.


The playbook implements the following tasks:
- installs docker.io
- Increases virtual memory
- Installs python3-pip
- Installs docker via pip
- Downloads and launces a docker web container that establishes what ports will be in use.


The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![ELKCAPTURE](https://user-images.githubusercontent.com/85464020/135788507-34ab59b9-256b-4995-a783-dead9d27b0d4.PNG)


### Target Machines & Beats
This ELK server is configured to monitor the following machines:
| Name      | IP Address   |
|-----------|--------------|
| Webserver | 172.31.5.79  |
| Webserver2| 172.31.36.208|
| ELKSERVER | 172.31.36.69 |


We have installed the following Beats on these machines:
- Filebeat
- Metricbeat
| Name      | IP Address   |
|-----------|--------------|
| Webserver | 172.31.5.79  |
| Webserver2| 172.31.36.208|
| ELKSERVER | 18.220.26.203|


These Beats allow us to collect the following information from each machine:
-Filebeat is a lightweight shipper that ships with modules for enhanced observability adn security data sources that greatly simplify he collection, parsinf and visualization of common log format down to a single comman.  It then fowards this info to either Elasticsearch or Logstash for indexing.
-Metricbeat is also a lightweight shipper that will periodically ollect metrics from the appropiate OS and from services that are currently running on hte server.

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the playbook yaml file to the Ansible Directory.
- Update the host file to include our webservers and the ELK server
- Run the playbook, and navigate to Kibana to check that the installation worked as expected.  You would use the public IP from your elk server 18.220.26.203

_TODO: Answer the following questions to fill in the blanks:_
- You have playbooks for elk(install-elk.yaml); filebeat (filebeat-playbook.yaml) and metricbeat (metricbeat.yaml) that are coipied in the Jumpbox Ansible machine.
- You have to update the hosts file in order to run the playbook on a specific machine.  Inside the host file you have to change the ip addresses specified under webservers.  Then add a line for elservers with the ELK's IP. In order to specify where you want your various deployments to go to make sure you have the proper usernmae under the ansible.config file.  In our case the user name is ec2-user for our webservers and ubuntu for our ELK servers.
- _Which URL do you navigate to in order to check that the ELK server is running?
- http://18.220.26.203:5601/app/kibana

These are the commands in order to run our playbooks and provide an update for our ELK server:
 ansible-playbook -i hosts elk-setup.yaml --key-file Cyber-Key.pem
 ansible-playbook -i hosts ubuntu-update.yaml --key-file Cyber-Key.pem
 ansible-playbook -i hosts filebeat-playbook.yml --key-file Cyber-Key.pem
 ansible-playbook -i hosts metricbeat.yml --key-file Cyber-Key.pem
