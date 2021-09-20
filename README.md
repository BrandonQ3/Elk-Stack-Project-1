# Elk-Stack-Project-1

## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![BW Elk Stack Project Diagram Submit JPG](https://user-images.githubusercontent.com/84944319/133934596-47d57c29-96cc-4cb4-b0c4-080f70454bcb.jpg)




These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the filebeat.yml file may be used to install only certain pieces of it, such as Filebeat.

[Elk.txt](https://github.com/BrandonQ3/Elk-Stack-Project-1/files/7198699/Elk.txt)

[Filebeat.txt](https://github.com/BrandonQ3/Elk-Stack-Project-1/files/7198712/Filebeat.txt)

[Metricbeat.txt](https://github.com/BrandonQ3/Elk-Stack-Project-1/files/7198718/Metricbeat.txt)




### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly reliable, in addition to restricting access/traffic to the network.
Prevent failure caused overloading and rebalances traffic in the event of an attack. The  Jump Box is where a user can access the environmentuser connects from a single node and this is a more secure way of monitoring the environment. 

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the data and system logs.
Monitors logs and events.
Metricbeat collects metrics and statistics and sent the info to a chosen output location.

The configuration details of each machine may be found below.
_Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table.

| Name     | Function | IP Address | Operating System |
|----------|----------|------------|------------------|
| Jump Box | Gateway  | 10.0.0.4   | Linux            |
| ELK      | Elk Server| 10.1.0.4   | Linux            |
| Web-1    | Webserver| 10.0.0.5   | Linux            |
| Web-2    | Webserver | 10.0.0.6   | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the jump box provisioner machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
Acces to this machine only allowd from my public IP.
Machines within the network can only be accessed by SSH.
Which machine did you allow to access your ELK VM? Jumpbox What was its IP address? 10.0.0.4

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| Jump Box | Yes                 | My public IP         |
| ELk      | No                  | 10.1.0.4             |
| Webb-1   | No                  | 10.1.0.4             |
| Webb-2   | No                  | 10.1.0.4             |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
What is the main advantage of automating configuration with Ansible? Automation for tasks that can be time consuming and tedious and its open source tool 

The playbook implements the following tasks:
- Install docker.io
- pip3
- Install Docker 
- Increase virtual memory
- Download and launch a docker

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![Elk Docker](https://user-images.githubusercontent.com/84944319/133934950-3b1bf030-3aa5-4db6-b066-bbe7f42f15a1.jpg)



### Target Machines & Beats
This ELK server is configured to monitor the following machines:
Web-1 10.0.0.5 Web-2 10.0.0.6

We have installed the following Beats on these machines:
Specify which Beats you successfully installed Filebeat and Metricbeat

![project 1 Filebeat screenshot submit](https://user-images.githubusercontent.com/84944319/133935162-320423b2-62d9-405a-904c-21cfc2c7d76c.jpg)

![project 1 Meticbeat screenshot submit](https://user-images.githubusercontent.com/84944319/133935181-25e4b2c2-080c-487f-a752-9986212dcb3f.jpg)



These Beats allow us to collect the following information from each machine:
In 1-2 sentences, explain what kind of data each beat collects, and provide 1 example of what you expect to see. E.g., `Winlogbeat` collects Windows logs, which we use to track user logon events, etc. Filebeat Filebeat will collect data on system and show changes made. Metricbeat will collect the metrics and statistics and show uptime.

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the playbook file to roles directory.
- Update the hosts file to include... webserver, IP's and elk.
- Run the playbook, and navigate to http:// ELK-VM IP:5601/app/kibana Elto check that the installation worked as expected.

![HTTP Kibana screenshot submit](https://user-images.githubusercontent.com/84944319/133935029-e9016e6d-94bc-4816-b88f-b0bc975cca50.jpg)


Answer the following questions to fill in the blanks:
- Which file is the playbook? Where do you copy it? filebeat-playbook.yml etc/ansible/roles
- Which file do you update to make Ansible run the playbook on a specific machine? How do I specify which machine to install the ELK server on versus which to install Filebeat on?_ /etc/ansible/hosts when configuring the filebeat.yml file you need to designate the Private IP of the Elk-Server in lines of the .yml file. 
- Which URL do you navigate to in order to check that the ELK server is running? Public IP:5601

As a **Bonus**, provide the specific commands the user will need to run to download the playbook, update the files, etc._

  Filebeat
- To create the filebeat-configuration.yml file: nano filebeat-configuration.yml. For this, I used the filebeat configuration file template.

- To create the playbook: nano filebeat-playbook.yml
 ---
 - name: installing and launching filebeat
	   hosts: webservers
       become: true
       tasks:

	   - name: download filebeat deb
  	     command: curl -L -O https://artifacts.elastic.co/downloads/beats/filebeat/filebeat-7.7.1-amd64.deb

	   - name: install filebeat deb
  	     command: dpkg -i filebeat-7.7.1-amd64.deb

	   - name: drop in filebeat.yml
  	     copy:
   	       src: ./files/filebeat-configuration.yml
   	       dest: /etc/filebeat/filebeat.yml

	   - name: enable and configure system module
  	     command: filebeat modules enable system

	   - name: setup filebeat
  	     command: filebeat setup

	   - name: start filebeat service
  	    command: service filebeat start

-To run the playbook: ansible-playbook filebeat-playbook.yml

Metricbeat
- To create the metricbeat-configuration.yml file: nano metricbeat-configuration.yml.
- To create the playbool: nano metricbeat-playbook.yml
---
  - name: installing and lunching metricbeat
    hosts: webservers
    become: true
    tasks:
    
  - name: download metricbeat deb
    command: curl -L -O https://artifacts.elastic.co/downloads/beats/metricbeat/metricbeat-7.7.1-amd64.deb
    
  - name: install metricbeat deb
    command: sudo dpkg -i metricbeat-7.7.1-amd64.deb
    
  - name: drop in metricbeat.yml
    copy:
      src: /etc/ansible/roles/files/metricbeat-configuration.yml
      dest: /etc/metricbeat/metricbeat.yml
      
   - name: enable and configure system module
     command: metricbeat modules enable system
     
   - name: setup metricbeat
     command: metricbeat setup
     
   - name: start metricbeat service
     command: service metricbeat start
        
   - To run the playbook: ansible-playbook metricbeat-playbook.yml
   
   to run the playbook, you have to be in the directory the playbook is at.


