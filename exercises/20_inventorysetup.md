# Inventory Setup

## Introduction

As you know, Ansible executes playbooks against managed nodes. For Ansible to know which nodes to manage it needs an inventory. Typically inventories are derived from some other source (e.g CMDB, vCenter, AWS, ..). As we do not want to add dependecies to systems outside our control and our environment is very small, we decided to go with static inventories entered into Tower directly.
To minimize the effort needed, we created an inventory `Lab inventory` and prefilled most of it.

## Inventory introduction
This setup is built with scale in mind even though we only have a limited number of Systems. For scalability we target host_groups (instead of single hosts), this would give us the chance to deploy dozens of servers at the same time.
The host groups we defined are:
- **target_hosts** : Including all the target hosts (physical servers), which will be newly deployed during this lab.<br>Correct target system needs to be added.
- **oneview_hosts** : Including all the HPE OneView hosts.<br>This is prefilled with the correct host(s).
- **bastion_hosts** : Including all the bastion hosts.<br>This is prefilled with the correct host(s).
- **tower_hosts** : The Tower Hosts Group was / is only needed to set up the Ansible Tower system properly and will not be found in the inventory inside Tower.

Since we do not have a DNS service, each host entry needs an additional `ansible_host` entry, which defines how Ansible can reach the host in question. In our case this `ansible_host` needs to contain a valid IP address.<br><br>


Typically the network layout defines which HPE Oneview host to use for a specific target host. Same is (most likely) true for the bastion host. To define this relationship the target_host needs a host variable `bastion_host` and `oneview_host` naming the correct bastion host and the correct HPE oneview host.<br>
As we want to install ESXi with static ip address configuration ansible needs to know the network parameters for each host to deploy. Therefore, we also need additional host variables for the target host to ensure ESXi installation to have networking information available.


## View Inventory and add missing host

* Navigate to **Inventory** in Tower UI, and click on **Lab inventory**
* Ensure that you have 3 groups (target_hosts, oneview_hosts, bastion_hosts). Ensure that 2 hosts in their corresponding groups. Check that the names relate to your lab (as outlined elsewhere). Also check if the host_vars related to the hosts are defined.

* To know what to add please open a second tab of your browser to `http://BASTION_IP_ADDRESS/isos/target_host.info`<br>
To add the target host to the right group:

* Select **Lab inventory** in Tower UI, click on **GROUPS** button, click on **target_hosts**, click on **hosts** button.
 
![AddHostToInventory](/images/AddHostToInventory.png)

As in the image you should see **INVENTORIES / Lab inventory / ALL GROUPS / target_hosts / ASSOCIATED HOSTS** in the headline. Click on **+** button and choose **New Host** .

The following is an example. Names and IP adresses wil differ in your environment!

| Parameter | Value |
|---|---|
| HOST NAME | g11 |
| DESCRIPTION | |
| VARIABLES |  see below |

The VARIABLES field as example:
```
--- 
ansible_host: "10.31.113.41"
ilo_ip: "10.31.114.41"
bastion_host: "bastion21"
oneview_host: "g21ov"  
esxi_bootproto: "static"
esxi_ip: "10.31.113.41"
esxi_mask: "255.255.0.0"
esxi_gw: "10.31.255.254"
esxi_fqdn: "esxi.example.com"
esxi_nameserver: "10.187.1.10"
esxi_domain: "example.com"
```

IMPORTANT:
Please leave the three dashes in place. And please avoid any white space in front of the variable names.
HINT:
It might be that the Info-Pages has a parameter `host_ip`. In the VARIABLES textbox this needs to be called `ansible_host`
