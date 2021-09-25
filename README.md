# Elk-Stack-Project-1

## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![BW Elk Stack Project Diagram Submit JPG](https://user-images.githubusercontent.com/84944319/133934596-47d57c29-96cc-4cb4-b0c4-080f70454bcb.jpg)




These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the filebeat.yml file may be used to install only certain pieces of it, such as Filebeat.

[Elk.yaml](https://github.com/BrandonQ3/Elk-Stack-Project-1/files/7198699/Elk.txt)

[Filebeat.yaml](https://github.com/BrandonQ3/Elk-Stack-Project-1/files/7198712/Filebeat.txt)

[Metricbeat.yaml](https://github.com/BrandonQ3/Elk-Stack-Project-1/files/7198718/Metricbeat.txt)



### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the Damn Vulnerable Web Application.

Load balancers protect against DDos attacks. So if one server goes down then the load balancer redistrubtes work to other servers keeping the whole system from going down. An advantage of a jump box is that you have to connect to it first in order to do any administrative task. You can also use it to streamline maintenance of a system by only having to update the jumpbox.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the file system and system metrics.

Filebeat monitors the log files or locations that you specify, collects log events, and forwards them either to Elasticserach or Logstash for indexing.

Metricbeat helps monitor servers by collecting metrics from the system and services running on the server.


The configuration details of each machine may be found below.
_Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table.

| Name     | Function | IP Address | Operating System |
|----------|----------|------------|------------------|
| Jump Box | Gateway  | 10.0.0.4   | Linux            |
| ELK-VM      | Elk Server| 10.1.0.4   | Linux            |
| Web-1    | Server| 10.0.0.5   | Linux            |
| Web-2    | Server | 10.0.0.6   | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the jump box provisioner machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
Acces to this machine only allowd from my public IP.
Machines within the network can only be accessed by SSH.

JumpBoxProvisioner:

Public IP: 20.94.249.7

Private IP: 10.1.0.4

Which machine did you allow to access your ELK VM? Jumpbox What was its IP address? 10.0.0.4

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| Jump Box | Yes                 |  20.94.249.7        |
| ELK-VM      | No                  | 10.1.0.4             |
| Webb-1   | No                  | 10.0.0.5             |
| Webb-2   | No                  | 10.0.0.6             |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
What is the main advantage of automating configuration with Ansible? Automation for tasks that can be time consuming and tedious and its open source tool. It also deploy to multiple servers using a single playbook. The configuration has also been tested and troubleshooted.

The playbook implements the following tasks:
- Install docker.io
- pip3
- Install Docker 
- Increase virtual memory
- Download and launchs a docker elk container

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![Elk Docker](https://user-images.githubusercontent.com/84944319/133934950-3b1bf030-3aa5-4db6-b066-bbe7f42f15a1.jpg)



### Target Machines & Beats
This ELK server is configured to monitor the following machines:

Web-1 10.0.0.5 

Web-2 10.0.0.6

We have installed the following Beats on these machines:
Specify which Beats you successfully installed Filebeat and Metricbeat

![project 1 Filebeat screenshot submit](https://user-images.githubusercontent.com/84944319/133935162-320423b2-62d9-405a-904c-21cfc2c7d76c.jpg)

![project 1 Meticbeat screenshot submit](https://user-images.githubusercontent.com/84944319/133935181-25e4b2c2-080c-487f-a752-9986212dcb3f.jpg)



These Beats allow us to collect the following information from each machine:
In 1-2 sentences, explain what kind of data each beat collects, and provide 1 example of what you expect to see. E.g., `Winlogbeat` collects Windows logs, which we use to track user logon events, etc. Filebeat will collect data on system and show changes made. Metricbeat will collect the metrics and statistics and show uptime.

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the playbook file Ansible Control Node .
- Update the hosts file to include... Webserver and Elk 
- Run the playbook, and navigate to (http://ELK-VMPublicIP:5601/app/kibana#/home) to check that the installation worked as expected.

![HTTP Kibana screenshot submit](https://user-images.githubusercontent.com/84944319/133935029-e9016e6d-94bc-4816-b88f-b0bc975cca50.jpg)


Answer the following questions to fill in the blanks:
- Which file is the playbook? Where do you copy it? filebeat-playbook.yml etc/ansible/roles
- Which file do you update to make Ansible run the playbook on a specific machine? How do I specify which machine to install the ELK server on versus which to install Filebeat on? 
-  filebeat-config.yml
-  Determine which machine to install by revising the host files with IP addresses of elk/webservers and choosing which group to run in Ansible.

- Which URL do you navigate to in order to check that the ELK server is running? (https://[public IP address of Elk VM]/app/kibana)

As a **Bonus**, provide the specific commands the user will need to run to download the playbook, update the files, etc.

cd /etc/ansible

mkdir files

get clone (https://github.com/BrandonQ3/Elk-Stack-Project-1.git)

cd/Elk-Stack-Project-1/README/roles/* /etc/ansible
