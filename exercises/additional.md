# Additional Reading


## Documetnation on the Red Hat Certified Content Collections from the Automation Hub
I normaly just use my faivorate search enginge and type in, `ansible &lt;name_of_module&bt; and get a pointer to the documentation i need. This only works partialy for the Content Collections from RH Automation Hub. My advice is to log in to https://console.redhat.com/ and navigate to **Automation Hub** -> **Collections**. There you can search for the collection of interest and navigate to the `Documentation` -tab to fibd the documentation matching the content collection in the right version and flavour.

## Documentation on the OneView API

One of the challanges i faced when creating the lab was to find the available parameters and inputs towards OneView. A place to find that is:

Start Page:<br>
https://techlibrary.hpe.com/docs/synergy/shared/error/GUID-BC2BCD7C-94D1-49CF-B03C-DE8748D839CA.html<br><br>
And as one example:<br>
I found many examples with `powerControl: MomentaryPress`, but i wanted to swithc off the systems harshly. The right parameter is found hrere:<br>
https://techlibrary.hpe.com/docs/enterprise/servers/oneview5.0/cicf-api/en/index.html#rest/server-hardware


## Persistance
Ansible gathers facts at the start of execution of a Playbook (or Job). During execution of such a job you can manipulate and add variables and facts. But they are typically lost at the end of the playbook execution. If needed in an information out of one job in the next would need some way of persistance. Trying to save data on a local system (the system which executes the playbook) works on command line but does not work with Controller (aka Tower). Why that is the case and how to work around that can be read here:<br>
https://serverfault.com/questions/697859/ansible-local-action-stat-doesnt-find-my-file




