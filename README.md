# ELK-Stack-project
cyber security ELK-Stack project

This document contains the following details:

- Description of the Topologu
- Access Policies
- ELK Configuration
- Beats in Use
- Machines Being Monitored
- How to Use the Ansible Build

### Description of the Topology

The files in this repository were used to configure the network depicted below.

![Diagram](https://github.com/bnicholson17/ELK-Stack-project/blob/3ae29553949d05b0e857c258de5a5ee74b032d8f/Network%20Diagram/Network_diagram.PNG)



The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the Damn Vulnerable Web Application.

Load balancing ensures that the application will be highly available, in addition to restricting inbound access to the network. Load ballancers 
ensure that web traffic will be processed and shared by all 3 vulnerable web servers. The Access controls in place ensure that only authorized 
users are able to connect.
Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the file systems of the VMs on the network 
as well as watching system metrics.
- Filebeat watches and monitors log files and collects log events.
- Metricbeat collects metrics and statistics. Metricbeat allows you to monitor services and system usage on your servers. 

The configuration details of each virtual machine may be found below.

![Diagram](https://github.com/bnicholson17/ELK-Stack-project/blob/c1f33143337686c8f21d599a8e76d5d409b40cda/extra%20screenshots/VM-table.PNG)
### Access Policies

The web servers on the internal network are not publicly accessable. They can only be accessed via the ansible container installed on the jumpbox via ssh.
Only the JumpBox via port 22 and the ELK server via port 5601 are publicly accessable, although inbound security rules ensure only my private IP has access. 

In addtion to being accessable via port 5601, the ELK server can also be accessed by using ssh from the JumpBox. 

A summary of the access policies in place can be found in the table below.

![Diagram](https://github.com/bnicholson17/ELK-Stack-project/blob/49c20d7bd71cad59dfa0fb2c6696ecfa4524ac6a/extra%20screenshots/access-policy.PNG)

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. This was advantageous as no configuration was performed manually. 
Only small changes are needed from playbook to playbook which is a fantastic time saver. 

The playbook implements the following tasks:

-  Install Docker (eg. docker.io)  
-  Install python3-pip
-  Install Docker python module  pip
-  download and launch a docker (sebp/elk:761sebp/elk:761 )
-  enable service docker on boot

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![Diagram](https://github.com/bnicholson17/ELK-Stack-project/blob/46d43788de748132acb32aa5d374afc48c481eab/Images/docker-ps.PNG)

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
- start and attach your ansible container 
- $ sudo docker start [container name]  
- $ sudo docker attach [container name] 
- Update the hosts file to specify which VM's to run the playbook on. To do this use to
- $ nano /etc/ansible/hosts
- run the playbooks :
  -                                    $ ansible-playbook /etc/ansible/install_elk.yml 
  -                                    $ ansible-playbook /etc/ansible/install_filebeat.yml 
  -                                    $ ansible-playbook /etc/ansible/install_metricbeat.yml 
																			
Head to your browser and type - http://[your.VM.IP]:5601/app/kibana - to check if the playbooks have run succesfully. The webpage should appear and you should be able to use
filebeat and metric beat to capture and monitor data from your webservers. 

We should now have 3 functioning web servers, placed behind a load balancer, which we are now able to monitor using the beats we have installed.


See examples of Kibana's home screen and confirmation of filebeat and metricbeat working correctly.


![Diagram](https://github.com/bnicholson17/ELK-Stack-project/blob/46d43788de748132acb32aa5d374afc48c481eab/Kabana/Kibana_Home.PNG)

![Diagram](https://github.com/bnicholson17/ELK-Stack-project/blob/a3470454c3f4a50b3b6247f564dc0ffc21bc71cc/Kabana/CHECK_DATA_1.PNG)

![Diagram](https://github.com/bnicholson17/ELK-Stack-project/blob/a3470454c3f4a50b3b6247f564dc0ffc21bc71cc/Kabana/CHECK_DATA_2.PNG)


    

