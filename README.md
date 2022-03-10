
# Welcome to Red Hat / HPE Hands On Labs

## Introduction

This Lab introduces the use of **Red Hat Ansible Automation Platform** to automate HPE tools like **HPE OneView** and **HPE iLO**. If you are new to the Red Hat Ansible Automation Platform, we suggest that you attend one of the [Ansible Automation workshops](https://ansible.github.io/workshops/) to get started with the concepts. If you are planning to use the platform in production, we highly recommend attending the [Red Hat official training](https://www.redhat.com/en/services/training/all-courses-exams?f%5B0%5D=taxonomy_product_tid%3A25911) to master the concepts as well as the product.

The overall idea of this lab is to automate all HPE physical server deployment steps from Hardware configuration (bios settings, local raid configuration..) to application deployment and configuration. This lab will guide you to automate the installation of VMware ESXi on an HPE Physical Server.

You can use this Workshop in to seperate ways. 
A. (#User Experience) : As a User or Operator you run through the working setup (predeployed by your instructor) and understand the steps needed to deploy servers
B. (#Admin Experience) : As a Content Provider or Domain Specialist you learn the steps needed to set up the environment to allow a user or operator to easily set up new servers.

# User Experience
By the end of this lab, you should have an overview of how Ansible Automation Controller can help to automate a deployment process. This process includes HW Configuratuion Management via HPE OneView and OS deploment - in this case the deployment of an ESXi server.  Hopefully you know how to adjust input parameters to adjust the deployment.

## Our workshop:
| Topic   | Exercises  | 
|---|---|
| **00 Introduction** :<br> This chapter introduces the overall setup and the objective of this lab. Automation Controller (Ansible Tower) is partly pre-configured to make your life easier. All needed details are explained here. | [Introduction](./exercises/00_user_introduction.md) |
| **10 Project Setup** :<br> This chapter will explain how to set up a project in Automation Controller | [Project Setup](./exercises/10_projectsetup.md) |
| **20 Inventory Setup** :<br> This chapter will show in details how to set up an inventory | [Inventory Setup](./exercises/20_inventorysetup.md) |
| **30 Automation Hub Setup** :<br> This chapter will help you to enable Automation Controller to fetch modules from Red Hat Automation Hub | [Automation Hub Setup](./exercises/30_automationhubsetup.md) |
| **40 Credentials Setup** :<br> This chapter will explain how to create and use the HPE OneView credentials | [Credentials Setup](./exercises/40_credentialsetup.md) |
| **50 Virtual Environment Setup** :<br> This chapter will explain how to setup HPE OneView python SDK in the Virtual Environment | [Virtual Environment Setup](./exercises/50_venvsetup.md) |
| **60 Job Template Setup** :<br> This chapter shows how to add an HPE physical server to HPE OneView, how to configure it, then how to setup VMware ESXi in a in step by steps jobs.  | [Job Template Setup](./exercises/60_jobtemplatesetup.md) |
| **70 Bonus Exercice** :<br> Learn how to create a workflow job template in Automation Controller  (Ansible Tower)| [Create an overall Workflow](./exercises/70_workflow.md)
| **Additional Reading: git** :<br> Gain a first overview of git and how it works in conjunction with Ansible Automation Controller (Ansible Tower)| [Git](./exercises/git.md)
| **Additional Reading: otehr stuff** :<br> Some small thoughts which we wanted to preserver somewhere.| [Additional](./exercises/additional.md)

jkk

# Admin Experience
By the end of this lab, you should have a good getting started knowledge on how to configure and use Ansible Automation Controller (formerly called Ansible Tower) to automate Hardware setup via HPE OneView and HPE iLO.
 
To allow this to happen in a timely manner, we prepared some playbooks to fast forward some configuration tasks. 


## Our workshop:
| Topic   | Exercises  | 
|---|---|
| **00 Introduction** :<br> This chapter introduces the overall setup and the objective of this lab. Automation Controller (Ansible Tower) is partly pre-configured to make your life easier. All needed details are explained here. | [Introduction](./exercises/00_admin_introduction.md) |
| **10 Project Setup** :<br> This chapter will explain how to set up a project in Automation Controller | [Project Setup](./exercises/10_projectsetup.md) |
| **20 Inventory Setup** :<br> This chapter will show in details how to set up an inventory | [Inventory Setup](./exercises/20_inventorysetup.md) |
| **30 Automation Hub Setup** :<br> This chapter will help you to enable Automation Controller to fetch modules from Red Hat Automation Hub | [Automation Hub Setup](./exercises/30_automationhubsetup.md) |
| **40 Credentials Setup** :<br> This chapter will explain how to create and use the HPE OneView credentials | [Credentials Setup](./exercises/40_credentialsetup.md) |
| **50 Virtual Environment Setup** :<br> This chapter will explain how to setup HPE OneView python SDK in the Virtual Environment | [Virtual Environment Setup](./exercises/50_venvsetup.md) |
| **60 Job Template Setup** :<br> This chapter shows how to add an HPE physical server to HPE OneView, how to configure it, then how to setup VMware ESXi in a in step by steps jobs.  | [Job Template Setup](./exercises/60_jobtemplatesetup.md) |
| **70 Bonus Exercice** :<br> Learn how to create a workflow job template in Automation Controller  (Ansible Tower)| [Create an overall Workflow](./exercises/70_workflow.md)
| **Additional Reading: git** :<br> Gain a first overview of git and how it works in conjunction with Ansible Automation Controller (Ansible Tower)| [Git](./exercises/git.md)
| **Additional Reading: otehr stuff** :<br> Some small thoughts which we wanted to preserver somewhere.| [Additional](./exercises/additional.md)

