# How to create a Switch with NAT enabled in Hyper-V

## No GUI way!!!

```
New-VMSwitch -Name NATNET -SwitchType Intern

Get-NetAdapter
#to find $switchID

New-NetIPAddress -IPAddress 172.17.0.1 -PrefixLength 16 -InterfaceIndex $switchId
```

* #### use this net in your vms and be happy :)

* #### Hyper-V has no build in DHCP for simple setups :(
