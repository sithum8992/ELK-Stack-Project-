## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![ELK-Project - Diagram](https://user-images.githubusercontent.com/86083475/142726519-83334c53-5d1e-434c-9825-f6ca8c9a2eed.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the ansible file may be used to install only certain pieces of it, such as Filebeat.

 ELK-Stack-Project-Ansible Playbook

This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly available for customers, in addition to restricting attack to the network.
- The off-loading funtion of a load balancer defends an organization against distributed DDoS attacks. It does this by shifting attack traffic from the corporate server to a public cloud provider. 
- A jump box is a system on a network used to access  and manage devices in a separate security zone. A jump server is a hardened and monitored device that spans two dissimilar security zones and provides a controlled means of access between them.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the logs and system files.
- Filebeat monitor the log files or locations specified, collect log events, and fowards them either to Elasticsearch or Logstash for indexing.
- Metricbeat is an extreamly easy-to use, efficent and reliable metric shipper for monitoring your system and the processes running on it. 

The configuration details of each machine may be found below.


| Name     | Function | IP Address | Operating System |
|----------|----------|------------|------------------|
| Jump Box | Gateway  | 10.0.0.7   | Linux            |
| Web 1     |     Server     |    10.0.0. 5      |        Linux            |
| Web 2    |  Server        |       10.0.0.6     |        Linux            |
| ELK Server     |   Monitoring       |      10.1.0.4      |          Linux          |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jumpbox machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- 40.117.146.125

Machines within the network can only be accessed by SSH.
- Jumpbox VM - IP address : 10.0.0.7 (Private IP)

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| Jump Box |          yes     | 40.117.146.125   |
|      Web 1    |        No             |         10.0.0. 5               |
|      Web 2    |        No             |              10.0.0.6 |
|ELK Server | yes |20.96.2.46 |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
- This allows you to deploy to multiple servers using a single playbook.

The playbook implements the following tasks:
- Install docker.io
- Install python3-pip
- Install docker via pip
- Increase virtual memory
- use more memory
- Download and launch a docker elk container
- Published Ports
- Enable service docker on boot

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![ELK  yml server run](https://user-images.githubusercontent.com/86083475/142726558-586f5640-3341-4076-b0be-3b5cdef9f646.PNG)


### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- WEB1 :  10.0.0. 5  
- WEB2 :  10.0.0.6 

We have installed the following Beats on these machines:
- Filebeat
- Metricbeat

These Beats allow us to collect the following information from each machine:
- Filebeat collects data about the filesystem. 
- Metricbeat periodically collect machine's metrics from services such as Apache and prometheus. 

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the Placybook file to /etc/ansible.
- Update the configuration file to include webservers and Elk VM - Private IP
    - /etc/ansible/host should include : 
        -  [Webservers]
             - 10.0.0.5 ansible_python_interpreter=/usr/bin/python3
             - 10.0.0.6 ansible_python_interpreter=/usr/bin/python3
        - [Elk]     
             - 10.1.0.4 ansible_python_interpreter=/usr/bin/python3
    -  update the ansible.cfg
        -  remote_user = Redadmin
- Run the playbook, and navigate to Elk VM to check that the installation worked as expected.
 

 Answer the following questions to fill in the blanks:
- Which file is the playbook? Where do you copy it?
    - Elk.yml - copy to /etc/ansible
    - filebeat-playbook.yml - copt to /etc/ansible/roles
    -  metricbeat-playbook.yml - copy to /etc/ansible/roles
    
- Which file do you update to make Ansible run the playbook on a specific machine? How do I specify which machine to install the ELK server on versus which to install Filebeat on?
    -  Elk.yml - update "hosts" file  (Elk.yml playbook host mention as "elk" in order to install into Elk VM)
    -  filebeat-playbook.yml -  update filebeat-config.yml (filebeat-playbook.yml playbook host mention as "webservers" in                              order to install into WEB1 & WEB2)
    -   metricbeat-playbook.yml - update metricbeat-config.yml (metricbeat-playbook.yml playbook host mention as                                          "webservers" in order to install into WEB1 & WEB2)
- Which URL do you navigate to in order to check that the ELK server is running?
    - http://20.96.2.46:5601/app/kibana.

Appendix 1 - Configuration of ELK server & Connect kibana
https://github.com/sithum8992/ELK-Stack-Project-/tree/main/Images/Appendix%201

Appendix 2 - Configuration of filebeat on WEB1 & WEB2 and connect to filebeat system
https://github.com/sithum8992/ELK-Stack-Project-/tree/main/Images/Appendix%202

Appendix 3 - Configuration of Metricbeat on WEB1 & WEB2 and connect to Metricbeat dashboard
https://github.com/sithum8992/ELK-Stack-Project-/tree/main/Images/Appendix%203
    -







