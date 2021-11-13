# Introduction

We have 20 Lab environments available each with
```Lab Systems:
    - Ansible Automation Platform Controller (formerly called Tower)
         RHEL 8, Ansible Controller installed
    - Bastion Host (RHEL 8)
         RHEL 8, Webserver installed, genisoimage installed, ansible cmd-line tool available
    - Windows Jump Host (Windows)
         Putty installed
    - Credentials to pull content from Red Hat Automation Hub
    - Oneview Instance
         shared with another team
    - Rack Mount Server with ILO Advanced Lisence
         shared with another team
```

## General Setup
- **Connect** : To reach the Lab you need to connect to: 
FIXME: URL and LOGIN and PASSWORD needed

The lab does not provide any DNS service so that you need to use IP-Addresses most of the time. Within Ansible the hostnames defined in the ansible inventory do work and should be used.

- **Jump Host** : This brings you to a Windows desktop presented within your browser. You might experience issues with cut&paste into and out of this system. A nice workaround is by creating an etherpad at: https://etherpad.opendev.org
You can open the same URL within and outside of the desktop and have a 2-step-cut&past working.

We use the windows system just to connect to other systems and services.

- **Controller** : The deployment will be managed from Controller(Tower) via the Web-UI of Controller. 
We have a RHEL 8 Server with Tower (AAP 1.2 / Tower Version 3.8) installed. The RHEL and Tower are correctly subscribed and registerd at cloud.redhat.com.
We already created an "Organization" called "Handsonlabs Organization". We recommend to use with this organization so that some predefined playbooks will not run into issues.

- **Bastion Host** : To configure the Controller and to have a place the controller can prepare e.g ISO-Images needed for the deployment we use the Bastion host. 
You typically work as user "ansible" on the bastion host.  

You find follwoing directories on bastion host:
|/var/www/html/isos|This directory offers the Installation ISO immages and is reachable via browser as http://..../isos/ . You will also find some usefull files about the setup of your environment.|
|$HOME/cmd_line|This directory offers some scripts to help you speed up repetetive or boring tasks.| 

- **Target Physical Server** : We have all together 10 DL360 Gen 9 Servers with an ILO 4. As we have 20 Lab environments please coordinate with your peers on usage.

- **OneView Instance** : We also have 10 OneView instances. The predefined naming assures that your Server Profile Templates are kept seperate as their names will differ. Adding the Server to Oneview and Deployment process can only be done one after the other.

- **Playbooks** : The playbooks for the deployment process reside in the repository https://github.com/mschreie/hpe_oneview_ansible_handsonlabs. The playbooks to help configure the Ansible Controller are tailored to your lab and are copied onto your bastion host. You should not need to alter either of the playbooks, variables files, inventory files or alike. Configuration will happen in the Controller UI.

