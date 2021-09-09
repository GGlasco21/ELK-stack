[README.md.txt](https://github.com/GGlasco21/ELK-stack/files/7139942/README.md.txt)
# ELK-Stack
Introductory Project built in Azure using Ansible and an ELK stack
## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

/Users/gavenglasco/Elk-stack/Diagrams/Cloud_Infrastructure.drawio


These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the YAML_Playbook_09:07:21.docx file may be used to install only certain pieces of it, such as Filebeat.

  - YAML_Playbook_09:07:21.docx
This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the Damn Vulnerable Web Application.

Load balancing ensures that the application will be highly resilient, in addition to restricting unauthorized users to the network.
A load balancer will protect the network from any DDoS attacks, it is placed in front of the Firewall as the first line of defense. Using a jump box allows the host to connect directly to a web a machine via the SSH protocol.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the performance and system logs.
- Filebeat will watch for log data in any location the creator specifies and has the log information sent to Kibana.
- Metricbeat will record the performance of the VMs such as the CPU and RAM usage of each individual machine. Sending this information back to Kibana will allows the user to scale up if they see the VMs reaching their maximum. 

The configuration details of each machine may be found below.
 
| Name     | Function | IP Address | Operating System |
|----------|----------|------------|------------------|
| JBP      | Gateway  | 10.0.0.5   | Linux            |
| Web-1    | DVWA     | 10.0.0.6   | MacOS            |
| Web-2    | DVWA     | 10.0.0.7   | MacOS            |
| Web-3    | DVWA     | 10.0.0.8   | MacOS            |
| ELK      | Kibana   | 10.1.0.5   | MacOS            |


### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jump Box Provisioner machine can accept connections from the Internet. Access to this machine is only allowed from the following IP address:
- Local Workstation 72.195.227.128

Machines within the network can only be accessed by local workstation.
- The local workstation of 72.195.227.128 was allowed to connect to the Elk server.

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| Jump Box | Yes                 | 72.195.227.128       |
| Web-1         | No                    | 10.0.0.5                     |
| Web-2         | No                    | 10.0.0.5                     |
| Web-3         | No                    | 10.0.0.5                     |
| ELK-Server    | Yes                   | 72.195.227.128               |          


### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
- Using Ansible greatly increases efficacy when you have the master YAML file saved you can create a new VM in a matter of minutes. 

The playbook implements the following tasks:
- Installing the latest version of docker.io.
- Installing pip3 and python so they can be used to read python.
- launch docker containers with an image.

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

/Users/gavenglasco/ELK-stack/Ansible/sudo_docker_ps_screenshot

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- Web-1: 10.0.0.6 
- Web-2: 10.0.0.7
- Web-3: 10.0.0.8

We have installed the following Beats on these machines:
- All three of these machines have Filebeat and Metricbeat monitoring there files and machine matrics.

These Beats allow us to collect the following information from each machine:
- Filebeat will collect data about the file systems from all three machines. Specifically, it will look at the systems logs and have those displayed through Kibana. Metricbeat collects machine metrics, such as up time. It will also give a live feed of the CPU and RAM usage of each individual VM.

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the ansible.cfg file to /etc/ansible directory.
- Update the ansible.cfg to include the IP addresses of the web machines and the remote user username. 
- Run the playbook and navigate to http://(IP_of_the_load_balancer)/login.php to check that the installation worked as expected.

- The my-playbook.yml is the playbook to copy to the /etc/ansible directory. 
- Update the ansible.cfg file to have the playbook run on a specific machine. To specify which machine to install the ELK server or Filebeat go to the corresponding configuration file. 
- Navigate to http://(public_IP_of_the_ELK_server):5601/app/kibana in order to check that the ELK server is running properly.

To run any of the playbooks use the command “ansible-playbook nameoftheplaybook.yml” If new VMs are added simply update/remove IP addresses from the ansible.cfg file.
