# Introduction

## Objective


Many Ansible users are already familiar with managing instances, systems and applications in a virtual environment… However, Ansible can also manage Hardware and devices such as Physical Servers and Network equipment... In this lab, we will introduce managing and automating HPE Hardware with Ansible and HPE OneView.<br>


This Lab will guide you through the steps needed to automate:
* Adding a server to HPE Oneview.
* Create a profile template : Oneview-Server-Profile-Template; It defines Hardware configuration and deploy it into a server.
* Preparing and triggering the installation of HPE VMware ESXi server.

While some steps need to be configured manually, we also prepared playbooks to speed up those tasks.

## General Setup

We have 20 Lab environments available, each with has the below setup:

![ans-wksp-01](/images/ansible-workshop-illustration-05.png)

```
    - Jump Host: a virtual machine running MS Windows.
        Putty installed
    - Automation Controller (formerly called Ansible Tower) : a virtual machine running RHEL 8, 
        Automation Controller installed and subscribed
    - Bastion Host : a virtual machine running RHEL 8
        Webserver installed, genisoimage installed, ansible cmd-line tool available
    - HPE Oneview host : an appliance running HPE Oneview shared with another team.
    - Rack Mount Server with ILO Advanced License shared with another team.
    
    - Red Hat Automation Hub Credentials to pull content from Red Hat Cloud.
```

- **Connect** : To reach the Lab please connect to the URL provided by your instructor. He will also share user credentials.
    
| Lab Credentials |                             |
|-----------------|-----------------------------|
| **LAB URL**     | Provided by Instructor      |
| **Login**       | Provided by Instructor      |
| **Password**    | Provided by Instructor      |
    

Since the lab has no DNS server, IP-Addresses will be used instead of FQDNs. The Ansible inventory maps hostnames to IP addresses, those hostnames can only be used when running Ansible plays.<br>
Please visit the **lab.html** file on your Desktop for **hosts**, **ip-addresses** and user **credentials**.

- **Jump Host** : When connected to the Lab URL, you will land on MS Windows Desktop presented within your browser. It is used as a jump host to access the other systems and services related to the lab.<br>
    You might experience issues with copy & paste from your own Personal computer to the MS Windows machine in the browser. A nice workaround can be achieved by creating an etherpad at: https://etherpad.opendev.org to share commands between both environments (2 step copy paste).<br>
    It might also make sense to open this lab guide within your MS Windows Desktop environment, so that you can copy & paste directly.<br>


- **Controller** : The deployment will be managed from Automation Controller(Ansible Tower) via the Web-UI. So the Automation Controller will be the object of interest, where we concentrate on the most.<br>
We have a RHEL 8 Server with Ansible Tower (AAP 1.2 / Tower Version 3.8) installed. RHEL and Tower are already subscribed and registered at cloud.redhat.com.<br><br>
The Tower SW itself runs as user `awx`. You as administrator of that host can connect as user `ansible`. Most of the tasks to perform here will need `root` privileges.<br>
We already created an **Organization** called `Handsonlabs Organization`. We recommend using this organization so that some predefined playbooks will not run into issues.

- **Bastion Host** : We provide a Bastion host running RHEL8 that will host:
   * ESXi ISO image using an apache server. This will image will be used to boot the physical servers. you will find under `/var/www/html/isos`<br>
      ex: http://BASTION_HOST_IP/isos/ .You will also find some useful files about the setup of your environment.
   * A Customer command_line to configure your Tower under : `$HOME/cmd_line`<br>
   This directory offers some scripts to help you speed up repetitive or boring tasks.

- **Target Physical Server** : Lab provides only 10 `DL360 Gen 9` Physical Servers with integrated `ILO 4`. As we have 20 Lab environments please coordinate with your peers on usage.

- **OneView Instance** : We also have only 10 HPE OneView instances. The predefined naming ensures that your Server Profile Templates are kept separate as their names will differ. Adding the Physical Server to HPE Oneview and the Deployment process can only be done one after the other.

- **Playbooks** : The playbooks for the deployment process reside in the repository `https://github.com/mschreie/hpe_oneview_ansible_handsonlabs`.<br>
The playbooks to help configure the Ansible Tower are tailored to your lab and are copied onto your bastion host at `/home/ansible/cmd_line` You should not need to alter either of the playbooks, variables files, inventory files or alike. Configuration will happen in the Controller UI.

HINT:
Please visit the lab.html file on your desktop for host, ip-addresses and user credentials of the just mentioned hosts.
