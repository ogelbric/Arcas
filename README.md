# Service Installer for VMware Tanzu (Project Arcas)
This write up focuses at a TKGs install with AVI (NSX advanced loadbalancer)

A nice network spread sheet is located here 

![Version]("https://github.com/ogelbric/Arcas/blob/main/Arcasdeploymentspreadsheet.xlsx")


## My vCenter set up (3 ESXi hosts with vSAN)

![Version](https://github.com/ogelbric/Arcas/blob/main/Arcas1.png)


## Download the Tanzu Service Installer OVA

need URL here... 

## Deploy the Tanzu Service Installer OVA 

![Version](https://github.com/ogelbric/Arcas/blob/main/Arcas2.png)

![Version](https://github.com/ogelbric/Arcas/blob/main/Arcas3.png)

![Version](https://github.com/ogelbric/Arcas/blob/main/Arcas4.png)

![Version](https://github.com/ogelbric/Arcas/blob/main/Arcas5.png)

Power on once deployed

![Version](https://github.com/ogelbric/Arcas/blob/main/Arcas10.png)
  
## DNS set up

![Version](https://github.com/ogelbric/Arcas/blob/main/Arcas6.png)

## Setup the AVI OVA in the content library in vCenter

![Version](https://github.com/ogelbric/Arcas/blob/main/Arcas7.png)

![Version](https://github.com/ogelbric/Arcas/blob/main/Arcas8.png)

## Use broswser and connect to port 8888 on the Tanzu Service Installer 
(In my case http://192.168.1.39:8888)

![Version](https://github.com/ogelbric/Arcas/blob/main/Arcas9.png)

## Here are the network settings for a 3 network setup

![Version](https://github.com/ogelbric/Arcas/blob/main/Arcas11.png)

![Version](https://github.com/ogelbric/Arcas/blob/main/Arcas12.png)

![Version](https://github.com/ogelbric/Arcas/blob/main/Arcas13.png)

![Version](https://github.com/ogelbric/Arcas/blob/main/Arcas14.png)

![Version](https://github.com/ogelbric/Arcas/blob/main/Arcas15.png)

![Version](https://github.com/ogelbric/Arcas/blob/main/Arcas16.png)

![Version](https://github.com/ogelbric/Arcas/blob/main/Arcas17.png)

![Version](https://github.com/ogelbric/Arcas/blob/main/Arcas18.png)

![Version](https://github.com/ogelbric/Arcas/blob/main/Arcas19.png)

![Version](https://github.com/ogelbric/Arcas/blob/main/Arcas20.png)

![Version](https://github.com/ogelbric/Arcas/blob/main/Arcas21.png)

![Version](https://github.com/ogelbric/Arcas/blob/main/Arcas22.png)

![Version](https://github.com/ogelbric/Arcas/blob/main/Arcas23.png)

```
cd /opt/vmware/arcas/src
arcas --env vsphere --file vsphere.json --avi_configuration --avi_wcp_configuration --enable_wcp
```

![Version](https://github.com/ogelbric/Arcas/blob/main/Arcas24.png)

### Please wait for about ~10-20 min for the WCp enablement to take place
The error can be ignored!

![Version](https://github.com/ogelbric/Arcas/blob/main/Arcas25.png)

## Outcome in WCP enable vCenter

![Version](https://github.com/ogelbric/Arcas/blob/main/Arcas26.png)

## Outcome in vCenter with AVI service engines deployed

![Version](https://github.com/ogelbric/Arcas/blob/main/Arcas27.png)

## Outcome loggin onto supervisor cluster

![Version](https://github.com/ogelbric/Arcas/blob/main/Arcas28.png)

## Deploying a namespace (a user needs to be added in the vCenter GUI!) 

```
arcas --env vsphere --file vsphere.json --create_supervisor_namespace
```

![Version](https://github.com/ogelbric/Arcas/blob/main/Arcas29.png)









