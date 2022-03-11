# Status Quo

## Introduction

We will now look into oneview and see the state of the systems. 
IMPORTANT: Please be aware that the systems we are working on are shared systems. Please take special caution to not alter other systems

Point your browser to the IP adress of "oneview" and login with the credentials provided.<br>

## Objective
The Objective of this chapter is to find our resources and assuer they are unconfigured and powered off.

## Tasks
### Review Server Hardware 
Within the provided Lab Table you find the target systems with the "OneView Name". This name is a combination of the enclosure name and the Bay-number within that enclosuer.<br>
Navigate to "Server Hardware" within OneView and locate "your" target machine. Click on it to get more details on the right hand side of the window.<br>
The Server should:
* match the definition in the spreadsheet
* match the definition in the inventory 
* have no server profile
* be switched off

### Review Server Profile Templates
Within OneView navigate to Server Profile and assure you do not find a Profile with "labXX", while XX is your dual digget lab-number. (e.g. Workshop_lab02_target2)<br>
Within OneView navigate to Server Profile Template and assure you do not find a Profile-Template with "labXX", while XX is your dual digget lab-number. (e.g. Workshop_lab02_target2)<br>

If you do find one, the other or both, please login to your controller, navigate to templates and press the rocket next to "OneView: Clean my templates in OneView". This should delete the server profile as well as the server profile template.

