# Credentials Setup

## Introduction

For the sake to seperate concerns and responsibilites and to be able to delegate job execution without disclosing the technical neccesarry access credentials Ansible Controller stores credentials securly within the system. These credentials get attached to the job templates which need them.<br>
As credentials need different atrributes and have different ways to be used, Ansible Controller has the concept of Credential Types. For instance the credential type `Machine Credential` is used to connect to a Server via ssh.<br>
To manage hardware through OneView we need to assure to have the credentials to connect to OneView. As Ansible Controller does not know the details of OneView, we will create a `custom credential type` which will e.g. be able to hold the API-Version. Thereafter we will create a credentail of that new type needed to connect to OneView.


## Our aim
- We will now create a first Job Template, which uses these credentials to connect to Oneview and fetch some data.
- Executing this Job Template will fail, because the credentails are missing.
- We will then create the credential type
- create the credential 
- Executing this Job Template again should at least have solved the issue with undefined variables

## The Tasks
### Create Job Template
HINT:<br>
Use putty to establish ssh connections to the bastion host.<br>
With putty type in a session name `bastionXX` and the IP-Adress and click `Save` bevor clicking `Open`.<br>

- Connect to your bastion host via ssh. 
- Login as user `ansible`.
- cd to cmd_line 
- and execute the playbook `30_create-test-job.yml`.

Example:
```
[ansible@bastion1 cmd_line]$ cd
[ansible@bastion1 ~]$ cd cmd_line
[ansible@bastion1 cmd_line]$ ansible-playbook -i inventory 30_create-test-job.yml
```
HINT:
Depending on time and interest you might want to look at `inventory` file and recon the different host_groups. If you then look at the header of the playbook you might find the host_group this play is targeted against.<br>
For a deeper investigation you might also want to look into `group_vars/all.yml` file, which defines many variables used throughout the cmd-line used playbooks. 

### Execute Job Template
Navigate to **Templates** in Tower UI, and click on **Oneview: Oneview testing** :

You should now see the definition of the Job Template. The Job Templates brings together:
- the playbook (found in the repository of the project)
- the project  (to know whihc repositoy to search)
- the inventory (to know which hosts to execute against)

We will discover more aspects of the Job Template later.<br><br>

press `LAUNCH`

This should bring you to the `JOBS / XX - OneView: Oneview testing` View.<br>
On the left hand side you find some information about this specific job just running. Examin what you see there.<br>  
After a short while the STATUS will be red `Failed`. Please investigate for the reason of failure on the right hand side in the log output. 

![Credentail-Missing](/images/credentials_missing.png)

### Create custom credential type
For the sake of time we provided a playbook to create the custom credential type.<br>
Please like before execute 31_create_oneview_cred_type.yml
Example:
```
[ansible@bastion1 cmd_line]$ cd
[ansible@bastion1 ~]$ cd cmd_line
[ansible@bastion1 cmd_line]$ ansible-playbook -i inventory 31_create_oneview_cred_type.yml
```

To verify what this did please:
Navigate to **Credential Types** in Tower UI, and click on **HPE Oneview Credentials** :
Besides `NAME` and `DESCRIPTION` you shoould see 2 boxes.<br>  
- `INPUT CONFIGURATON` defines how input fields are named, how they are headlined in an Webform, when credentails are entered or altered.
- `INJECTOR CONFIGURATION` defines how the information is presented to the jobs (or the plays) respectively. We configured 2 seperate ways. With `env` the defined variables are injected as environment variables into the environment of the running playbook. With `extra_vars` ansible variables are made available within the running playbook. In this scenario we use the extra_vars as this seems more obvious to understand.

### Create OneView credential 
Navigate to **Credentials** in Tower UI, and click on **+** :

The Credentail  we need is:

| Parameter | Value |
|---|---|
| NAME | HPE OneView Credential |
| DESCRIPTION | HPE Oneview SDK Credential |
| ORGANIZATION | Handsonlabs Organization |
| CREDENTIAL TYPE | HPE Oneview Credential |
| HPE ONEVIEW USERNAME | Administrator |
| HPE ONEVIEW PASSWORD | will be defined elsewhere |
| HPE ONEVIEW DOMAIN | domain |
| HPE ONEVIEW API VERSION | 2000 |

IMPORTANT:<br>
please be precise with the NAME of the Credential. The prepared playbooks which take over some configuration steps for you, expect Names to be exatly as noted here.<br><br>
HINT:<br>
The domain will not be needed in our setup. But as it is defined as a mandatory field you need to put in something.

### Execut Job Template again 
Launch the Job / Job Template a second time and review the output. We should be able to see a different error. Most likely the module was not found. This tells us that all variables are defined now.

