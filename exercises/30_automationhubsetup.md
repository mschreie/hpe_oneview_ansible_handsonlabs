# Automation Hub

## Introduction

Ansible is very powerful. One reason to that is the huge community providing roles and content collections. The community versions can be found on https://galaxy.ansible.com. To have a trustful source with certified modules Red Hat Partners and Customers should use Automation Hub as source of content collections and roles.<br>
The HPE OneView Collection for instance is a certified and supported content collection, found on Red Hat Automation Hub.<br><br>

Within Ansible Controller you define a credential for each repository you want to connect to. This credential is of credential_type `Ansible Galaxy/Automation Hub API Token`.<br>
A freshly installed Tower has the parameters needed to connect to galaxy (the community repository) predefined in a credentail called `Ansible Galaxy`.<br>
Automation Hub needs a valid subscription and a downloaded Automation Token. [see here for more details](https://console.redhat.com/ansible/automation-hub/token) As we did not want to disclose this token, we created the `Automation Hub` Credential on your behalf.

## Our aim
- We will now create a first Job Template, which uses Oneview Module to connect to Oneview and fetch some data.
- Executing this Job Template will fail, becaus the Content Collection holding the Module is not downloadable.
- We will then assure that the Organization has `Automation Hub` and `Ansible Galaxy` credentials attached. (order important)
- Executing this Job Template again should get the module started. Most likely we will run in other issues. (which will be addressed later).

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

Switch `VERBOSITY` to `3 (Debug)` and press `SAVE`.<br>
press `LAUNCH`

This should bring you to the `JOBS / XX - OneView: Oneview testing` View.<br>
You find some information about this specific job just running and the log output. After a short while the STATUS will be red `Failed`. Please investigate for the reason of failure.

### Assure `Automation Hub` and `Ansible Galaxy` credentials attached to Organization
Navigate to **Organizations** in Tower UI, and click on **Handsonlabs Organization** :

Left to the `GALAXY CREDENTIALS` Textbox click on the **magnifying glass**.<br>
Tower will only show credentials of the coresponding type. Select both credentials. Please assure that `Automation Hub` shows up first. Tower will search for colletions in the order the repositories are listed.<br>
Click `SAVE`

### Execute Job Template again
Launch the Job / Job Template a second time and review the output. We should be able to see the Module got executed but will then fail for other reasons. Maybe you can analyse the reason?
