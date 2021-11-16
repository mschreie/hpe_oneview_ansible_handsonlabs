# Automation Hub

## Introduction

Ansible is very powerful. One reason to that is the huge community providing roles and content collections. The community versions can be found on https://galaxy.ansible.com. To have a trustful source with certified modules Red Hat Partners and Customers should use Automation Hub as source of content collections and roles.<br>
The HPE OneView Collection for instance is a certified and supported content collection, found on Red Hat Automation Hub.<br><br>

Within Ansible Controller you define a credential for each repository you want to connect to. This credential is of credential_type `Ansible Galaxy/Automation Hub API Token`.<br>
A freshly installed Tower has the parameters needed to connect to galaxy (the community repository) predefined in a credentail called `Ansible Galaxy`.<br>
Automation Hub needs a valid subscription and a downloaded Automation Token. [see here for more details](https://console.redhat.com/ansible/automation-hub/token) As we did not want to disclose this token, we created the `Automation Hub` Credential on your behalf.

## Our aim
- We know from the last section that our Job Template is still not working. Executing this Job Template fails, becaus the Content Collection holding the Module is not downloadable.
- We will then assure that the Organization has `Automation Hub` and `Ansible Galaxy` credentials attached. (order important)
- Executing this Job Template again should get the module started. Most likely we will run in other issues. (which will be addressed later).

## The Tasks

### Review Job Execution 
Review the output of the last time we executed the Job template
Navigate to **Jobs** in Tower UI, and click on the upmost **XX - Oneview: Oneview testing** :

This should bring you back to the `JOBS / XX - OneView: Oneview testing` View.<br>
Please investigate for the reason of failure in the provided logs. Most likely the module to be executed can not be found.

### Assure `Automation Hub` and `Ansible Galaxy` credentials attached to Organization
Navigate to **Organizations** in Tower UI, and click on **Handsonlabs Organization** :

Left to the `GALAXY CREDENTIALS` Textbox click on the **magnifying glass**.<br>
Tower will only show credentials of the coresponding type. Select both credentials. Please assure that `Automation Hub` shows up first. Tower will search for colletions in the order the repositories are listed.<br>
Click `SAVE`

### Execute Job Template again
Launch the Job / Job Template a second time and review the output. We should be able to see the Module got executed but will then fail for other reasons. Maybe you can analyse the reason?
