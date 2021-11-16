# Project Setup

## Introduction

As mentioned in the [Introduction](00_introduction.md) we start with a freshly installed Ansible Controller (Tower Version 3.8, AAP 1.2), which is subscribed and registered.<br>

Point your browser to the IP adress of "tower" found in your lab.html and login with the credentials provided in the same document.<br>

An **Organization** called `Handsonlabs Organization` is created. 

## Create a Project

Now we need to set up a Project. The project defines the source repository where Ansible Controller finds the playbooks, to be executed with the help of a job template defenition. 

Navigate to **Projects** in Tower UI, create a **New Project** :

![Create-Prj](/images/create-prj.png)

The Project we need is:

| Parameter | Value |
|---|---|
| NAME | HPE OneView Workshop |
| DESCRIPTION | Project for the hands on labs |
| ORGANIZATION | Handsonlabs Organization |
| SCM TYPE | Git |
| SCM URL | https://github.com/mschreie/hpe_oneview_ansible_handsonlabs |
| other fields | Leave them blank or with default values.<br>
| SCM UPDATE OPTIONS | You do not need to tick any |

Press `Save`

IMPORTANT:<br>
please be make sure to type the **exact** the NAME of the Project. The prepared playbooks which take over some configuration steps for you, expect the Project name to be exactly as noted in the table above.


Hint:<br>
We do not want the project to be updated before a job is launched to save time. In our case the repository is quite stable and if for any reason an update is needed, we can still trigger this manualy.<br>
