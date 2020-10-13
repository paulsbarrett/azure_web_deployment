## Automated ELK Stack Deployment
The files in this repository were used to configure the network depicted below.
  
![Azure Topology including ELK deployment](https://github.com/paulsbarrett/azure_web_deployment/blob/main/screenshots/azure_topology_including_ELK_deployment.png)

**The Full Infrastructure of all Virtual Machines:**
![Full Infrastructure](https://github.com/paulsbarrett/azure_web_deployment/blob/main/screenshots/Full_Infrastructure_v2.png)  
These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the install-elk.yml file may be used to install only certain pieces of it, such as Filebeat.
  * ansible-playbook install-elk.yml
This document contains the following details:
- Description of the Topology
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
| Elk-Server    | No                  | 20.188.243.120, 10.0.0.4, 10.0.0.11, 10.0.0.12, 10.0.0.13 | 

Note that it is not possible to connect to the Elk-server directly from the Jump Box Provisioner as we have not set a public key to access.
![Jump box to Elk direct connection denied](https://github.com/paulsbarrett/azure_web_deployment/blob/main/screenshots/JB%20to%20Elk%20denied.png)

### Elk Configuration
Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because the configuration can be automated and run on every machine within your network, that is specified in the .yml file. This way, you can role out to one machine, or dozens of machines. The process can be done individually by logging in to each machine (provided you have ssh access), however this is time consuming.
The playbook implements the following tasks:
- it installs docker, via the install-elk.yml file
- it increases the virtual memory allocation of the Elk-server
- it downloads and launches the docker container
The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.
![Docker PS Output Results](https://github.com/paulsbarrett/azure_web_deployment/blob/main/screenshots/docker_ps_output.png)

The yaml file is available here: ![Config Web VM with Docker](https://github.com/paulsbarrett/azure_web_deployment/blob/main/yaml_files/deploy-dvwa-ansible.yml)

The Elk Configuration file is available here: ![Configure Elk VM with Docker](https://github.com/paulsbarrett/azure_web_deployment/blob/main/yaml_files/install-elk.yml)

### Target Machines & Beats
This ELK server is configured to monitor the following machines: Web-1, Web-2, Web-3
- The IP addresses of the machines you I am monitoring include; 10.0.0.11, 10.0.0.12, 10.0.0.13

We have installed the following Beats on these machines:
- I installed FileBeat and MetricBeat onto the Elk-server
These Beats (services) allow us to collects information from each machine, including system usage, data usage, and system metrics such as uptime and connections.
- FileBeat collects and forwards log data such as log files and log events, and forwards them to either Elasticsearch or Logstash for indexing.
- MetricBeat takes the metrics and statistics that it collects and sends them to a analytics engine such as Elasticsearch. Elasticseach can analyse and visualise the data in real time.

The FileBeat Installation and Launch playbook is available here: ![Installing and Launch Filebeat Playbook](https://github.com/paulsbarrett/azure_web_deployment/blob/main/yaml_files/filebeat-playbook.yml)

The MetricBeat Installation playbook is available here: ![Intalling MetriBeat Playbook](https://github.com/paulsbarrett/azure_web_deployment/blob/main/yaml_files/metricbeat-playbook.yml)

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 
SSH into the control node and follow the steps below:
- Copy the install-elk.yml file to the /etc/ansible/ folder on the ansible container machine.
- Update the install-elk.yml file to include the machines that you want to have the playbook action - in this case, the machine is Elk-server.
- Update the hosts file found in /etc/ansible/hosts/ folder on the ansible container machine. check!
- Run the playbook, and navigate to your Elk-server to check that the installation worked as expected. From your web browser, navigate to [Elk-serverIP]:5601/app/kibana which, in my case, was http://20.37.45.178:5601/app/kibana

- Copy the install-elk.yml playbook file to the /etc/ansible/ folder on your ansible container machine.
- On the docker container VM, navigate to /etc/ansible/ and update the hosts file with specific IPs of each VM.
- To check that the Elk server is running, from the docker container, run the following: ssh azadmin@10.1.0.4 (to connect to the Elk-server).

The Hosts file above is available here: ![Ansible Hosts file](https://github.com/paulsbarrett/azure_web_deployment/blob/main/yaml_files/hosts)

**Bonus**

![Jumpbox Successful Connection](https://github.com/paulsbarrett/azure_web_deployment/blob/main/screenshots/jumpbox_successful_connection.png)

From the command line, run ssh azadmin@10.1.0.4
sudo docker start e6c1873a57ef
sudo docker attach e6c1873a57ef
ssh azadmin@10.1.0.4 (to connect to Elk-server)
run exit to return to the docker container.
ssh azadmin@10.0.0.11 (to connect to Web-1 server)


