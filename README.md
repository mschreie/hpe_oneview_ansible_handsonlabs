
# Welcome to Red Hat / HPE Hands On Labs

## Introduction

This Lab will help understand how to use Ansible to automate HPE tools like HPE OneView and HPE iLO with Ansible. If you’re new to Ansible Automation, we suggest that you attend one of the Ansible Automation workshops to get started with the concepts. If you are planning to use Ansible Automation in production, we highly recommend attending the Red Hat official training to master the concepts as well as the product.

The overall idea is to be able to automate the whole step from hw configuration (bios settings, local raid configuration) up to application configuration. In this Lab we will end with an installed VMware ESXi server.
After finishing this lab you will have a slight getting started knowledge on how to configure and use Ansible Controller (formerly Ansible Tower) to use Ansible for automating HW setup via HPE OneView and HPE iLO.

To allow this to happen in a timely manner, we prepared some playbooks to fast forward some configuration tasks. 

## Our workshop:
| Topic   | Exercises  | 
|---|---|
| **00 Introduction** :<br> This document will introduce the overall setup and the aim. Tower is partly preconfigured to make your life easier. All this is explained here. | [Introduction](./exercises/00_introduction.md) |
| **10 Proejct Setup** : Within this chapter we will set up a project | [ProjectSetup](./exercises/10_projectsetup.md) |
| **20 Inventory Setup** : Within this chapter we will set up an inventory | [InventorySetup](./exercises/20_inventorysetup.md) |
| **30 Automation Hub Setup** : Within this chapter we will enable the system to fetch modules from Automation Hub | [AutomationhubSetup](./exercises/30_automationhubsetup.md) |
| **40 Virtual Environment Setup** : The OneView Ansible Modules need python modules available. We will configure this | [VenvSetup](./exercises/40_venvsetup.md) |
| **50 Credentials Setup** : To connect to OneView instance you need credentials. We will configure this | [CredentialSetup](./exercises/50_credentialsetup.md) |
| **60 Job Template Setup** : The whole process form adding the server to oneview up to installation ov ESXi is seperated into a couple of jobs, each with it's own playbook. We set up these job templates and let them run to see things working | [JobtemplateSetup](./exercises/60_jobtemplatesetup.md) |








## Our workshop:

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
| **Exercice 6** : This excerice automates deployment of ESXi with Ansible Tower (Controller)| [VMware ESXi Automated Deployment](./exercises/vmware_install.md)
| **Bonus Exercice 7** : Learn how to create a workflow template in Ansible Tower (Controller)| [Create an overall Workflow](./exercises/workflow.md)

