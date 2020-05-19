# vswitch trunk - vswitches are not just cables

goal is to ping on vlan 50 between the vms


```
                             via private vswitch
+------------------------+                          +-----------------------+
|  centos1               |                          | centos2               |
|                        |      untagged            |                       |
|  eth0    172.30.0.1/24 |--------------------------| eth0    172.30.0.2/24 |
|                        |                          |                       |
|  eth0.50 10.55.55.1/24 |--------------------------| eth0.50 10.55.55.2/24 |
+------------------------+      tagged vlan 50      +-----------------------+                                                   
```


```
PS C:\WINDOWS\system32> get-VMNetworkAdapterVlan

VMName       VMNetworkAdapterName Mode     VlanList
------       -------------------- ----     --------
centos7-1    Netzwerkkarte        Untagged
centos7-2    Netzwerkkarte        Untagged

PS C:\WINDOWS\system32> Set-VMNetworkAdapterVlan -Trunk -AllowedVlanIdList "50" -VMName "centos7-1" -VMNetworkAdapterName "Netzwerkkarte" -NativeVlanId 0
PS C:\WINDOWS\system32> Set-VMNetworkAdapterVlan -Trunk -AllowedVlanIdList "50" -VMName "centos7-2" -VMNetworkAdapterName "Netzwerkkarte" -NativeVlanId 0

PS C:\WINDOWS\system32> Get-VMNetworkAdapterVlan

VMName       VMNetworkAdapterName Mode     VlanList
------       -------------------- ----     --------
centos7-1    Netzwerkkarte        Trunk    0,50
centos7-2    Netzwerkkarte        Trunk    0,50
```
