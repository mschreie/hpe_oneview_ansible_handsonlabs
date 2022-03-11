# Input parameters

## Introduction

As mentioned in the [Introduction](user_00_introduction.md) we have a fully configured controller and are ready to start a configuration and deployment of one system. Some parameters need to be available for this to work. The system needs to 
* identify the right hw
* know how to configure the firmware
* know parameters for the ESXi deployment (like IP-addresses, hostnames).

Point your browser to the IP adress of "controller" and login with the credentials provided.<br>
Please also connect via ssh as user "root" to the same controller.<br>
HINT: Please be carefull - root user is very powerfull.

## Objective
The Objective of this chapter is to review how this is presented to the systm.

## Tasks
### Review the blueprint of the server profile template
We provided a textfile in /tmp/work/ called standard_template.yml. This is the blueprint of the server profile template which wil be created within oneview.<br>
Experienced OneView users can easily adopt this blueprint to their needs. It might also be possible to generate this file out of a web based questionair or maybe even out of the orderfullfillment (which should know the targeted hw configuration very well). Please also notice that the blueprint contains some variables which can easily be defined elsewhere.

Questions:
1: How is the local storage configured?
2: Is an ILO password defined?
3: Is there a POST (Power On Self Test) - Message defined? (feel free to alter it).

HINT: If you want to alter the blueprint, review HPEs OneView API documentation:
https://techlibrary.hpe.com/docs/enterprise/servers/oneview5.0/cicf-api/en/index.html#rest/server-profile-templates


### Review the inventory
Ansible Controller uses an inventory which defines the managed nodes. Within the inventory you may provide additional parameters, as host parameters, host-group parameters or generel parameters. Ansible can pull inventories dynamically, from a file managed in git or statically entered into the Controller. This injection into the controller could again be automated from elsewhere.<br>
In our case we use a static inventory reviewed within the web-UI of the controller. <br>

Questions:
1: Which inventory is dedicated to our Lab?
2: Which hosts are defined withn the inventory?
3: Which hosts belong to the target_hosts host group?
4: Which parameters are defined for the target host?

