---
title: Virtualbox host and guest network
description: Change host network from one routher enviorment to another no impact the connectivity 
categories:
 - VM
tags:
 - Virtualbox
 - Network
---

> Virtualbox host and guest network

## Versions

 - Virtualbox 5.2
 - Ubuntu 16
 - Ubuntu 18

## Problem and Solution

### Issues

- Once the VM setup, if chose network adapter "Bridged Adapter" we can easily get network between host and guest, and also access internet inside guest.
- But when we change the laptop from one WIFI network (DHCP) to another network (DHCP), the guest IP will have problem if we still use Bridged Adapter network, as we may referring one guest IP (database guest server) in another guest (app guest server).


### Solutions

To solve this problem we need two different network cards for the Virtualbox guest, one "NAT Adapter" network adapter allow guest access external network, and one "Host-only Adapter" to allow guest access other guests and host access this guest.



Config example for Ubuntu 18

1. Open Settings for the VirtualBox VM 
2. Open network, enable one Adapter and select Attached to "Host-only Adapter"
3. Re-generate the MAC Address for this adapter
4. Enable second Adapter and select attached to "NAT"
5. Re-generate the MAC Address for this adapter
6. Start the VM and check the network config by ifconfig -a | more
7. Check the network been config in Ubuntu interfaces, if not need add it and then apply the changes

```bash
root@hank:~# cat /etc/netplan/*.yaml
# This file is generated from information provided by
# the datasource.  Changes to it will not persist across an instance.
# To disable cloud-init's network configuration capabilities, write a file
# /etc/cloud/cloud.cfg.d/99-disable-network-config.cfg with the following:
# network: {config: disabled}
network:
    ethernets:
        enp0s3:
            addresses: []
            dhcp4: true
        enp0s8:
            addresses: []
            dhcp4: true
        enp0s9:
            addresses: []
            dhcp4: true
    version: 2
root@hank:~# sudo netplan apply

```

Config example for Ubuntu 16

1. Open Settings for the VirtualBox VM 
2. Open network, enable one Adapter and select Attached to "Host-only Adapter"
3. Re-generate the MAC Address for this adapter
4. Enable second Adapter and select attached to "NAT"
5. Re-generate the MAC Address for this adapter
6. Start the VM and check the network config by ifconfig -a | more
7. Check the network been config in Ubuntu interfaces, if not need add it and then apply the changes

```bash
root@ubuntu16:~# cat /etc/network/interfaces
# This file describes the network interfaces available on your system
# and how to activate them. For more information, see interfaces(5).

source /etc/network/interfaces.d/*

# The loopback network interface
auto lo
iface lo inet loopback

# The primary network interface
auto enp0s3
iface enp0s3 inet dhcp

auto enp0s8
iface enp0s8 inet dhcp

auto enp0s9
iface enp0s9 inet dhcp
root@ubuntu16:~# sudo reboot
```

Now we can access to each other
1. From guest to other guests
2. From host to guests
3. From guest to internet