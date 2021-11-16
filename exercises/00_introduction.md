# Introduction

## Objective

Unlike managing and automating operating systems (rhel, windows..) and Applications, automating hardware is not commonly used. Managing Hardware is often left behind, maybe because many Ansible gurus do not see the magic of using HPE OneView and Ansible.<br>

This Lab will guide through the steps needed to automate:
* Adding a server to HPE Oneview
* Create profile template : Oneview-Server-Profile-Template; It defines Hardware configuration and deploy it onto such a server.
* Preparing and triggering the installation of VMware ESXi server.

While some steps need to be configured manually, we also prepared playbooks to speed up those tasks.

## General Setup

We have 20 Lab environments available, each with

```Lab Systems:
    - Ansible Automation Platform Controller (formerly called Ansible Tower)
         RHEL 8, Ansible Controller installed
    - Bastion Host
         RHEL 8, Webserver installed, genisoimage installed, ansible cmd-line tool available
    - Windows Jump Host (Windows)
         Putty installed
    - Red Hat Automation Hub Credentials to pull content from 
    - Oneview Instance
         shared with another team
    - Rack Mount Server with ILO Advanced License
         shared with another team
```

- **Connect** : To reach the Lab please connect to the URL provided by your instructor. HE will also share user credentials.
Within the lab you do not find any DNS service so that you need to use IP-Addresses most of the time. Within Ansible the hostnames defined in the ansible inventory do work and should be used.<br>
Please visit the lab.html file on your desktop for host, ip-addresses and user credentials.

- **Jump Host** : When connected to the Lab via browser you will land on a Windows desktop presented within your browser. You might experience issues with copy & paste from your laptop to the windows machine in the browser. A nice workaround can be achieved by creating an etherpad at: https://etherpad.opendev.org and opening it to share commands between both environments.
You can open the same URL within and outside of the desktop and have a 2-step copy & paste solution.<br>
It might also make sense to open this lab guide within your environment, so that you can copy & paste directly.<br>
We use the windows system as a jump host to access the other systems and services related to the lab.

- **Controller** : The deployment will be managed from Automation Controller(Tower) via the Web-UI. So the Controller will be the object of interest, where we concentrate on the most.<br>
We have a RHEL 8 Server with Ansible Tower (AAP 1.2 / Tower Version 3.8) installed. RHEL and Tower are correctly subscribed and registered at cloud.redhat.com.<br><br>
The Controller SW itself runs as user `awx`. You as administrator of that host can connect as user `ansible`. Most of the tasks to perform here will need `root` privileges.<br>
We already created an **Organization** called `Handsonlabs Organization`. We recommend using this organization so that some predefined playbooks will not run into issues.

- **Bastion Host** : To configure the Controller and to have a place where the controller can prepare the ISO-Images, we use the Bastion host.<br><br> 
You typically work as user "ansible" on the bastion host.<br><br> 
You find following directories on bastion host:
   - `/var/www/html/isos`<br>This directory offers the Installation ISO immages and is reachable via browser as http://..../isos/ . You will also find some useful files about the setup of your environment.
   - `$HOME/cmd_line`<br>This directory offers some scripts to help you speed up repetitive or boring tasks.

- **Target Physical Server** : We have all together 10 `DL360 Gen 9` Servers with integrated `ILO 4`. As we have 20 Lab environments please coordinate with your peers on usage.

- **OneView Instance** : We also have 10 OneView instances. The predefined naming ensure that your Server Profile Templates are kept separate as their names will differ. Adding the Server to Oneview and the Deployment process can only be done one after the other.

- **Playbooks** : The playbooks for the deployment process reside in the repository `https://github.com/mschreie/hpe_oneview_ansible_handsonlabs`.<br>
The playbooks to help configure the Ansible Controller are tailored to your lab and are copied onto your bastion host at `/home/ansible/cmd_line` You should not need to alter either of the playbooks, variables files, inventory files or alike. Configuration will happen in the Controller UI.

HINT:
Please visit the lab.html file on your desktop for host, ip-addresses and user credentials of the just mentioned hosts.
