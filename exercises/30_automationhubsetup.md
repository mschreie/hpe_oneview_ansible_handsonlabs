# Automation Hub

## Introduction

Ansible is very powerful. One reason to that is the huge community providing roles and content collections. The community versions can be found on https://galaxy.ansible.com. To have a trustful source with certified modules Red Hat Partners and Customers should use Automation Hub as source of content collections and roles.<br>
The HPE OneView Collection for instance is a certified and supported content collection, found on Red Hat Automation Hub.<br><br>

Within Ansible Controller you define a credential for each repository you want to connect to. This credential is of credential_type `Ansible Galaxy/Automation Hub API Token`.<br>
A freshly installed Tower has the parameters needed to connect to galaxy (the community repository) predefined in a credentail called `Ansible Galaxy`.<br>
Automation Hub needs a valid subscription and a downloaded Automation Token. [see here for more details](https://console.redhat.com/ansible/automation-hub/token) As we did not want to disclose this token, we created the `Automation Hub` Credential on your behalf.

## Our aim
- We will now create a first Job Template, which connects to Oneview and fetches some data.
- Executing this Job Template will fail, because the OneView Content Collection is missing.
- We will then ensure that the Organization has `Automation Hub` and `Ansible Galaxy` credentials attached. (order important)
- Executing this Job Template again should get us one step forward. Most likely we will run in other issues. (which will be addressed later).

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
- the project  (to know which repositoy to search)
- the inventory (to know which hosts to execute against)

We will discover more aspects of the Job Template later.<br><br>

press `LAUNCH`

This should bring you to the `JOBS / XX - OneView: Oneview testing` View.<br>
On the left hand side you find some information about this specific job just running. Examin what you see there.<br>  
After a short while the STATUS will be red `Failed`. Please investigate the reason of the failure on the right hand side in the log output. 

![Module-Missing](/images/module_missing.png)

### Assure `Automation Hub` and `Ansible Galaxy` credentials attached to Organization
In order to allow Ansible Controller to pull the missing content from Red Hat Automation Hub we add the credentials to the Organization.

Navigate to **Organizations** in Tower UI, and click on **Handsonlabs Organization** :

Left to the `GALAXY CREDENTIALS` Textbox click on the **magnifying glass**.<br>
Tower will only show credentials of the coresponding type. Select both credentials. Please ensure that `Automation Hub` shows up first. Tower will search for colletions in the order the repositories are listed.<br>
Click `SAVE`

### Execute Job Template again
Launch the Job / Job Template a second time and review the output. We should be able to see the Module got executed but will then fail for other reasons. Maybe you can analyse the reason?
