# Service Installer for VMware Tanzu (Project Arcas)

This write up focuses at a TKGs install with AVI (NSX advanced loadbalancer)
Further down is the TKGm install

## TKGs

A nice network spread sheet is located here 

https://github.com/ogelbric/Arcas/blob/main/Arcasdeploymentspreadsheet.xlsx


## My vCenter set up (3 ESXi hosts with vSAN)

![Version](https://github.com/ogelbric/Arcas/blob/main/Arcas1.png)


## Download the Tanzu Service Installer OVA

Send e-mail or ogelbrich@vmware.com to get access

https://www.dropbox.com/sh/xxx/AADU_xxxxxxxxxxztl7ESHa?dl=0


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
If you have this error you may have to pull the kubectl-vsphere binary from the API endpoint
```
wget --no-check-certificate https://192.168.4.71/wcp/plugin/linux-amd64/vsphere-plugin.zip

```
And unzip it and place it in /usr/local/bin


![Version](https://github.com/ogelbric/Arcas/blob/main/Arcas25.png)

## Outcome in WCP enable vCenter

![Version](https://github.com/ogelbric/Arcas/blob/main/Arcas26.png)

## Outcome in vCenter with AVI service engines deployed

![Version](https://github.com/ogelbric/Arcas/blob/main/Arcas27.png)

## Outcome loggin onto supervisor cluster

```
/usr/local/bin/kubectl-vsphere login --vsphere-username administrator@vsphere.local --server=https://192.168.4.71 --insecure-skip-tls-verify
kubectl config use-context 192.168.4.71
kubectl get nodes
```

![Version](https://github.com/ogelbric/Arcas/blob/main/Arcas28.png)

## Deploying a namespace (a user needs to be added in the vCenter GUI!) 

```
arcas --env vsphere --file vsphere.json --create_supervisor_namespace
```

![Version](https://github.com/ogelbric/Arcas/blob/main/Arcas29.png)


#### jason file example

```
root@arcas [ /opt/vmware/arcas/src ]# cat vsphere.json
{
    "env-spec": {
        "vcenter-details": {
            "vcenter-address": "192.168.1.50",
            "vcenter-sso-user": "administrator@vsphere.local",
            "vcenter-sso-password-base64": "Vk13YXJlMSE=",
            "vcenter-datacenter": "avi-Datacenter",
            "vcenter-cluster": "avi-Cluster",
            "vcenter-datastore": "vsanDatastore",
            "content-library-name": "avi",
            "avi-ova-name": "controller-21.1.2-9124"
        },
        "env-type": "tkgs",
        "marketplace-spec": {
            "refresh-token": ""
        },
        "saas-endpoints": {
            "tmc-details": {
                "tmc-availability": "false",
                "tmc-refresh-token": "",
                "tmc-supervisor-cluster-name": ""
            }
        },
        "infra-components": {
            "dns-servers-ip": "192.168.1.7",
            "search_domains": "lab.local",
            "ntp-servers": "10.128.152.81"
        }
    },
    "tkgs-component-spec": {
        "control-plane-size": "MEDIUM",
        "avi-mgmt-network": {
            "avi-mgmt-network-name": "DVPG-Management Network",
            "avi-mgmt-network-gateway-cidr": "192.168.1.1/24",
            "avi-mgmt-service-ip-startrange": "192.168.1.60",
            "avi-mgmt-service-ip-endrange": "192.168.1.70"
        },
        "avi-components": {
            "avi-password-base64": "Vk13YXJlMSE=",
            "avi-backup-passphrase-base64": "Vk13YXJlMSE=",
            "avi-controller01-ip": "192.168.1.40",
            "avi-controller01-fqdn": "avi.lab.local"
        },
        "tkgs-vip-network": {
            "tkgs-vip-network-name": "DVPG-Frontend Network",
            "tkgs-vip-network-gateway-cidr": "192.168.4.1/24",
            "tkgs-vip-ip-startrange": "192.168.4.70",
            "tkgs-vip-ip-endrange": "192.168.4.100"
        },
        "tkgs-mgmt-network-spec": {
            "tkgs-mgmt-network-name": "DVPG-Management Network",
            "tkgs-mgmt-network-gateway-cidr": "192.168.1.1/24",
            "tkgs-mgmt-network-starting-ip": "192.168.1.80",
            "tkgs-mgmt-network-dns-server": "192.168.1.7",
            "tkgs-mgmt-network-search-domains": "lab.local",
            "tkgs-mgmt-network-ntp": "10.128.152.81"
        },
        "tkgs-primary-workload-network": {
            "tkgs-primary-workload-network-name": "DVPG-Workload Network",
            "tkgs-primary-workload-network-gateway-cidr": "192.168.5.1/24",
            "tkgs-primary-workload-network-start-range": "192.168.5.70",
            "tkgs-primary-workload-network-end-range": "192.168.5.100",
            "tkgs-workload-dns-server": "192.168.1.7",
            "tkgs-workload-service-cidr": "10.96.0.0/22"
        },
        "tkgs-storage-policy-spec": {
            "master-storage-policy": "vSAN Default Storage Policy",
            "ephemeral-storage-policy": "vSAN Default Storage Policy",
            "image-storage-policy": "vSAN Default Storage Policy"
        },
        "tkgs-vsphere-namespace-spec": {
            "tkgs-vsphere-namespace-name": "namespace1000",
            "tkgs-vsphere-namespace-description": "",
            "tkgs-vsphere-namespace-workload-network": "DVPG-Workload Network",
            "tkgs-vsphere-namespace-content-library": "avi",
            "tkgs-vsphere-namespace-vm-classes": [
                "best-effort-small",
                "best-effort-2xlarge",
                "best-effort-large",
                "best-effort-xsmall",
                "best-effort-medium",
                "best-effort-xlarge"
            ],
            "tkgs-vsphere-namespace-resource-spec": {},
            "tkgs-vsphere-namespace-storage-spec": [
                {
                    "storage-policy": "vSAN Default Storage Policy"
                }
            ],
            "tkgs-vsphere-workload-cluster-spec": {
                "tkgs-vsphere-namespace-name": "namespace1000",
                "tkgs-vsphere-workload-cluster-name": "tkg-cluster",
                "allowed-storage-classes": [
                    "vSAN Default Storage Policy"
                ],
                "default-storage-class": "vSAN Default Storage Policy",
                "node-storage-class": "vSAN Default Storage Policy",
                "service-cidr-blocks": "192.168.0.0/16",
                "pod-cidr-blocks": "10.96.0.0/12",
                "control-plane-vm-class": "best-effort-medium",
                "worker-vm-class": "best-effort-medium",
                "worker-node-count": "3",
                "enable-control-planne-ha": "false"
            }
        }
    }
}
```

## TKGm
This write up focuses at a TKGm install with AVI (NSX advanced loadbalancer)

Arcas is deployed(use previous section for that)
And here are the input screens

![Version](https://github.com/ogelbric/Arcas/blob/main/tkgm1.png)

![Version](https://github.com/ogelbric/Arcas/blob/main/tkgm2.png)

![Version](https://github.com/ogelbric/Arcas/blob/main/tkgm3.png)

![Version](https://github.com/ogelbric/Arcas/blob/main/tkgm4.png)

![Version](https://github.com/ogelbric/Arcas/blob/main/tkgm5.png)

![Version](https://github.com/ogelbric/Arcas/blob/main/tkgm6.png)

![Version](https://github.com/ogelbric/Arcas/blob/main/tkgm7.png)

![Version](https://github.com/ogelbric/Arcas/blob/main/tkgm8.png)

![Version](https://github.com/ogelbric/Arcas/blob/main/tkgm9.png)

![Version](https://github.com/ogelbric/Arcas/blob/main/tkgm10.png)

![Version](https://github.com/ogelbric/Arcas/blob/main/tkgm11.png)

![Version](https://github.com/ogelbric/Arcas/blob/main/tkgm12.png)

![Version](https://github.com/ogelbric/Arcas/blob/main/tkgm13.png)

![Version](https://github.com/ogelbric/Arcas/blob/main/tkgm14.png)







