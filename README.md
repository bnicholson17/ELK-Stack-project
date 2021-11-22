# ELK-Stack-project
cyber security ELK-Stack project

    ## Automated ELK Stack Deployment
This document contains the following details:


- Description of the Topologu
- Access Policies
- ELK Configuration
- Beats in Use
- Machines Being Monitored
- How to Use the Ansible Build

### Description of the Topology

The files in this repository were used to configure the network depicted below.

![Diagram](https://github.com/bnicholson17/ELK-Stack-project/blob/76d13076342bf09a10d6cfa82616cc7a4f483b4e/Network%20Diagram/Network_diagram.PNG)

https://github.com/bnicholson17/ELK-Stack-project/blob/76d13076342bf09a10d6cfa82616cc7a4f483b4e/Network%20Diagram/Network_diagram.PNG

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly available, in addition to restricting inbound access to the network. Load ballancers 
ensure that web traffic will be processed and shared by all 3 vulnerable web servers. The Access controls in place ensure that only authorized 
users are able to connect.
Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the file systems of the VMs on the network 
as well as watching system metrics.
- Filebeat watches and monitors log files and collects log events.
- Metricbeat collects metrics and statistics. Metricbeat allows you to monitor services and system usage on your servers. 

The configuration details of each machine may be found below.

| Name           | Function   | IP Address | Operating System |
|----------------- |-----------------|--------------|----------|
| Jump Box    | Gateway     | 10.0.0.4   | Linux  |
| Web-1         | Web Server | 10.0.0.5   | Linux  |
| Web-2         | Web Server | 10.0.0.6   | Linux  |
| Web-3         | Web Server | 10.0.0.9   | Linux  |
| ELK-Server |Monitoring    | 10.1.0.5   | Linux  |

### Access Policies

The web servers on the internal network are not publicly accessable. They can only be accessed via the ansible container installed on the jumpbox via ssh.
Only the JumpBox via port 22 and the ELK server via port 5601 are publicly accessable, although inbound security rules ensure only my private IP has access. 

A summary of the access policies in place can be found in the table below.

| Name           | Publicly Accessible | Allowed IP Address |
|------------------|---------------------------|---------------------------|
| Jump Box     |         YES                | 14.2.53.191            |
| Web-1          |          NO                 | 10.0.0.4                  |
| Web-2          |          NO                 | 10.0.0.4                  |
| Web-3          |          NO                 | 10.0.0.4                  |
| ELK-Server  |         YES                | 14.2.53.191            |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. This was advantageious as no configuration was performed manually, which allowed me to save a lot
of time configuring and deploying the ansible playbooks. 
The playbook implements the following tasks:

-  Install Docker (eg. docker.io)  
-  Install python3-pip
-  Install Docker python module  pip
-  download and launch a docker (sebp/elk:761sebp/elk:761 )
-  enable service docker on boot

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

https://github.com/bnicholson17/ELK-Stack-project/blob/46d43788de748132acb32aa5d374afc48c481eab/Images/docker-ps.PNG

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- web-1 10.0.0.5
- web-2 10.0.0.6
- web-3 10.0.0.9

We have installed the following Beats on these machines:
- Metricbeat
- Filebeat

These Beats allow us to collect the following information from each machine:

- Filebeats captures and monitor log files that you specify, and forwards them either to Elasticsearch or Logstash for indexing. For example capturing syslogs can allow us to monitor
sudo commands, SSH logins or new users and groups created. 

- Metricbeats allow you to collect metrics from the operating systems and services running on the server your'e monitoring. For example you can monitor CPU usage and or RAM statistics. 

### Using the Playbook
In order to use the Playbooks we have created, you first need to ssh into your Ansible control node, which in this case is our JumpBox ( ssh RedAdmin@52.189.250.82 )

You'll then need to follow the below steps ;
- start and attach your ansible container ( sudo docker start [container name] ) ( sudo docker attach [container name] )
- Update the hosts file to specify which VM's to run the playbook on (nano /etc/ansible/hosts) you should list the IP's of the VM's you wish to run the playbooks on. 
- run the playbooks eg . $ ansible-playbook install_elk.yml elk
                                       $ ansible-playbook install_filebeat.yml webservers
                                       $ ansible-playbook install_metricbeat.yml webservers
																			
In this instance we have run the install elk , install filebe

See example of Kibana's home screen https://github.com/bnicholson17/ELK-Stack-project/blob/46d43788de748132acb32aa5d374afc48c481eab/Kabana/Kibana_Home.PNG


- _Which file is the playbook? Where do you copy it?_
- _Which file do you update to make Ansible run the playbook on a specific machine? How do I specify which machine to install the ELK server on versus which to install Filebeat on?_
- _Which URL do you navigate to in order to check that the ELK server is running?

_As a **Bonus**, provide the specific commands the user will need to run to download the playbook, update the files, etc._
    

