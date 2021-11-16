# Credentials Setup

## Introduction

For the sake to seperate concerns and responsibilites and to be able to delegate job execution without disclosing the technical neccesarry access credentials Ansible Controller stores credentials securly within the system. These credentials get attached to the job templates which need them.<br>
As credentials need different atrributes and have different ways to be used, Ansible Controller has the concept of Credential Types. For instance the credential type `Machine Credential` is used to connect to a Server via ssh.<br>
To manage hardware through OneView we need to ensure to have the credentials to connect to OneView. As Ansible Controller does not know the details of OneView, we will create a `custom credential type` which will e.g. be able to hold the API-Version. Thereafter we will create a credentail of that new type needed to connect to OneView.


## Our aim
- We know from the last section that our Job Template is still not working. Executing this Job Template fails, because the variables holding the credentials are not available.
- We will therefor create the credential type
- create the credential 
- Executing this Job Template again should at least have solved the issue with undefined variables
- Create all remaining credentials 

## The Tasks
### Review Job Execution 
Review the output of the last time we executed the Job template
Navigate to **Jobs** in Tower UI, and click on the upmost **XX - Oneview: Oneview testing** :

This should bring you back to the `JOBS / XX - OneView: Oneview testing` View.<br>
Please investigate for the reason of failure in the provided logs. Most likely the credentials are missing.

![Credentail-Missing](/images/credentials_missing.png)

### Create custom credential type
For the sake of time we provided a playbook to create the custom credential type.<br>
Please like before execute 41_create_oneview_cred_type.yml
Example:
```
[ansible@bastion1 cmd_line]$ cd
[ansible@bastion1 ~]$ cd cmd_line
[ansible@bastion1 cmd_line]$ ansible-playbook -i inventory 41_create_oneview_cred_type.yml
```

To verify what this did please:
Navigate to **Credential Types** in Tower UI, and click on **HPE Oneview Credentials** :
Besides `NAME` and `DESCRIPTION` you should see 2 boxes.<br>  
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

### Create all remaining credentials 
For the sake of time we provided a playbook to create the remaining credentials.<br>
Please like before execute 43_create_allother_credentials.yml
Example:
```
[ansible@bastion1 cmd_line]$ cd
[ansible@bastion1 ~]$ cd cmd_line
[ansible@bastion1 cmd_line]$ ansible-playbook -i inventory 43_create_allother_credentials.yml
```

