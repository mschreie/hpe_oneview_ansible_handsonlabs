# Virtual Environment Setup

## Introduction

Ansible Modules are typically written in python. Some of these ansible modules need python modules to run. Python has a concept of virtual environments, which allow you to install python modules within one such virtual environment without harming the other virtual environments. Ansible Tower makes use of this and allows to choose which venv (virtual environment) to execute with.
We will create a venv on the Tower host and assure the 


## Our aim
- We will examin the last run of our Job Template, which uses Oneview Module. Most likely some python module is missing.
- We will create a virtual environment on the TOWER node manually
- We will assure that our Job Template will use the newly created venv.
- Executing this Job Template again should get the job run through.

## The Tasks

### Review Job Execution 
Review the output of the last time we executed the Job template
Navigate to **Jobs** in Tower UI, and click on the upmost **XX - Oneview: Oneview testing** :

This should bring you back to the `JOBS / XX - OneView: Oneview testing` View.<br>
Please investigate for the reason of failure in the provided logs. Most likely some pyhton modules are missing.

![venv-Missing](/images/venv_missing.png)

### Create a virtual environment
HINT:<br>
Use putty to establish ssh connections to the TOWER host.<br>
With putty type in a session name `towerXX` and the IP-Adress and click `Save` bevor clicking `Open`.<br>

- Connect to your tower host via ssh. 
- Login as user `root`.
- cd to virtual environment base directory and create a new virtual python environment 
```
# cd /var/lib/awx/venv/
# python3 -m venv hpe_venv --system-site-packages
```
- activate that environment
```
# source hpe_venv/bin/activate
(hpe_venv) # python3 -V
Python 3.6.8
```

- install all needed python modules 
With your virtual environment set up and active, you can install the HPE sdks required for this use-case. In this workshop we will focus on :

   - HPE OneView
   - HPE ILO
To Install HPE OneView SDK, there are three ways to do so. In this workshop we will rely on pip to do so. Further details can be found on HPE official github repository in the link below :

https://github.com/HewlettPackard/oneview-python
```
(hpe_venv) $ pip install hpeOneView hpICsp python-hpilo python-ilorest-library psutil
Collecting hpOneView
  Downloading https://files.pythonhosted.org/packages/75/0c/a932041b58827c04cf3a565e0ace692e75f731d368e532ec4d484c870030/hpOneView-5.3.0.tar.gz (81kB)
    100% |████████████████████████████████| 81kB 3.6MB/s 
Collecting hpICsp
  Cache entry deserialization failed, entry ignored
  Using cached https://files.pythonhosted.org/packages/16/7d/22dcc6291808384bcc3bae3d50100662c607456695841aa48dedd3d8e445/hpICsp-1.0.2.tar.gz
Collecting python-ilorest-library
...
Successfully installed decorator-5.1.0 hpICsp-1.0.2 hpeOneView-5.3.0 jsonpatch-1.32 jsonpath-rw-1.4.0 jsonpointer-2.1 ply-3.11 python-ilorest-library-3.2.2 six-1.16.0 urllib3-1.26.6

```
- verify installation
```
(hpe_venv) $ pip freeze 
```
- deactivate the environment and exit
```
(hpe_venv) $ deactivate 
[root@tower venv]#  exit
```

### Configure Job Template to use the new a virtual environment
Navigate to **Templates** in Tower UI, and click on **OneView: Oneview testing** :

Change the ANSIBLE ENVIRONMENT

| Parameter | Value |
|---|---|
| ANSIBLE ENVIRONMENT | /var/lib/awx/venv/hpe_venv |
Leave all other fields unaltered and Click `SAVE`

### Execute Job Template again
Launch the Job / Job Template a second time and review the output. The Job should run through without error. 
