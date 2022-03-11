# Job Template Setup and Execution

## Introduction

We have prooven that a Job is able to reach out to OneView and perform tasks there. Therefore we have now ensured all prerequisits in Ansible Controller are avaiable, so that we can concentrate on the deployment itself.<br> 
We will now add the missing  job templates into the Ansible Controller. 
Please remember: Each job template combines the
- **Organization** which ensure access to the content collections on Automation Hub
- **Project** which ensures access to the playbooks (and other data) in the (git) repository
- **Inventory** which defines wich nodes are availbale / should be reached out to
- **Playbook** which defines what tasks to execute
- **Virtual Python Environment** which holds all python modules needed without harming other python environments

As adding these jobs might be a tedious task we once again help you with a playbook taking over this task. The time saved is better invested with examination and execution.

HINT: Please sync with your peer, who uses the same target systems on who taks which role (User A or User B). After the integration of all playbooks one user might want to start with executing while the other starts with analysing. You should swap roles after first run went through.

##### User A
- Add all missing Job Templates 
- Execute the job templates 
- Hand over the environment to your peer
- start examination of the playbooks and job templates

##### USER B
- Add all missing Job Templates 
- start examination of the playbooks and job templates
- get the environment handed over 
- Execute the job templates 

## The Tasks

### Add all missing Job Templates 
- Connect to your bastion host via ssh. 
- and execute the playbook `60_setup-other-jobs.yml`.

Example:
```
[ansible@bastion1 cmd_line]$ ansible-playbook -i inventory 60_setup-other-jobs.yml
```

### Execute the job templates

Please execute the following job templates Nr 1 to Nr 5 in the order given.<br> 
The first first 3 job templates will set up HPE Oneview, the job templates 4 and 5 will configure and install ESXi on Top.<br>
The Job Template a) to d) are not part of the workflow but might be helpful during the exersices.<br>

* First three job templates:

| Nr | Job Template | explanation | ways to check |
|---|---|---|---|
| 1| **OneView : Add Server to OneView** | needs the ILO-IP (and the credentials) to add this server into Oneview Management. | changes in Oneview |
| 2| **OneView : Create Server Profile Template** | creates a server profile template from a text based template file. | changes in Oneview |
| 3| **Oneview : Deplay Server Profile Template** | deploys the created Templeate as Server Profile onto a server. | changes in Oneview |

* Job templates 4 and 5 that effectively manage the physical server:

| **Nr** | **Job Template** | **explanation** | **ways to check** |
|---|---|---|---|
| 4| **ESXi : Customize boot ISO** | Adds kickstart file with customized  network config, root password into iso images and alters ISO behavior to auto install using this kick file. | view http:/\<bastion>/isos/ |
| 5| **ESXi : Boot from ISO via ILO** | One-Time boots the server from the customized ISO image | connect to ILO and to Server Console to see isntallation process |

* Additional Job templates that will be useful:

| **Nr** | **Job Template** | **explanation** | **ways to check** |
|---|---|---|---|
| a| **Demo Job Template** |  preinstalled jobt template on  afreshly installed Ansible Controller | - |
| b| **ESXi : Cleanup ISO creation** |  Wipes out temporary files and directories which where created during ISO preparation | see filesystem on bastion host |
| c| **OneView : Get Server Profile Facts** |  Gets facts from a server profile | see log output |
| d| **OneView: Remove Server from OneView** |  Powers down given server, deletes Server Profile from Server and deletes the same. | changes in OneView |
| e| **OneView: Wipe clean whole OneView** |  Deletes all Servers, Server Profiles and Server Profile Templates from Oneview | Changes in OneView |

For the overall review, proof, please connect to the ILO of your server, open a console and watch server boot and install process. During our preparation work this had massive network latency issues but was good enough to see that teh system did get installed.

### Hand Over of the environment
Please run following playbook to reset OneView 
* **OneView: Wipe clean whole OneView** Deletes all Servers, Server Profiles and Server Profile Templates from Oneview

### Examination:
#### Overview:
Look at the Job Template definition of **OneView: Add Server to OneView**. Which Virtual Environment is used? Which credentials are available? What is the playbook called?
If time allows also look at **ESXi: Customize boot ISO** for the same questions. What does the additional box ticked mean?

#### Dig into the playbook **OneView: Add Server to OneView**
NAvigate to the github repository with your browser. Open the playbook for the named Job template. What steps does it take? Why does it need ILO credentials when reaching out to OneView?  What is the second last Task for?

#### Dig into the playbook **ESXi: Customize boot ISO**
NAvigate to the github repository with your browser. Open the playbook for the named Job template. What steps does it take? Why does it need root priviledges? 

####  Additional questions:
Which file is usesd as a text templat for Server Profile Template creation?
How does "OneView : Deplay Server Profile Template" know the Name of the Server (as seen within OneView) to be deployed onto?

