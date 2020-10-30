# projectelk2

## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

Diagram/Diagram.jpg

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the filebeat-playbook.yml file may be used to install only certain pieces of it, such as Filebeat.

---
- name: Filebeat
  hosts: webservers
  become: true
  tasks:
  - name: filebeat DL
    command: curl -L -O https://artifacts.elastic.co/downloads/beats/filebeat/filebeat-7.4.0-amd64.deb
  - name: filebeat install
    command: sudo dpkg -i filebeat-7.6.1-amd64.deb
  - name: copy config.yml
    copy:
      src: /etc/ansible/files/filebeat-config.yml
      dest: /etc/filebeat/filebeat.yml
  - name: enable system
    command: filebeat modules enable system
  - name: setup
    command: filebeat setup
  - name: filebeat start
    command: service filebeat start


This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be available when needed, in addition to restricting access to the network.
Load balancers are a great defense against denial of service attacks (DoS) 
The advantage of a jupmp box is so that there is one singular place that controls all the others and all users and accounts can be managed


Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the _____ and system _____.
Filebeat watches and monitors files or locations that are specified, it collects log events and sends them to Elastic search.
Metricbeat collects metrics from the operating system and from applications running on the server. It collects the statistics and send them to Elasticsearch

The configuration details of each machine may be found below.

| Name     | Function | IP Address | Operating System |
|----------|----------|------------|------------------|
| Jump Box | Gateway  | 10.0.0.8   | Linux            |
| web1     | Backup   | 10.0.0.13  | Linux            |
| web2     | Backup   | 10.0.0.14  | Linux            |
| web3     | Backup   | 10.0.0.16  | Linux            |
| ElkVM1   | Monitor  | 10.1.0.4   | Linux            |


### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jumphost machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
67.213.142.180

Machines within the network can only be accessed by the Jumphost.
Only the Jumphost can gain access to the ELKstack and its IP is 10.0.0.8

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| Jump Box | Yes                 | 67.213.142.180       |
| web1     | No                  | 10.0.0.8             |
| web1     | No                  | 10.0.0.8             |
| web1     | No                  | 10.0.0.8             |
| Elkvm1   | Yes                 | 10.0.0.8             | 


### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
The main advantage of automation is that it frees up people to be able to do other more important tasks

The playbook implements the following tasks:
- Download and install the docker container
- Configure the host file to allow new VM
- Create playbook
- Run the playbook
- Test that its all working

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

Images/Screenshot__41_.png

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
10.0.0.13
10.0.0.14
10.0.0.16

We have installed the following Beats on these machines:
Filebeat and Metricbeat

These Beats allow us to collect the following information from each machine:
Filebeat allows you to collect information on the files and locations specified and Metricbeat gathers information on the operating system and applications that are running on the server.
They both collect this information and send it to Elasticsearch.

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the filebeat-config.yml file to /etc/filebeat/filebeat.yml.
- Update the filebeat-config.yml file to include the elk machine IP 

this is on line #1106
output.elasticsearch:
hosts: ["10.1.0.4:9200"]
username: "elastic"
password: "changeme"

this is on line #1806
setup.kibana:
host: "10.1.0.4:5601"



- Run the playbook, and navigate to Filebeat installation page to check that the installation worked as expected with Step 5 Module data, Check data button.


Scripts and Files/filebeat-playbook.yml
You update the filebeat-config.yml file. You add in the private IP address of the specific machine you want.
You have to go to http://13.77.4.101:5601/app/kibana to make sure it is all working corrrectly



Bonus

https://education.github.com/git-cheat-sheet-education.pdf

This has all the commands you need if you want to run it through the command line for some reason.
I personally think its easier just using the GUI on the website
