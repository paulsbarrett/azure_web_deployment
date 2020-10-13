## Automated ELK Stack Deployment
The files in this repository were used to configure the network depicted below.
  
  
  [Azure Topology including ELK deployment] (file:///C:\Users\paulb\Downloads\Week-13-ELK-Stack-Project_Resources_README\README\Images\azure_topology_including_ELK_deployment.png)
  
These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the elk-install.yaml file may be used to install only certain pieces of it, such as Filebeat.
  * elk-install.yaml
This document contains the following details:
- Description of the Topologu
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build
### Description of the Topology
The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.
Load balancing ensures that the application will be highly distributed, in addition to restricting access to the network.
   Load Balancers makes sure that each machine specified by the load balancer, receives a distributed amount of traffic. This means that the system is more accessible by lessening the chance of a DDoS attack, and generally, ensuring that no single machine is overwhelmed with traffic.
Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the system and system logs.
   What does Filebeat watch for? Filebeat monitors log files and collects log events, and forwards them to either elasticsearch or logstash for indexing.
   What does Metricbeat record? Metricbeat takes the metrics and statistics that it colects and sends them to Elasticsearch or Logstash. It helps to monitor servers by collecting metrics from the services running on the server.
The configuration details of each machine may be found below.

| Name       | Function   | IP Address | Operating System |
|------------|------------|------------|------------------|
| Jump Box   | Gateway    | 10.0.0.4   | Linux            |
| Web-1      | Web Server | 10.0.0.11  | Linux            |
| Web-2      | Web Server | 10.0.0.12  | Linux            |
| Web-3      | Web Server | 10.0.0.13  | Linux            |
| Elk-Server | Log Server | 10.1.0.4   | Linux            |

### Access Policies
The machines on the internal network are not exposed to the public Internet. 
Only the load balancer can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
   * My personal laptop, IP address allocated by my ISP
   * The Load Balancer, Public IP address of 20.188.243.120
Machines within the network can only be accessed by SSH via the Jump Box provisioner.
   * The Jump Box provisioner has a public IP address of 52.187.202.203 and a private IP address of 10.0.0.4
A summary of the access policies in place can be found in the table below.
| Name          | Publicly Accessible | Allowed IP Addresses                                      |
|---------------|---------------------|-----------------------------------------------------------|
| Jump Box      | Yes                 | My ISP allocated ISP                                      |
| Load Balancer | Yes                 | 52.187.202.203                                            |
| Web-1         | No                  | 10.0.0.4                                                  |
| Web-2         | No                  | 10.0.0.4                                                  |
| Web-3         | No                  | 10.0.0.4                                                  |
| Elk-Server    | No                  | 20.188.243.120, 10.0.0.4, 10.0.0.11, 10.0.0.12, 10.0.0.13 | can the JB directly SSH?
### Elk Configuration
Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because the configuration can be automated and run on every machine within your network, that is specified in the .yml file. This way, you can role out to one machine, or dozens of machines. The process can be done individually by logging in to each machine (provided you have ssh access), however this is time consuming.
The playbook implements the following tasks:
- it installs docker, via the install-elk.yml file
- it increases the virtual memory allocation of the Elk-server
- it downloads and launches the docker container
The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.
![TODO: Update the path with the name of your screenshot of docker ps output](Images/docker_ps_output.png)
### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- _TODO: List the IP addresses of the machines you are monitoring_
We have installed the following Beats on these machines:
- we installed FileBeat and MetricBeat onto the Elk-server
These Beats allow us to collect the following information from each machine:
- _TODO: In 1-2 sentences, explain what kind of data each beat collects, and provide 1 example of what you expect to see. E.g., `Winlogbeat` collects Windows logs, which we use to track user logon events, etc._
### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 
SSH into the control node and follow the steps below:
- Copy the install-elk.yml file to the /etc/ansible/ folder on the ansible container machine.
- Update the install-elk.yml file to include the machines that you want to have the playbook action - in this case, the machine is Elk-server.
- Update the hosts file found in /etc/ansible/hosts/ folder on the ansible container machine. check!
- Run the playbook, and navigate to your Elk-server to check that the installation worked as expected. From your web browser, navigate to http
_TODO: Answer the following questions to fill in the blanks:_
- _Which file is the playbook? Where do you copy it?_
- _Which file do you update to make Ansible run the playbook on a specific machine? How do I specify which machine to install the ELK server on versus which to install Filebeat on?_
- _Which URL do you navigate to in order to check that the ELK server is running? To check that the Elk server is running, ssh to
_As a **Bonus**, provide the specific commands the user will need to run to download the playbook, update the files, etc._





From the command line, run ssh azadmin@10.1.0.4
