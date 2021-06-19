# Project1
Project1 repository
Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![Diagram](https://github.com/lchuber1990/Project1/blob/main/Diagrams/Diagram.JPG)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the YAML file may be used to install only certain pieces of it, such as Filebeat.

[install-elk.yml](https://github.com/lchuber1990/Project1/blob/main/Ansible/install-elk.yml)


This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build

### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.
Load balancing ensures that the application will be highly dynamic, in addition to restricting access to the network.

##### What aspect of security do load balancers protect? What is the advantage of a jump box?  
A load balancer distributes traffic across multiple servers.  This provides the user with optimal service.  Load balancers enhance the security, performance, resilience, and scalability of a website.  Many load balancers include a Web Application Firewall (WAF) that protects against incoming threats.  Load balancers also help prevent DDoS attacks. DDoS attacks try to overwhelm a server, whereas a load balancer distributes traffic which helps prevent a server from becoming overloaded.
The jump box is a virtual machine that is security hardened.  A jump box bridges 2 networks and the jump box virtual machine acts as a toll booth: all traffic must go through it before using the network.  This is beneficial because all necessary data regarding incoming traffic will be logged through the jump box.  Another advantage is that it allows you to easily turn on/off the remote desktop protocol.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the configuration and system files.

##### What does Filebeat watch for? 
Filebeat monitors log files and/or specified locations, collects log events and then sends the information to Elasticsearch or Logstash.  
##### What does Metricbeat record? 
Metricbeat records system and service metrics.  This data is then typically set up to be sent to Elasticsearch; however, it can also be set up to a messaging or queuing buffer.

The configuration details of each machine may be found below.

| Name     | Function  | IP Address | Operating System |
|----------|-----------|------------|------------------|
| Jump Box | Gateway   | 10.0.0.4   | Linux            |
| Web-1    | webserver | 10.0.0.5   | Linux            |
| Web-2    | webserver | 10.0.0.6   | Linux            |
| ELK-VM   | webserver | 10.1.0.4   | Linux            |

#### Access Policies
The machines on the internal network are not exposed to the public Internet.

##### Only the jumpbox machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
Only my IP address is whitelisted.

Machines within the network can only be accessed by the JumpBoxProvisioner.

##### Which machine did you allow to access your ELK VM? What was its IP address? 
JumpBoxProvisioner has access to my ELK_VM. The IP address to the JumpBoxProvisioner is 10.0.0.4

A summary of the access policies in place can be found in the table below.

| Name               | Publicly Accessible | Allowed IP Addresses |
|--------------------|---------------------|----------------------|
| JumpBoxProvisioner | yes                 | My IP Address        |
| ELK-VM             | SSH-No, http-Yes    | My IP Address        |
| Web-1              | No                  | My IP Address        |
| Web-2              | No                  | My IP Address        |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...

#### What is the main advantage of automating configuration with Ansible?  
The main advantage of automating configuration with Ansible is that it saves time and is consistent across all Virtual Machines associated with the playbook.  This allows for uniformity across the board.

The playbook implements the following tasks:
- Sysctl module to be able to use more memory 
- Docker_container module downloads and launches docker to the elk container and indicates which ports that ELK should run on
- Systemd Module enables service docker on boot

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.
![Diagram](https://github.com/lchuber1990/Project1/blob/main/Images/elk%20vm%20docker%20running%20elk.JPG)

### Target Machines & Beats
#### This ELK server is configured to monitor the following machines:
JumpBoxProvisioner 10.0.0.4, ELK-VM 10.1.0.4, Web-1 10.0.0.5, Web-2 10.0.0.6

#### We have installed the following Beats on these machines:
I have installed Metricbeat and filebeat to my virtual machines

#### These Beats allow us to collect the following information from each machine:
Filebeat monitors log files and/or specified locations, collects log events and then sends the information to Elasticsearch.  It will collect data such as hostname and system logs
Metricbeat records system and service metrics.  This data is then typically set up to be sent to Elasticsearch; however, it can also be set up to a messaging or queuing buffer. This provides us with operating system data such as CPU, RAM, and network usage.


### Using the Playbook
[filebeat-playbook.yml](https://github.com/lchuber1990/Project1/blob/main/Ansible/filebeat-playbook.yml)
[metricbeat-playbook.yml](https://github.com/lchuber1990/Project1/blob/main/Ansible/metricbeat-playbook.yml)
[install-elk.yml](https://github.com/lchuber1990/Project1/blob/main/Ansible/install-elk.yml)


In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned:

SSH into the control node and follow the steps below:
- Copy the .yml file to /etc/ansible directory.
- Update the hosts file to include webservers

![diagram](https://github.com/lchuber1990/Project1/blob/main/Images/Host%20file%20update.JPG)

- Run the playbook (using ansible-playbook <file>), and navigate to JumpBoxProvisioner to check that the installation worked as expected.

#### Which file is the playbook? Where do you copy it?_
Filebeat-playbook.yml and metricbeat-playbook.yml  These playbooks are copied into the /etc/ansible/roles directory.

#### Which file do you update to make Ansible run the playbook on a specific machine? How do I specify which machine to install the ELK server on versus which to install Filebeat on?
The /etc/ansible/hosts file is updated in order for Ansible to run the playbook on a specific machine.  You can determine which machine in which you would like to install the ELK server vs the Filebeat by assigning the appropriate IP addresses in the playbook.

#### Which URL do you navigate to in order to check that the ELK server is running?
http://20.56.59.99:5601/app/kibana

### As a **Bonus**, provide the specific commands the user will need to run to download the playbook, update the files, etc.
#### To install ansible playbook
  
ansible-playbook metricbeat-playbook.yml

ansible-playbook filebeat-playbook.yml

#### To download to the repository

git clone “https://github.com/lchuber1990/Project1”

#### To sync all items

git add .

git commit -m “First commit”

git push
