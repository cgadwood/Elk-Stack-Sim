## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.



These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the below file may be used to install only certain pieces of it, such as Filebeat.

 - /etc/ansible/install-elk.yml

This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly protected from DDoS attacks, in addition to restricting access to the network by creating the jumpbox portal where all admins must first connect to before doing any administrative work.


Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the log file systems for the VMs and watch system metrics (SSH logins, sudo usage).


The configuration details of each machine may be found below.


| Name     | Function | IP Address | Operating System |
|----------|----------|------------|------------------|
| Jump Box | Gateway   | 10.0.0.1   | Linux            |
|  Web 1   | Server    | 10.0.0.5   | Linux            |
|  Web 2   | Server    | 10.0.0.6   | Linux            |
|  Elk     | Montioring| 10.1.0.4   | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the jump-box-provisioner machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:

-65.28.82.148- Home IP address 

Machines within the network can only be accessed by my personal vm, withe the IP address of:
Jump box IP: 10.0.0.4 and local VM IP: 65.28.82.148.


A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses  |
|----------|---------------------|---------------------- |
| Jump Box |  Yes                | 65.28.82.148          |
| Web 1    |  No                 | 10.0.0.4              |
| Web 2    |  No                 | 10.0.0.4              |
| Elk      |  No                 | 10.0.0.4, 65.28.82.148|
### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because it allows you save time by automating these tasks. This will allow more time to be freed up to focus on more time consuming tasks.  

We first installed "Docker" on the VM, which is how we can download our Elk container and maintain it.

In order to get to the playbook for installing ELK, First you SSh into the jump box, the run the playbook with the command "ansible-playbook install_elk.yml elk"  

This playbook will: 

- Install docker.io, then install pip3, then install Docker python module
- Create a "play" to use more memory in order for the files to be stored.
- The final "play" should be to launch and download elk container, making sure to add the published ports. 

See "ELK playbook" file for full playbook

The screenshot labeled "Docker PS" in the screenshot folder displays the result of running `docker ps` after successfully configuring the ELK instance.


### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- 10.0.0.5 - Web-1
- 10.0.0.6 - Web-2

We have installed the following Beats on these machines:
- Metricbeat
- Filebeat

These Beats allow us to collect the following information from each machine:
- Metricbeat watches for changes in the system metrics, such as SSH login attempts. We can also use this to dectect sudo usage, such as failed attempts or usage escalation.

- Filebeat watches for changes in the filesystem. It's main purpose is to collect log events for log files or locations and sends them to Elasticsearch.

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 


SSH into the control node (jumpbox) and follow the steps below:

 -Copy the playbooks files to etc/ansible/.
 -Update the host file to include IP addresses for the servers and the ports
 
 -Run the playbook, the command to check to see if it was installed correctly
   
    -Install-elk.yml and location: /etc/ansible/isntall-elk.yml
   
    -Edit host file to add servers (web and elk) ip addresses
   
-The URL in order to check to see if your ELK server is running is: http:// (public IP of ELK VM):5601/app/kibana

        


