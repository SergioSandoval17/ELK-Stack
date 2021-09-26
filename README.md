## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![](diagram/ELK_Diagram.png)![ELK_Diagram](https://user-images.githubusercontent.com/84549277/134789794-b1a0a1db-6ad7-45ce-b782-40dd822479f5.png)


These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the playbook file may be used to install only certain pieces of it, such as Filebeat.

  - elkplaybook-yml.txt
  - Filebeat-playbook.yml.txt
  - playbook.yml.txt

This document contains the following details:
- Description of the Topologu
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly redundant, in addition to restricting traffic to the network.
- Load Balancers will protect servers by moving data more efficiently, decrease the chance of a potential DDoS attack and can prevent server overloads.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the files and system metrics.
- Filebeat monitors the log files or locations that you specifiy, collects log events and forwards them either to Elasticsearch or Logstash for indexing.
- Metricbeat takes the metrics and statistics that it collects and ships them to the output that you specify, such as Elasticsearch or Logstash.

The configuration details of each machine may be found below.

| Name     | Function    | IP Address | Operating System |
|----------|-------------|------------|------------------|
| Jump Box | Gateway     | 10.0.0.4   | Linux            |
| Web-1 VM | DVMA Server | 10.0.0.5   | Ubuntu           |
| Web-2 VM | DVMA Server | 10.0.0.6   | Ubuntu           |
| Web-3 VM | DVMA Server | 10.0.0.7   | Ubuntu           |
| ELK VM   | ELK Stack   | 10.1.0.5   | Ubuntu           |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the JumpBox machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- My Workstation public IPv4 address. Confidential.

Machines within the network can only be accessed by The Jump Box.
- The ELK VM accepts public connections also but only from my IP address of my workstation, which is confidential.

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses    |
|----------|---------------------|-------------------------|
| Jump Box | Yes                 | Confidential            |
| Web-1 VM | No                  | 10.0.0.4                |
| Web-2 VM | No                  | 10.0.0.4                |
| Web-3 VM | No                  | 10.0.0.4                |
| ELK-VM   | Yes                 | Confidential & 10.0.0.4 |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because you will be able to configure multiple containers with ansible. Saving time and increases efficiency.

The playbook implements the following tasks:
- Use Docker to configure ELK stack
- Increase and use more memory
- Install Docker.io
- Install Python3-pip
- Install Python Docker Module
- Download and launch a Docker Web Container

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![](linux/Docker_PS.png)![Docker_PS](https://user-images.githubusercontent.com/84549277/134789806-25597f33-3b13-4317-be2d-77308e21fde5.png)


### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- Web-1 VM 10.0.0.5
- Web-2 VM 10.0.0.6
- Web-3 VM 10.0.0.7

We have installed the following Beats on these machines:
- Filebeat
- Metricbeat

These Beats allow us to collect the following information from each machine:
- Filebeat will allow you to collect log files or location where you will be able to see in a graph all the traffic to the server, unique connections, type of errors, and sources of IP address and geolocation.

- Metricbeat collects and analyzes metrics of applications and will show inbound and outbound traffic, CPU usage, Memory usage, and Disk usage.

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the elkplaybook.yml.txt , Filebeat-playbook.yml.txt , and playbook.yml.txt file to /etc/ansible.
- Update the etc/ansible/hosts file to include IP addresses of your VMs and group name.
- Run the playbook, and navigate to http://[Your.VM.Public.IP]:5601/app/kibana to check that the installation worked as expected.

Curl commands to download the appropriate yaml files

- curl https://github.com/SergioSandoval17/ELK-Stack/blob/main/ansible/playbook.yml.txt
- curl https://github.com/SergioSandoval17/ELK-Stack/blob/main/ansible/Filebeat-playbook.yml.txt
- curl https://github.com/SergioSandoval17/ELK-Stack/blob/main/ansible/elkplaybook.yml.txt

Commands to run Playbooks
- ansible-playbook playbook.yml
- ansible-playbook Filebeat-playbook.yml
- ansible-playbook elkplaybook.yml
