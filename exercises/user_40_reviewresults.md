# Review Results

## Introduction
While the deployment might take a while it makes sense to check the progress and the changes within OneView. 
IMPORTANT: Please be aware that the systems we are working on are shared systems. Please take special caution to not alter other systems

Point your browser to the IP adress of "oneview" and login with the credentials provided.<br>

## Objective
The Objective of this chapter is to assure the system is correctly configured and installed.

## Tasks
### Review Server Profile Templates
Within OneView navigate to Server Profile Template, find "your" template and click on it. The Server profile template should
* have one Server Profile derived from it (cicle at the right hand side).
Maybe you find the POST Message and some ohter stuff we defined in our blueprint?

### Review Server Profile
Navigate to "Server Profile" within OneView and locate "your" server profile. Click on it to get more details on the right hand side of the window.<br>
Your profile should 
* reviel the server it is put on (see "Server Hardware") - please compare the "bay number
* state that the server is powered on.
Again you should find the settings we provided.<br><br>

### Assure ISO disk is connected
Navigate to "Server Hardware" within OneView and locate "your" server. Click on it to get more details on the right hand side of the window. Connect to the ILO by clicking on the ILO IP-Address.<br>
Within ILO navigate to "Virtual Media" -> "Virtual Media". <br> You should see an http URI pointing to the customized ISO image. 


### Open a Console
To review the boot (and install) process of the server, we need to open a console. This can be done multiple ways:
Within Oneview navigate to your server profile or to your server and click on "Actions" -> "Launch HTML5 Console"<br>
OR: Within ILO-Interface navigate to "Information" -> "Overview" and click on "Integrated Remote Console "HTML5"<br><br>

Within the console you should see VMware ESXi installing and booting. Later on the screen should show the prefined static IP address.
