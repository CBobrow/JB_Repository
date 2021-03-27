## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

  ![Network Diagram](https://github.com/CBobrow/JB_Repository/blob/main/ELK_Stack/Images/Network%20Diagram.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the All-in-One.yml file may be used to install only certain pieces of it, such as Filebeat.

![All-In-One.yml](https://github.com/CBobrow/JB_Repository/blob/main/ELK_Stack/Files/all-in-one.yml)

This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly available, in addition to restricting access to the network.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the log files and system services.

The configuration details of each machine may be found below.
| Name                 | Function       | External IP    | Internal IP | OS    |
|----------------------|----------------|----------------|-------------|-------|
| Jump Box Provisioner | Gateway        | 52.183.37.75   | 10.0.0.4    | Linux |
| Web1                 | DVWA Container | 52.191.161.215 | 10.0.0.5    | Linux |
| Web2                 | DVWA Container | 52.191.161.215 | 10.0.0.6    | Linux |
| Web3                 | DVWA Container | 52.191.161.215 | 10.0.0.8    | Linux |
| Load Balancer        | Load Balancing | 52.191.161.215 | N/A         | N/A   |
| ELK Server           | ELK Stack      | 104.45.237.38  | 10.1.0.4    | Linux |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Load Balancer machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
 Local computer: [Local workstation IP]

Machines within the network can only be accessed by the Jump Box Provisioner.
 Jump Box Provisioner: 52.183.37.75

A summary of the access policies in place can be found in the table below.

| Name                 | Publicly Accessible  | Allowed IP Addresses |
|----------------------|----------------------|:--------------------:|
| Jump Box Provisioner | No                   |    174.51.241.214    |
| Web1                 | No                   |     52.183.37.75     |
| Web2                 | No                   |     52.183.37.75     |
| Web3                 | No                   |     52.183.37.75     |
| Load Balancer        | Yes                  |    Local Workstation |
| ELK Server           | No                   |     52.183.37.75     |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because it saves time by cicumventing the need for individual machine configuration as well as ensures that the configuration is identical across multple machines. 

The playbook implements the following tasks:

Uses apt to install docker.io
Uses apt to install python3-pip
Uses pip to install docker module
Uses sysctl to increase virtual memory and then utlize the memory
Downloads and launches an ELK docker container
Uses systemd to ensure docker is launched on reboot

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![dockpsout](https://github.com/CBobrow/JB_Repository/blob/main/ELK_Stack/Images/elk%20container%20running.png)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:

| Name | External IP    | Internal IP |
|------|----------------|-------------|
| Web1 | 52.191.161.215 | 10.0.0.5    |
| Web2 | 52.191.161.215 | 10.0.0.6    |
| Web3 | 52.191.161.215 | 10.0.0.8    |

We have installed the following Beats on these machines:
Filebeat and Metricbeat

These Beats allow us to collect the following information from each machine:
Filebeat collects system logs and metricbeat collect system metric information from each if the target systems. 
 
### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the all-in-one.yml file to /etc/ansible/roles.
- Update the hosts file to include the IP of the machine you want the ELK-stack running on under the group [elk]
- Run the playbook, and navigate to http://[ELK-VM-External-IP]:5061 to check that the kibana installation worked as expected.

### Running the Playbook
Run the all-in-one.yml by executing `ansible-playbook all-in-one.yml`
If you wish to install only certain asecpts of the modules detailed then run `ansible-playbook [Whichever .yml file you want to install].yml
