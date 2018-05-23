# Netwerken II

## Chapter 1

### IPv4 instellen

Interface configuration mode:

> ip address *ip-address* *subnetmask*

> no shutdown

Verificatie:

> show ip interface brief

### IPv6 instellen

Interface configuration mode:

> ipv6 address *ip-address* / *prefix-length* [link-local | eul-64]

> no shutdown

Genereer link-local adres:

> ipv6 enable

Stel eigen static link-local adres in:

Dit wordt gebruikt i.p.v. gegenereerd link-local adres.

> ipv6 address *ip-address* / *prefix-length* link-local

Verificatie:

> show ipv6 interface brief

## Chapter 2

### IPv4 static routes

Global configuration mode:

> ip route *network-address* *subnet-mask* [ *ip-address* | *exit-int* ]

Static route

> ip route *network-address* *subnet-mask* [ *next-hop-ip* | *exit-intf* ]

Fully specified static route

> ip route *network-address* *subnet-mask* *exit-intf* *next-hop-ip*

Directly connected static route

> ip route *network-address* *subnet-mask* *exit-intf*

Default route

> ip route 0.0.0.0 0.0.0.0 [*exit-intf* | *next-hop-ip*]

Verificatie:

> show ip route *static*

### IPv6 static routes

The ipv6 unicast-routing global configuration command must be configured to enable the router to forward IPv6 packets

> ipv6 route *ipv6-prefix/prefix-length [ ipv6 address | exit-int ]*

Default static route

> ipv6 route ::/0 [ipv6-address | exit-intf]

Enable IPv6 unicast-routing

> ipv6 unicast-routing

Verificatie:

> show ipv6 route *static*

### Floating static routes

Aanschouw volgende administrative distance waarden:

* EIGRP = 90
* IGRP = 100
* OSPF = 110
* IS-IS = 115
* RIP = 120

IPv4:

> ip route 0.0.0.0 0.0.0.0 value

IPv6:

> ipv6 route 0.0.0.0 0.0.0.0 value

## Chapter 3

## Router RIP configuration mode

Enable RIP (v1)

> router rip

Switch to RIPv2

> version 2

Enable RIP routing for network:

> network *network-address*

Disable auto-summary

> no auto-summary

Passive interface

> passive-interface *int-name*

Propagate default route

> default-information originate

Verificatie:

> show ip protocols

## Chapter 5

### SSH

Global configuration mode:

> ip domain-name cisco
> crypto key generate rsa
> username admin secret ccna
> line vty 0 15
> transport input ssh
> login local
> exit
> ip ssh version 2
> exit

### Port security

Disable unused ports

> interface range fa0/1-9
> shutdown

Configure port security

> switchport port-security mac-address *mac-addr*

Sticky

> switchport port-security mac-address sticky *mac-addr*

Violation modes

* **Protect**: When limit of secure MAC is reached, drop packets with unknown source address.
* **Restrict**: Same as protect but with notification
* **Shutdown** (default): Violation causes interface to shutdown

> switchport port-security violation [ protect | restrict | shutdown ]

Verificatie:

> show port-security interface *[interface-id]*
> show port-security address

## Chapter 6

### VLANs

VLAN types:

* **Default**: All switch ports become part of default VLAN to allow any device to connect with other devices.
* **Native**: Is assigned to a trunk port. It supports traffic coming from many VLANs.
* ...

VLAN maken

```
configure terminal
vlan 20
name student
end
```

Assign ports to VLAN

```
configure terminal
interface *interface_id*
switchport mode access
switchport access vlan *vlan_id*
end
```

Assign ip to VLAN
```
int vlan *nummer*
ip add *ip* *sub*
no shutdown
exit
ip default-gateway *ip*
```

Set VTP

```
vtp domain *naam*
```

Voice VLAN

```
switchport voice vlan *vlan_id*
```

Configure Trunk Links

```
configure terminal
interface *interface_id*
switchport mode trunk
switchport trunk native vlan *vlan_id*      #Specify a native VLAN for untagged frames
switchport trunk allowed vlan *vlan-list*   #Specify list of VLANs to be allowed on trunk link
end
```

Configure router-on-a-Stick subinterface configuration

```
interface g0/0.10
encapsulation dot1q 10
ip address 172.17.10.1 255.255.255.0

interface g0/0
no shutdown

vlan 10
interface f0/5
switchport mode trunk
end
```

Verificatie

> show vlan brief
> show interfaces f0/18 switchport

## Chapter 7

### ACL

Types:

* **Inboud ACL**: Incoming packets are processed before they are routed to the outbound interface
* **Outbound ACL**: Incoming packets are routed to the outbound interface, and then they are processed through the outbound ACL.

#### Wildcard masking

Neem 255.255.255.255 en trek er de subnetmask van af

Binary:

    0 = match the value
    1 = ignore the value

Voorbeelden:

    IP-Address  192.168.1.1

    IP must match exactly:

        Wildcard mask 0.0.0.0

    Anything will match:

        Wildcard mask 255.255.255.255

ACL instellen

> access-list access-list-number { deny | permit | remark } source [ source-wildcard ] [ log ]

ACL toevoegen aan interface

> ip access-group { access-list-number | access-list-name } { in | out }

ACL voor SSH

    line vty 0 15
    login local
    transport input ssh
    access-class 21 in
    exit

Verificatie:

> show access-lists
