# Introduction

## Objective

Many Ansible users are already familiar with managing instances, systems and applications in a virtual environment… However, Ansible can also manage Hardware and devices such as Physical Servers and Network equipment... In this lab, we will introduce managing and automating HPE Hardware with Ansible and HPE OneView.<br>

This Lab will guide you through the deployment process covering HW configuration up to ESXi installation:

![DeploySimple](/images/ansible-workshop-illustration-deploymentprocess-simple.png)

* Adding a server to HPE Oneview. - If this lab is set up with Synergy Blades Servers. This step wil be ommited. 
* Create a profile template : Oneview-Server-Profile-Template; It defines Hardware configuration and deploy it into a server.
* Preparing and triggering the installation of HPE VMware ESXi server.


## General Setup

We have 10 Lab environments available, each with has the below setup:

![ans-wksp-01](/images/ansible-workshop-illustration-05.png)

```
    - User: The user / the participant needs to connect to machines via ssh and via http / https. 
        We can not grant that DNS will be working. So it is best to use IP-Adresses to connect.
        If you have a Windows machine it is best to have Putty installed.
    - Automation Controller (formerly called Ansible Tower) : a virtual machine running RHEL 8, 
        Automation Controller installed and subscribed.
	It's the controlling node you will mostly work on.
    - Automation Hub : a virtual machine running RHEL 8, 
        With private Automation Hub installed and subscribed. It is used in AAP 2 environments to 
        host the Execution Environment.
    - Bastion Host : a virtual machine running RHEL 8
        Webserver installed, genisoimage installed, ansible cmd-line tool available
    - HPE Oneview host : an appliance running HPE Oneview. Depending on setup this can be a shared 
        OneView instance. Please only change your dedicated Server as you might break other labs.
    - Server with ILO Advanced License 
        If it's a rack mount server it needs to be added to OneView as a first deployment step.
        If it's a Synergy Blade it is integrated into OneView and needs to be identified clearly.   
```

- **Connect** : To reach the Lab please connect your VPN as sent to you via email.
    
Review the presentation provided by the instructor to find the credentials and the target systems. 
We provide a list with Hostnames and IP addresses somehow.

Since the lab has no DNS server, IP-Addresses will be used instead of FQDNs. The Ansible inventory maps hostnames to IP addresses, those hostnames can only be used when running Ansible plays.<br>


- **Automation Controller** : The deployment will be managed from Automation Controller(Ansible Tower) via the Web-UI. So the Automation Controller will be the object of interest, where we concentrate on the most.<br>
We have a RHEL 8 Server with Ansible Controller (formerly known as Tower) installed. Everything is installed and subscribed. Organization, Project, Jobs, Credentials, et all is set up and ready to perform the deployment tasks.<br><br>
The Tower SW itself runs as user `awx`. You as administrator of that host can connect as user `ansible`. Most of the tasks to perform here will need `root` privileges.<br>

- **Bastion Host** : We provide a Bastion host running RHEL8 that will host:
   * ESXi ISO image using an apache server. This image will be used to boot the physical servers. you will find under `/var/www/html/isos`<br>
      ex: http://BASTION_HOST_IP/isos/ 

- **Target Host or Physical Server** : Lab provides only 10 `BL460c Gen9` Physical Servers with integrated `ILO 4`. 

- **HPE OneView Host** : All physical Servers of this lab (and also some belonging to other environments) are managed from one OneView instance. The predefined naming ensures that your Server Profile Templates are kept separate from your peers.

- **Ansible Playbooks** : The playbooks for the deployment process reside in the repository `https://github.com/mschreie/hpe_oneview_ansible_handsonlabs`.<br>
The relevant playbooks are part of the coresponding job-template definitions within the Controller. 
