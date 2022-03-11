# Deploy it

## Introduction

In Ansible Automation Controller a job is a distinct "task"  being run at a certain point in time. If the same "task" will run again, it will be a different job. The definition of these jobs, which could be executed at any time are called "Job Templates".<br>
In a production setup we would have a single workflow which would need to get started. A workflow can easily combine multiple Job-Templates to a single stream.<br>
In this lab we start each Job seperately so that you, as the participant gain a better understanding of what is being done. You will understand the existing Job Templates. 

Point your browser to the IP adress of "controller" and login with the credentials provided.<br>

## Objective
The Objective of this chapter is to run through the deployment process.

## Tasks
### Execute the job templates

Please execute the following job templates Nr 1 to Nr 5 in the order given.<br> 
The first first 3 job templates will set up HPE Oneview, the job templates 4 and 5 will configure and install ESXi on Top.<br>
The Job Template a) to d) are not part of the workflow but might be helpful during the exersices.<br>

* First three job templates:
HINT: As we do not have Rack-Mount servers the server is already connected to OneView. Therefor the first step to add the server to OneView is omitted.

| Nr | Job Template | explanation | ways to check |
|---|---|---|---|
~~| 1| **OneView : Add Server to OneView** | needs the ILO-IP (and the credentials) to add this server into Oneview Management. | changes in Oneview |~~
| 2| **OneView : Create Server Profile Template** | creates a server profile template from a text based template file. | changes in Oneview |
| 3| **Oneview : Deplay Server Profile Template** | deploys the created Templeate as Server Profile onto a server. | changes in Oneview |

Hint: Step 3 needed roughly 15 minutes to complete, while i was testing. You can start step 4 in parallel.<br><br>

* Job templates 4 and 5 that effectively install on the physical server:

| **Nr** | **Job Template** | **explanation** | **ways to check** |
|---|---|---|---|
| 4| **ESXi : Customize boot ISO** | Adds kickstart file with customized network config, root password into iso images and alters ISO behavior to auto install using this kick file. | view http:/\<bastion>/isos/ |
| 5| **ESXi : Boot from ISO via ILO** | One-Time boots the server from the customized ISO image | connect to ILO and to Server Console to see isntallation process |

* Additional Job templates that will be useful:

| **Nr** | **Job Template** | **explanation** | **ways to check** |
|---|---|---|---|
| a| **Demo Job Template** |  preinstalled jobt template on  afreshly installed Ansible Controller | - |
| b| **ESXi : Cleanup ISO creation** |  Wipes out temporary files and directories which where created during ISO preparation | see filesystem on bastion host |
| c| **OneView : Get Server Profile Facts** |  Gets facts from a server profile | see log output |
| d| **OneView: Clean my templates in OneView** |  Powers down given server, deletes the Server Profile from the Server and deletes the coresponding Server Profile Template. | changes in OneView |

