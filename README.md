
# Welcome to Red Hat / HPE Hands On Labs

## Introduction

This Lab introduces the use of Ansible Automation Platform to automate HPE tools like HPE OneView and HPE iLO. If you are new to Ansible Automation Platform, we suggest that you attend one of the Ansible Automation workshops to get started with the concepts. If you are planning to use the platform in production, we highly recommend attending the Red Hat official training to master the concepts as well as the product.

The overall idea of this lab is to automate all HPE physical server deployment steps from Hardware configuration (bios settings, local raid configuration) to application deployment and configuration. This lab will guide you to automate the installation of VMware ESXi on an HPE Server.

By the end of this lab, you should have a good getting started knowledge on how to configure and use Ansible Automation Controller (formerly called Ansible Tower) to automate Hardware setup via HPE OneView and HPE iLO.
 
To allow this to happen in a timely manner, we prepared some playbooks to fast forward some configuration tasks. 


## Our workshop:
| Topic   | Exercises  | 
## Our workshop:
| Topic   | Exercises  | 
|---|---|
| **00 Introduction** :<br> This document will introduce the overall setup and the objective of this lab. Tower is partly preconfigured to make your life easier. All this is explained here. | [Introduction](./exercises/00_introduction.md) |
| **10 Project Setup** :<br> Within this chapter we will set up a project | [Project Setup](./exercises/10_projectsetup.md) |
| **20 Inventory Setup** :<br> Within this chapter we will set up an inventory | [Inventory Setup](./exercises/20_inventorysetup.md) |
| **30 Credentials Setup** :<br> To connect to the HPE OneView instance you need credentials. We will configure this | [Credentials Setup](./exercises/30_credentialsetup.md) |
| **40 Automation Hub Setup** :<br> Within this chapter we will enable the system to fetch modules from Automation Hub | [Automation Hub Setup](./exercises/40_automationhubsetup.md) |
| **50 Virtual Environment Setup** :<br> The HPE OneView Ansible Modules need python modules to be available. We will configure this | [Virtual Environment Setup](./exercises/50_venvsetup.md) |
| **60 Job Template Setup** :<br> This chapter shows how to add an HPE physical server to HPE OneView, how to configure it, then how to setup VMware ESXi in a number in step by steps jobs.  | [Job Template Setup](./exercises/60_jobtemplatesetup.md) |
| **70 Bonus Exercice** :<br> Learn how to create a workflow job template in Ansible Tower (Controller)| [Create an overall Workflow](./exercises/70_workflow.md)


<!-- ## Our workshop:

 | Topic   | Exercises  | 
 |---|---|
 | **Prerequisites** : This document will explain the prerequisites for this workshop| [Prerequisites](./exercises/prerequisites.md) |
 | **Exercice 0** : This guide explains how to install Red Hat Ansible Tower (Controller)| [Ansible Tower Deployment](./exercises/ansible_tower_install.md) |
 | **Preparation** : This preparation guides you to setup the bastion host| [Prepare Bastion Host](./exercises/prepare_bastion_host.md) |
 | **Exercice 1** : This prerequisite guides you to setup git and vscode on your windows laptop| [Code Editor and Git on Windows](./exercises/code_editor_and_git_on_windows.md) |
 | **Exercice 2** : This prerequisites guides you to create a fork of the provided workshop repository| [Cloning Workshop Using Git](./exercises/git.md) |
 | **Exercice 3** : This exercise helps to create your first virtual environement in tower| [Setting up Virtual Environment](./exercises/virtual_environment.md) |
 | **Exercice 4** : This exercise introduces how to automate HPE OneView with Ansible Tower (Controller)| [Getting Started with HPE OneView](./exercises/getting_started_with_hpe_oneview.md) |
 | **Exercice 5** : This excerice automates HW manipulation via  HPE OneView with Ansible Tower (Controller)| [Automationg HPE OneView to manipulate Server Configuration](./exercises/oneview_server_config.md) |
 |  **Exercice 6** : This excerice automates deployment of ESXi with Ansible Tower (Controller)| [VMware ESXi Automated Deployment](./exercises/vmware_install.md)
-->
