# Service Installer for VMware Tanzu (Project Arcas 1.1)

## TKGm

Network Setup:

```
Networks .3 .5 .7
.3 = Management
	vCenter 3.50
	Arcas79 3.39
	Avi 3.40
	
	Avi mgt Start 3.60-69
	TKGm mgt start 3.70-89
	TKGm work 3.90-99
	
.5 = Frontend
	AVI .5-60-89
	
.7 = Workload

Gateway = "192.168.3.1"
Gateway = "192.168.5.1"
Gateway = "192.168.7.1"

DNS = "10.197.79.7"
NTP = "10.128.152.81"

```
OVA Deploy

![Version](https://github.com/ogelbric/Arcas/blob/main/arcas11-1.png)
![Version](https://github.com/ogelbric/Arcas/blob/main/arcas11-2.png)
![Version](https://github.com/ogelbric/Arcas/blob/main/arcas11-3.png)
![Version](https://github.com/ogelbric/Arcas/blob/main/arcas11-4.png)
![Version](https://github.com/ogelbric/Arcas/blob/main/arcas11-5.png)
![Version](https://github.com/ogelbric/Arcas/blob/main/arcas11-6.png)
![Version](https://github.com/ogelbric/Arcas/blob/main/arcas11-7.png)
![Version](https://github.com/ogelbric/Arcas/blob/main/arcas11-8.png)
![Version](https://github.com/ogelbric/Arcas/blob/main/arcas11-9.png)
![Version](https://github.com/ogelbric/Arcas/blob/main/arcas11-10.png)
![Version](https://github.com/ogelbric/Arcas/blob/main/arcas11-11.png)
![Version](https://github.com/ogelbric/Arcas/blob/main/arcas11-12.png)
![Version](https://github.com/ogelbric/Arcas/blob/main/arcas11-13.png)
![Version](https://github.com/ogelbric/Arcas/blob/main/arcas11-14.png)
![Version](https://github.com/ogelbric/Arcas/blob/main/arcas11-141.png)
![Version](https://github.com/ogelbric/Arcas/blob/main/arcas11-15.png)
![Version](https://github.com/ogelbric/Arcas/blob/main/arcas11-16.png)
![Version](https://github.com/ogelbric/Arcas/blob/main/arcas11-17.png)
![Version](https://github.com/ogelbric/Arcas/blob/main/arcas11-18.png)
![Version](https://github.com/ogelbric/Arcas/blob/main/arcas11-19.png)
![Version](https://github.com/ogelbric/Arcas/blob/main/arcas11-20.png)
![Version](https://github.com/ogelbric/Arcas/blob/main/arcas11-21.png)
![Version](https://github.com/ogelbric/Arcas/blob/main/arcas11-22.png)
![Version](https://github.com/ogelbric/Arcas/blob/main/arcas11-23.png)
![Version](https://github.com/ogelbric/Arcas/blob/main/arcas11-24.png)
![Version](https://github.com/ogelbric/Arcas/blob/main/arcas11-25.png)
![Version](https://github.com/ogelbric/Arcas/blob/main/arcas11-26.png)
![Version](https://github.com/ogelbric/Arcas/blob/main/arcas11-27.png)
![Version](https://github.com/ogelbric/Arcas/blob/main/arcas11-28.png)
![Version](https://github.com/ogelbric/Arcas/blob/main/arcas11-29.png)
![Version](https://github.com/ogelbric/Arcas/blob/main/arcas11-30.png)
![Version](https://github.com/ogelbric/Arcas/blob/main/arcas11-31.png)

Execute on the Arcas VM: 

```
arcas --env vsphere --file /opt/vmware/arcas/src/vsphere-dvs-tkgm.json --avi_configuration --tkg_mgmt_configuration --verbose
kubectl config use-context mgtcluster-admin@mgtcluste

arcas --env vsphere --file /opt/vmware/arcas/src/vsphere-dvs-tkgm.json --avi_configuration --tkg_mgmt_configuration --shared_service_configuration

arcas --env vsphere --file /opt/vmware/arcas/src/vsphere-dvs-tkgm.json --avi_configuration --tkg_mgmt_configuration --shared_service_configuration --workload_preconfig --workload_deploy
```

Results for each line above: 

![Version](https://github.com/ogelbric/Arcas/blob/main/arcas11-32.png)
![Version](https://github.com/ogelbric/Arcas/blob/main/arcas11-33.png)
![Version](https://github.com/ogelbric/Arcas/blob/main/arcas11-34.png)



YAML file: vsphere-dvs-tkgm.json

```
{
    "envSpec": {
        "vcenterDetails": {
            "vcenterAddress": "192.168.3.50",
            "vcenterSsoUser": "administrator@vsphere.local",
            "vcenterSsoPasswordBase64": "Vk13YXJlMSE=",
            "vcenterDatacenter": "avi-Datacenter",
            "vcenterCluster": "avi-Cluster",
            "vcenterDatastore": "vsanDatastore",
            "contentLibraryName": "avi",
            "aviOvaName": "controller-20.1.7-9154",
            "resourcePoolName": ""
        },
        "envType": "tkgm",
        "marketplaceSpec": {
            "refreshToken": ""
        },
        "saasEndpoints": {
            "tmcDetails": {
                "tmcAvailability": "false",
                "tmcRefreshToken": ""
            },
            "tanzuObservabilityDetails": {
                "tanzuObservabilityAvailability": "false",
                "tanzuObservabilityUrl": "",
                "tanzuObservabilityRefreshToken": ""
            }
        },
        "infraComponents": {
            "dnsServersIp": "10.197.79.7",
            "ntpServers": "10.128.152.81",
            "searchDomains": "lab.local"
        },
        "proxySpec": {
            "arcasVm": {
                "enableProxy": "false",
                "httpProxy": "",
                "httpsProxy": "",
                "noProxy": ""
            },
            "tkgMgmt": {
                "enableProxy": "false",
                "httpProxy": "",
                "httpsProxy": "",
                "noProxy": ""
            },
            "tkgSharedservice": {
                "enableProxy": "false",
                "httpProxy": "",
                "httpsProxy": "",
                "noProxy": ""
            },
            "tkgWorkload": {
                "enableProxy": "false",
                "httpProxy": "",
                "httpsProxy": "",
                "noProxy": ""
            }
        }
    },
    "tkgComponentSpec": {
        "aviMgmtNetwork": {
            "aviMgmtNetworkName": "DVPG-Management Network",
            "aviMgmtNetworkGatewayCidr": "192.168.3.1/24",
            "aviMgmtServiceIpStartRange": "192.168.3.60",
            "aviMgmtServiceIpEndRange": "192.168.3.69"
        },
        "tkgClusterVipNetwork": {
            "tkgClusterVipNetworkName": "DVPG-Frontend Network",
            "tkgClusterVipNetworkGatewayCidr": "192.168.5.1/24",
            "tkgClusterVipIpStartRange": "192.168.5.60",
            "tkgClusterVipIpEndRange": "192.168.5.89"
        },
        "aviComponents": {
            "aviPasswordBase64": "Vk13YXJlMSE=",
            "aviBackupPassphraseBase64": "Vk13YXJlMSE=",
            "enableAviHa": "false",
            "aviController01Ip": "192.168.3.40",
            "aviController01Fqdn": "avi.lab.local",
            "aviController02Ip": "",
            "aviController02Fqdn": "",
            "aviController03Ip": "",
            "aviController03Fqdn": "",
            "aviClusterIp": "",
            "aviClusterFqdn": "",
            "aviSize": "small",
            "aviCertPath": "",
            "aviCertKeyPath": ""
        },
        "tkgMgmtComponents": {
            "tkgMgmtNetworkName": "DVPG-Management Network",
            "tkgMgmtGatewayCidr": "192.168.3.1/24",
            "tkgMgmtClusterName": "mgtcluster",
            "tkgMgmtSize": "medium",
            "tkgMgmtCpuSize": "",
            "tkgMgmtMemorySize": "",
            "tkgMgmtStorageSize": "",
            "tkgMgmtDeploymentType": "dev",
            "tkgMgmtClusterCidr": "100.96.0.0/11",
            "tkgMgmtServiceCidr": "100.64.0.0/13",
            "tkgMgmtBaseOs": "photon",
            "tkgSharedserviceClusterName": "sharedcluster",
            "tkgSharedserviceSize": "medium",
            "tkgSharedserviceCpuSize": "",
            "tkgSharedserviceMemorySize": "",
            "tkgSharedserviceStorageSize": "",
            "tkgSharedserviceDeploymentType": "dev",
            "tkgSharedserviceWorkerMachineCount": "2",
            "tkgSharedserviceClusterCidr": "100.96.0.0/11",
            "tkgSharedserviceServiceCidr": "100.64.0.0/13",
            "tkgSharedserviceBaseOs": "photon",
            "tkgSharedserviceKubeVersion": "v1.22.5"
        }
    },
    "tkgMgmtDataNetwork": {
        "tkgMgmtDataNetworkName": "DVPG-Management Network",
        "tkgMgmtDataNetworkGatewayCidr": "192.168.3.1/24",
        "tkgMgmtAviServiceIpStartRange": "192.168.3.70",
        "tkgMgmtAviServiceIpEndRange": "192.168.3.89"
    },
    "tkgWorkloadDataNetwork": {
        "tkgWorkloadDataNetworkName": "DVPG-Management Network",
        "tkgWorkloadDataNetworkGatewayCidr": "192.168.3.1/24",
        "tkgWorkloadAviServiceIpStartRange": "192.168.3.90",
        "tkgWorkloadAviServiceIpEndRange": "192.168.3.99"
    },
    "tkgWorkloadComponents": {
        "tkgWorkloadNetworkName": "DVPG-Management Network",
        "tkgWorkloadGatewayCidr": "192.168.3.1/24",
        "tkgWorkloadClusterName": "workcluster",
        "tkgWorkloadSize": "medium",
        "tkgWorkloadCpuSize": "",
        "tkgWorkloadMemorySize": "",
        "tkgWorkloadStorageSize": "",
        "tkgWorkloadDeploymentType": "dev",
        "tkgWorkloadWorkerMachineCount": "2",
        "tkgWorkloadClusterCidr": "100.96.0.0/11",
        "tkgWorkloadServiceCidr": "100.64.0.0/13",
        "tkgWorkloadBaseOs": "photon",
        "tkgWorkloadKubeVersion": "v1.22.5",
        "tkgWorkloadTsmIntegration": "false",
        "namespaceExclusions": {
            "exactName": "",
            "startsWith": ""
        }
    },
    "harborSpec": {
        "enableHarborExtension": "true",
        "harborFqdn": "harbor",
        "harborPasswordBase64": "Vk13YXJlMSE=",
        "harborCertPath": "",
        "harborCertKeyPath": ""
    },
    "tanzuExtensions": {
        "enableExtensions": "false",
        "tkgClustersName": "",
        "logging": {
            "syslogEndpoint": {
                "enableSyslogEndpoint": "false",
                "syslogEndpointAddress": "",
                "syslogEndpointPort": "",
                "syslogEndpointMode": "",
                "syslogEndpointFormat": ""
            },
            "httpEndpoint": {
                "enableHttpEndpoint": "false",
                "httpEndpointAddress": "",
                "httpEndpointPort": "",
                "httpEndpointUri": "",
                "httpEndpointHeaderKeyValue": ""
            },
            "elasticSearchEndpoint": {
                "enableElasticSearchEndpoint": "false",
                "elasticSearchEndpointAddress": "",
                "elasticSearchEndpointPort": ""
            },
            "kafkaEndpoint": {
                "enableKafkaEndpoint": "false",
                "kafkaBrokerServiceName": "",
                "kafkaTopicName": ""
            },
            "splunkEndpoint": {
                "enableSplunkEndpoint": "false",
                "splunkEndpointAddress": "",
                "splunkEndpointPort": "",
                "splunkEndpointToken": ""
            }
        },
        "monitoring": {
            "enableLoggingExtension": "false",
            "prometheusFqdn": "",
            "prometheusCertPath": "",
            "prometheusCertKeyPath": "",
            "grafanaFqdn": "",
            "grafanaCertPath": "",
            "grafanaCertKeyPath": "",
            "grafanaPasswordBase64": ""
        }
    }
}
```

Log onto a worker node (key is in root .ssh): 

ssh capv@<worker_node_ip> 




### Arcas 1.1 TKGs WCP enablement
## TKGs

Network Setup:
```
Networks .3 .5 .7
.3 = Management
	vCenter 3.50
	Arcas79 3.39
	Avi.lab.local 3.40
	
	Avi mgt Start 3.60-69
	
	WCP mgt start 3.70-79
	
.5 = Frontend
	AVI VIP .5-60-89
	
.7 = Workload

	WCP workload - .7.100-119
	
Gateway = "192.168.3.1"
Gateway = "192.168.5.1"
Gateway = "192.168.7.1"

DNS = "10.197.79.7"
NTP = "10.128.152.81"
```


![Version](https://github.com/ogelbric/Arcas/blob/main/arcas11_TKGs_1.png)
![Version](https://github.com/ogelbric/Arcas/blob/main/arcas11_TKGs_2.png)
![Version](https://github.com/ogelbric/Arcas/blob/main/arcas11_TKGs_3.png)
![Version](https://github.com/ogelbric/Arcas/blob/main/arcas11_TKGs_4.png)
![Version](https://github.com/ogelbric/Arcas/blob/main/arcas11_TKGs_5.png)
![Version](https://github.com/ogelbric/Arcas/blob/main/arcas11_TKGs_6.png)
![Version](https://github.com/ogelbric/Arcas/blob/main/arcas11_TKGs_7.png)
![Version](https://github.com/ogelbric/Arcas/blob/main/arcas11_TKGs_8.png)
![Version](https://github.com/ogelbric/Arcas/blob/main/arcas11_TKGs_9.png)
![Version](https://github.com/ogelbric/Arcas/blob/main/arcas11_TKGs_10.png)
![Version](https://github.com/ogelbric/Arcas/blob/main/arcas11_TKGs_11.png)
![Version](https://github.com/ogelbric/Arcas/blob/main/arcas11_TKGs_12.png)
![Version](https://github.com/ogelbric/Arcas/blob/main/arcas11_TKGs_13.png)

WCP enablement:
```
cd  /opt/vmware/arcas/src

arcas --env vsphere --file /opt/vmware/arcas/src/vsphere-dvs-tkgs-wcp.json  --avi_configuration --avi_wcp_configuration --enable_wcp

```
Results:

![Version](https://github.com/ogelbric/Arcas/blob/main/arcas11_TKGs_14.png)


Get the kubectl-vsphere binaries from API endpoint:
```
cd /usr/local
wget --no-check-certificate https://192.168.5.62/wcp/plugin/linux-amd64/vsphere-plugin.zip
unzip vsphere-plugin.zip
```

![Version](https://github.com/ogelbric/Arcas/blob/main/arcas11_TKGs_15.png)

Log onto supervisor cluster:
```
kubectl-vsphere login --vsphere-username administrator@vsphere.local --server=https://192.168.5.62 --insecure-skip-tls-verify

```

KUBECTL_VSPHERE_PASSWORD environment variable is not set. Please enter the password below
Password: 
Logged in successfully.

You have access to the following contexts:
   192.168.5.62

If the context you wish to use is not in this list, you may need to try
logging in again later, or contact your cluster administrator.

To change context, use `kubectl config use-context <workload name>`
root@arcas79 [ /usr/local ]# 

```
kubectl config use-context 192.168.5.62

```
Switched to context "192.168.5.62".
```
kubectl get nodes

```
Output:

```
NAME                               STATUS   ROLES                  AGE    VERSION
42133bfc2b5aaf343a32dbce9200c435   Ready    control-plane,master   178m   v1.21.0+vmware.1-wcp
4213a81423b462db51d5f4a4b406d255   Ready    control-plane,master   178m   v1.21.0+vmware.1-wcp
4213ac7fd275d92df89b6cd2eed0e007   Ready    control-plane,master   3h2m   v1.21.0+vmware.1-wcp
```

Building the namespace (GUI): 

![Version](https://github.com/ogelbric/Arcas/blob/main/arcas11_TKGs_16.png)
![Version](https://github.com/ogelbric/Arcas/blob/main/arcas11_TKGs_17.png)
![Version](https://github.com/ogelbric/Arcas/blob/main/arcas11_TKGs_18.png)
![Version](https://github.com/ogelbric/Arcas/blob/main/arcas11_TKGs_19.png)
![Version](https://github.com/ogelbric/Arcas/blob/main/arcas11_TKGs_20.png)
![Version](https://github.com/ogelbric/Arcas/blob/main/arcas11_TKGs_21.png)
![Version](https://github.com/ogelbric/Arcas/blob/main/arcas11_TKGs_22.png)
![Version](https://github.com/ogelbric/Arcas/blob/main/arcas11_TKGs_231.png)
![Version](https://github.com/ogelbric/Arcas/blob/main/arcas11_TKGs_24.png)

There seems to be an issue with the Harbor enablement!

![Version](https://github.com/ogelbric/Arcas/blob/main/arcas11_TKGs_25.png)



Building the namespace (CMD line): 


```
arcas --env vsphere --file /opt/vmware/arcas/src/vsphere-dvs-tkgs-namespace.json --create_supervisor_namespace --create_workload_cluster --deploy_extensions

```

Result:

![Version](https://github.com/ogelbric/Arcas/blob/main/arcas11_TKGs_26.png)


Loggin onto guest workload cluster: 

```
kubectl-vsphere login --vsphere-username administrator@vsphere.local --server=https://192.168.5.62 --tanzu-kubernetes-cluster-namespace namespace1000 --tanzu-kubernetes-cluster-name workloadcluster1 --insecure-skip-tls-verify

```

```
Logged in successfully.

You have access to the following contexts:
   192.168.5.62
   namespace1000
   workloadcluster1

If the context you wish to use is not in this list, you may need to try
logging in again later, or contact your cluster administrator.

To change context, use `kubectl config use-context <workload name>`

root@arcas79 [ /usr/local ]# kubectl config use-context workloadcluster1    
Switched to context "workloadcluster1".
root@arcas79 [ /usr/local ]# kubectl get nodes
NAME                                            STATUS   ROLES                  AGE     VERSION
workloadcluster1-control-plane-v7f4x            Ready    control-plane,master   10m     v1.20.12+vmware.1
workloadcluster1-workers-ct6fp-bfb88d59-45bcp   Ready    <none>                 6m22s   v1.20.12+vmware.1
workloadcluster1-workers-ct6fp-bfb88d59-lk2qr   Ready    <none>                 6m28s   v1.20.12+vmware.1
	
```

	



TKGs YAML file for WCP enablement: 
```
{
    "envSpec": {
        "envType": "tkgs-wcp",
        "vcenterDetails": {
            "vcenterAddress": "vcenteravi.lab.local",
            "vcenterSsoUser": "administrator@vsphere.local",
            "vcenterSsoPasswordBase64": "Vk13YXJlMSE=",
            "vcenterDatacenter": "avi-Datacenter",
            "vcenterCluster": "avi-Cluster",
            "vcenterDatastore": "vsanDatastore",
            "contentLibraryName": "avi",
            "aviOvaName": "controller-20.1.7-9154"
        },
        "marketplaceSpec": {
            "refreshToken": ""
        },
        "saasEndpoints": {
            "tmcDetails": {
                "tmcAvailability": "false",
                "tmcRefreshToken": "",
                "tmcSupervisorClusterName": ""
            }
        },
        "infraComponents": {
            "dnsServersIp": "10.197.79.7",
            "searchDomains": "lab.local",
            "ntpServers": "10.128.152.81"
        }
    },
    "tkgsComponentSpec": {
        "controlPlaneSize": "MEDIUM",
        "aviMgmtNetwork": {
            "aviMgmtNetworkName": "DVPG-Management Network",
            "aviMgmtNetworkGatewayCidr": "192.168.3.1/24",
            "aviMgmtServiceIpStartRange": "192.168.3.60",
            "aviMgmtServiceIpEndRange": "192.168.3.69"
        },
        "aviComponents": {
            "aviPasswordBase64": "Vk13YXJlMSE=",
            "aviBackupPassphraseBase64": "Vk13YXJlMSE=",
            "enableAviHa": "false",
            "aviController01Ip": "192.168.3.40",
            "aviController01Fqdn": "avi.lab.local",
            "aviController02Ip": "",
            "aviController02Fqdn": "",
            "aviController03Ip": "",
            "aviController03Fqdn": "",
            "aviClusterIp": "",
            "aviClusterFqdn": "",
            "aviSize": "small",
            "aviCertPath": "",
            "aviCertKeyPath": ""
        },
        "tkgsVipNetwork": {
            "tkgsVipNetworkName": "DVPG-Frontend Network",
            "tkgsVipNetworkGatewayCidr": "192.168.5.1/24",
            "tkgsVipIpStartRange": "192.168.5.60",
            "tkgsVipIpEndRange": "192.168.5.89"
        },
        "tkgsMgmtNetworkSpec": {
            "tkgsMgmtNetworkName": "DVPG-Management Network",
            "tkgsMgmtNetworkGatewayCidr": "192.168.3.1/24",
            "tkgsMgmtNetworkStartingIp": "192.168.3.70",
            "tkgsMgmtNetworkDnsServers": "10.197.79.7",
            "tkgsMgmtNetworkSearchDomains": "lab.local",
            "tkgsMgmtNetworkNtpServers": "10.128.152.81"
        },
        "tkgsStoragePolicySpec": {
            "masterStoragePolicy": "pacific-gold-storage-policy",
            "ephemeralStoragePolicy": "pacific-gold-storage-policy",
            "imageStoragePolicy": "pacific-gold-storage-policy"
        },
        "tkgsPrimaryWorkloadNetwork": {
            "tkgsPrimaryWorkloadPortgroupName": "DVPG-Workload Network",
            "tkgsPrimaryWorkloadNetworkName": "workload1",
            "tkgsPrimaryWorkloadNetworkGatewayCidr": "192.168.7.1/24",
            "tkgsPrimaryWorkloadNetworkStartRange": "192.168.7.100",
            "tkgsPrimaryWorkloadNetworkEndRange": "192.168.7.119",
            "tkgsWorkloadDnsServers": "10.197.79.7",
            "tkgsWorkloadNtpServers": "10.128.152.81",
            "tkgsWorkloadServiceCidr": "10.96.0.0/22"
        }
    }
}
```

TKGs YAML namespace and work load cluster enablement

```
cat  /opt/vmware/arcas/src/vsphere-dvs-tkgs-namespace.json 
```
TKGs YAML 2:
```
{
    "envSpec": {
        "envType": "tkgs-ns",
        "vcenterDetails": {
            "vcenterAddress": "192.168.3.50",
            "vcenterSsoUser": "administrator@vsphere.local",
            "vcenterSsoPasswordBase64": "Vk13YXJlMSE=",
            "vcenterDatacenter": "avi-Datacenter",
            "vcenterCluster": "avi-Cluster"
        },
        "saasEndpoints": {
            "tmcDetails": {
                "tmcAvailability": "false",
                "tmcRefreshToken": "",
                "tmcSupervisorClusterName": ""
            },
            "tanzuObservabilityDetails": {
                "tanzuObservabilityAvailability": "false",
                "tanzuObservabilityUrl": "",
                "tanzuObservabilityRefreshToken": ""
            }
        }
    },
    "tkgsComponentSpec": {
        "tkgsWorkloadNetwork": {
            "tkgsWorkloadNetworkName": "workload1",
            "tkgsWorkloadPortgroupName": "",
            "tkgsWorkloadNetworkGatewayCidr": "",
            "tkgsWorkloadNetworkStartRange": "",
            "tkgsWorkloadNetworkEndRange": "",
            "tkgsWorkloadServiceCidr": ""
        },
        "tkgsVsphereNamespaceSpec": {
            "tkgsVsphereNamespaceName": "namespace1000",
            "tkgsVsphereNamespaceDescription": "",
            "tkgsVsphereNamespaceContentLibrary": "SubscribedAutomation-Lib",
            "tkgsVsphereNamespaceVmClasses": [
                "best-effort-medium",
                "best-effort-large",
                "best-effort-2xlarge",
                "best-effort-small"
            ],
            "tkgsVsphereNamespaceResourceSpec": {},
            "tkgsVsphereNamespaceStorageSpec": [
                {
                    "storagePolicy": "pacific-gold-storage-policy"
                }
            ],
            "tkgsVsphereWorkloadClusterSpec": {
                "tkgsVsphereNamespaceName": "namespace1000",
                "tkgsVsphereWorkloadClusterName": "workloadcluster1",
                "tkgsVsphereWorkloadClusterVersion": "v1.20.12+vmware.1-tkg.1.b9a42f3",
                "allowedStorageClasses": [
                    "pacific-gold-storage-policy"
                ],
                "defaultStorageClass": "pacific-gold-storage-policy",
                "nodeStorageClass": "pacific-gold-storage-policy",
                "serviceCidrBlocks": "10.96.0.0/12",
                "podCidrBlocks": "192.168.0.0/16",
                "controlPlaneVmClass": "best-effort-medium",
                "workerVmClass": "best-effort-medium",
                "workerNodeCount": "2",
                "enableControlPlaneHa": "false",
                "tkgWorkloadTsmIntegration": "false",
                "namespaceExclusions": {
                    "exactName": "",
                    "startsWith": ""
                }
            }
        }
    },
    "harborSpec": {
        "enableHarborExtension": "true",
        "harborFqdn": "harbor.lab.local",
        "harborPasswordBase64": "Vk13YXJlMSE=",
        "harborCertPath": "",
        "harborCertKeyPath": ""
    },
    "tanzuExtensions": {
        "enableExtensions": "false",
        "tkgClustersName": "",
        "logging": {
            "syslogEndpoint": {
                "enableSyslogEndpoint": "false",
                "syslogEndpointAddress": "",
                "syslogEndpointPort": "",
                "syslogEndpointMode": "",
                "syslogEndpointFormat": ""
            },
            "httpEndpoint": {
                "enableHttpEndpoint": "false",
                "httpEndpointAddress": "",
                "httpEndpointPort": "",
                "httpEndpointUri": "",
                "httpEndpointHeaderKeyValue": ""
            },
            "elasticSearchEndpoint": {
                "enableElasticSearchEndpoint": "false",
                "elasticSearchEndpointAddress": "",
                "elasticSearchEndpointPort": ""
            },
            "kafkaEndpoint": {
                "enableKafkaEndpoint": "false",
                "kafkaBrokerServiceName": "",
                "kafkaTopicName": ""
            },
            "splunkEndpoint": {
                "enableSplunkEndpoint": "false",
                "splunkEndpointAddress": "",
                "splunkEndpointPort": "",
                "splunkEndpointToken": ""
            }
        },
        "monitoring": {
            "enableLoggingExtension": "false",
            "prometheusFqdn": "",
            "prometheusCertPath": "",
            "prometheusCertKeyPath": "",
            "grafanaFqdn": "",
            "grafanaCertPath": "",
            "grafanaCertKeyPath": "",
            "grafanaPasswordBase64": ""
        }
    }
}
```



# Service Installer for VMware Tanzu (Project Arcas 1.0)

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


#### TKGs json file example

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

### Deploy from JSON file:
```
arcas --env vsphere --file /opt/vmware/arcas/src/vsphere.json --avi_configuration --tkg_mgmt_configuration
```

### Follow in the log:
```
journalctl -u arcas.service --follow
```

### Deploy the rest of the clusters:
```
arcas --env vsphere --file /opt/vmware/arcas/src/vsphere.json --avi_configuration --tkg_mgmt_configuration --shared_service_configuration --workload_preconfig --workload_deploy
```
### Result from Arcas deploy

![Version](https://github.com/ogelbric/Arcas/blob/main/tkgm14.png)


### Commands for the below output and adding the harbor IP to DNS
```
kubectl config get-contexts
kubectl config use-context sharedtkg1-admin@sharedtkg1
kubectl get svc -A
kubectl get httpproxy -A
```

![Version](https://github.com/ogelbric/Arcas/blob/main/tkgm15.png)

### DNS

![Version](https://github.com/ogelbric/Arcas/blob/main/tkgm16.png)

### TKGm json file example

```
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
            "avi-ova-name": "controller-21.1.2-9124",
            "resource-pool-name": ""
        },
        "env-type": "tkgm",
        "marketplace-spec": {
            "refresh-token": ""
        },
        "custom-repository-spec": {
            "tkg_custom_image_repository": "",
            "tkg_custom_image_repository_public_ca_cert": ""
        },
        "saas-endpoints": {
            "tmc-details": {
                "tmc-availability": "false",
                "tmc-refresh-token": ""
            },
            "tanzu-observability-details": {
                "tanzu-observability-availability": "false",
                "tanzu-observability-url": "",
                "tanzu-observability-refresh-token": ""
            }
        },
        "infra-components": {
            "dns-servers-ip": "192.168.1.7",
            "ntp-servers": "10.128.152.81",
            "search_domains": "lab.local"
        },
        "proxy-spec": {
            "arcas-vm": {
                "enable-proxy": "false",
                "http-proxy": "",
                "https-proxy": "",
                "no-proxy": ""
            },
            "tkg-mgmt": {
                "enable-proxy": "false",
                "http-proxy": "",
                "https-proxy": "",
                "no-proxy": ""
            },
            "tkg-sharedservice": {
                "enable-proxy": "false",
                "http-proxy": "",
                "https-proxy": "",
                "no-proxy": ""
            },
            "tkg-workload": {
                "enable-proxy": "false",
                "http-proxy": "",
                "https-proxy": "",
                "no-proxy": ""
            }
        }
    },
    "tkg-component-spec": {
        "avi-mgmt-network": {
            "avi-mgmt-network-name": "DVPG-Management Network",
            "avi-mgmt-network-gateway-cidr": "192.168.1.1/24",
            "avi-mgmt-service-ip-startrange": "192.168.1.60",
            "avi-mgmt-service-ip-endrange": "192.168.1.70"
        },
        "tkg-cluster-vip-network": {
            "tkg-cluster-vip-network-name": "DVPG-Frontend Network",
            "tkg-cluster-vip-network-gateway-cidr": "192.168.4.1/24",
            "tkg-cluster-vip-ip-startrange": "192.168.4.70",
            "tkg-cluster-vip-ip-endrange": "192.168.4.100"
        },
        "avi-components": {
            "avi-password-base64": "Vk13YXJlMSE=",
            "avi-backup-passphrase-base64": "Vk13YXJlMSE=",
            "avi-controller01-ip": "192.168.1.40",
            "avi-controller01-fqdn": "avi.lab.local"
        },
        "tkg-mgmt-components": {
            "tkg-mgmt-network-name": "DVPG-Management Network",
            "tkg-mgmt-gateway-cidr": "192.168.1.1/24",
            "tkg-mgmt-cluster-name": "tkgmgt1",
            "tkg-mgmt-size": "medium",
            "tkg-mgmt-deployment-type": "dev",
            "tkg-mgmt-cluster-cidr": "100.96.0.0/11",
            "tkg-mgmt-service-cidr": "100.64.0.0/13",
            "tkg-mgmt-base-os": "photon",
            "tkg-sharedservice-cluster-name": "sharedtkg1",
            "tkg-sharedservice-size": "large",
            "tkg-sharedservice-deployment-type": "dev",
            "tkg-sharedservice-worker-machine-count": "1",
            "tkg-sharedservice-cluster-cidr": "100.96.0.0/11",
            "tkg-sharedservice-service-cidr": "100.64.0.0/13",
            "tkg-sharedservice-base-os": "photon",
            "tkg-sharedservice-kube-version": "v1.21.2"
        }
    },
    "tkg-mgmt-data-network": {
        "tkg-mgmt-data-network-name": "DVPG-Management Network",
        "tkg-mgmt-data-network-gateway-cidr": "192.168.1.1/24",
        "tkg-mgmt-avi-service-ip-startrange": "192.168.1.80",
        "tkg-mgmt-avi-service-ip-endrange": "192.168.1.100"
    },
    "tkg-workload-data-network": {
        "tkg-workload-data-network-name": "DVPG-Workload Network",
        "tkg-workload-data-network-gateway-cidr": "192.168.5.1/24",
        "tkg-workload-avi-service-ip-startrange": "192.168.5.70",
        "tkg-workload-avi-service-ip-endRange": "192.168.5.100"
    },
    "tkg-workload-components": {
        "tkg-workload-network-name": "DVPG-Workload Network",
        "tkg-workload-gateway-cidr": "192.168.5.1/24",
        "tkg-workload-cluster-name": "worktkg1",
        "tkg-workload-size": "medium",
        "tkg-workload-deployment-type": "dev",
        "tkg-workload-worker-machine-count": "1",
        "tkg-workload-cluster-cidr": "100.96.0.0/11",
        "tkg-workload-service-cidr": "100.64.0.0/13",
        "tkg-workload-base-os": "photon",
        "tkg-workload-kube-version": "v1.21.2",
        "tkg-workload-tsm-integration": "false",
        "namespace-exclusions": {
            "exact-name": "",
            "starts-with": ""
        }
    },
    "harbor-spec": {
        "enable-harbor-extension": "true",
        "harbor-fqdn": "harbor.lab.local",
        "harbor-password-base64": "Vk13YXJlMSE=",
        "harbor-cert-path": "",
        "harbor-certkey-path": ""
    },
    "tanzu-extensions": {
        "enable-extensions": "false",
        "tkg-clusters_name": "",
        "logging": {
            "syslog_endpoint": {
                "enable_syslog_endpoint": "false",
                "syslog_endpoint_address": "",
                "syslog_endpoint_port": "",
                "syslog_endpoint_mode": "",
                "syslog_endpoint_format": ""
            },
            "http_endpoint": {
                "enable_http_endpoint": "false",
                "http_endpoint_address": "",
                "http_endpoint_port": "",
                "http_endpoint_uri": "",
                "http_endpoint_header_key_value": ""
            },
            "elastic_search_endpoint": {
                "enable_elastic_search_endpoint": "false",
                "elastic_search_endpoint_address": "",
                "elastic_search_endpoint_port": ""
            },
            "kafka_endpoint": {
                "enable_kafka_endpoint": "false",
                "kafka_broker_service_name": "",
                "kafka_topic_name": ""
            },
            "splunk_endpoint": {
                "enable_splunk_endpoint": "false",
                "splunk_endpoint_address": "",
                "splunk_endpoint_port": "",
                "splunk_endpoint_token": ""
            }
        },
        "monitoring": {
            "enable-logging-extension": "false",
            "prometheus-fqdn": "",
            "prometheus-cert-path": "",
            "prometheus-certkey-path": "",
            "grafana-fqdn": "",
            "grafana-cert-path": "",
            "grafana-certkey-path": "",
            "grafana-password-base64": ""
        }
    }
}
```


