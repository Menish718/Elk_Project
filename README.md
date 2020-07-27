# Elk_Project
Elk Project with ansible
## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![RedTeam Architecture.drawio](https://drive.google.com/file/d/1za-f8II-_IwPOhgblL4Le3qeXshRDdte/view?usp=sharing)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the .YML file may be used to install only certain pieces of it, such as Filebeat.

Enter the playbook file. ansibleplaybook.yml

This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly stable and redundant, in addition to restricting DDoS to the network.
-What aspect of security do load balancers protect? 
         Load balancers provide protection when one of the VMs are down.

What is the advantage of a jump box? 
  The advantage of a jump box is to allow users access to computers in different environments.  It controls access to the other machines by allowing connections from specific IP   addresses and forwarding to those machines.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the data and system users.
- What does Filebeat watch for? 
         Collects data about filesystem

- What does Metricbeat record?
         Collects machine metrics such as uptime.

The configuration details of each machine may be found below.


| Name     | Function | IP Address | Operating System |
|----------|----------|------------|------------------|

| Jump Box - RedTeamVM | Gateway  | 10.0.0.5   | Linux  |
| DVWA-VM1 |  Web Application  |   Dynamic Public IP address / Private IP – 10.0.0.6  |   Linux  |
| DVWA-W2  |    Web Application   |   Dynamic Public IP address / Private IP – 10.0.0.8     |  Linux  
| ELK Server |    log searching and managing data|   Public IP address – 13.92.44.46/ Private IP – 10.0.0.8  |  Linux  |


### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the ELK Server machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
-Add whitelisted IP addresses - Public IP addresses for DVWA1 & DVWA2

Machines within the network can only be accessed by RedTeamVM JumpBox

- Which machine did you allow to access your ELK VM? What was its IP address? My personal network – 96.246.26.226

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| Jump Box - RedTeamVM | Yes  | 40.118.146.223    |
|  DWVA1    |    Yes    |    Dynamic IP   |
|   DWVA2    |    Yes   |    Dynamic IP   |


### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
- What is the main advantage of automating configuration with Ansible?
         Ansible is fast and performs all functions over SSH and doesn't require agent installation. The main advantage is Ansible can be run from the command line without the use of configuration files for simple tasks.

The playbook implements the following tasks:
- In 3-5 bullets, explain the steps of the ELK installation play. E.g., install Docker; download image; etc._
1.	Create a new VM. Deploy a new VM into the network. This VM will host the ELK server.
2.	Download and configure the container. Download and configure the elk-docker container onto this new VM.
3.	Launch and expose the container. Launch the elk-docker container to start the ELK server.
4.	Implement identity and access management. Configure your preexisting security group so you can connect to ELK via HTTP, and view it through the browser.


The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

(Images/docker_ps_output.png)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- List the IP addresses of the machines you are monitoring:
         DVWA-VM1
         DVWA_VM2


We have installed the following Beats on these machines:
- Specify which Beats you successfully installed - Filebeat & Metricbeat

These Beats allow us to collect the following information from each machine:
- In 1-2 sentences, explain what kind of data each beat collects, and provide 1 example of what you expect to see. E.g., `Winlogbeat` collects Windows logs, which we use to track user logon events, etc._
         Filebeat monitors the log files or locations that you specify, collects log events, and forwards them either to Elasticsearch or Logstash for indexing.
         Metricbeat collect metrics from the operating system and from services running on the server.


### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the Debian file to playbook.yml.
- Update the hosts file to include webserver private IP addresses and elkserver IP file to include...
- Run the playbook, and navigate to curl localhost/setup.php to check that the installation worked as expected.

Answer the following questions to fill in the blanks:_
- _Which file is the playbook? Filebeat-playbook.yml & metrcibeat-playbook.yml 
   Where do you copy it?  /ect/ansible/
- _Which file do you update to make Ansible run the playbook on a specific machine? Host file 
   How do I specify which machine to install the ELK server on versus which to install Filebeat on? - filebeat.yml 
- _Which URL do you navigate to in order to check that the ELK server is running? http://[your.VM.IP]:5601.(ELK server IP)

_As a **Bonus**, provide the specific commands the user will need to run to download the playbook, update the files, etc.

ssh sysadmin@(redteamVM IP)
sudo docker container list -a
sudo docker start quirky_noether
sudo docker attach quirky_noether

root: cd /etc/ansible/

sudo nano hosts file
sudo nano +1106 filebeat.yml
sudo nano +1806 filebeat.yml
sudo nano +62 metricbeat.yml
sudo nano +96 metricbeat.yml
sudo ansible-playbook filebeat.yml
sudo ansible-playbook filebeat-playbook.yml
sudo ansible-playbook metricbeat.yml
sudo ansible-playbook metricbeat-playbook.yml

http://13.92.44.46:5601/ - access Kibana
