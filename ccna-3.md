# Netwerken 3 Commando's

## VLAN

## VTP

VTP Server

```
vtp mode server
vtm domain ?
```

VTP Client
```
vtp mode client
vtp domain ?
```

### Verificatie

```
show vtp status
```

```
show vlan brief
```

## DTP

### Verificatie

```
show dtp interface f0/1
```

## STP

```
config-if
spanning-tree mode ?
spanning-tree vlan 1,10,20 root primary
spanning-tree portfast
spanning-tree bpduguard enable
```

### Verificatie
```
show cdp neighbors
show spanning-tree vlan
```

## L3 Inter VLAN routing

```
int g0/2
no switchport
ip addr ip sub
```

Enable routing:

```
ip routing
```

## NTP

```
clock set
ntp server in
```

## CDP

```
show cdp (interface/neighbours)
cdp enable
```

## Etherchannel

```
interface range Fa0/1-2
channel-group 1 mode active/desirable
interface port-channel 1
switchport mode trunk
switchport trunk allowed vlan 1,2,20

show interfaces port-channel 1
show etherchannel summary
show etherchannel port-channel
```

LACP: active/passive
PagP: desirable/auto

## HSRP

```
interface
standy version 2
standby 1 ip
standby 1 priority 100
standby 1 preempt
no shut
```

### Verificatie

```
show standby brief
```

## OSPF

```
router ospf 10
router-id
network x.x.x.x wildcardmask area area-id
passive-interface gigabitethernet 0/0
```

```
clear ip ospf process
show ip protocols
show ospf interface serial 0/0/0
show ip ospf neighbor
```

### OSPFv3

```
ipv6 unicast routing
router-id 1.1.1.1
ipv6 ospf area
```

```
clear ipv6 ospf process
```

## EIGRP

```
router eigrp 1
eigrp router-id
network network-addr wildcardmask
```

### Configure passive interfaces

```
router eigrp 1
passive-interface gigabitethernet 0/0
```

### Verificatie

```
show ip protocols
show ip eigrp neighbors
show ip eigrp topology
show running-config | section eigrp 1
```

## EIGRPv6

```
ipv6 unicast-routing
ipv6 router eigrp 2
eigrp router-id 2.0.0.0
no shutdown
```

### Configure passive interfaces

```
ipv6 router eigrp 2
passive-interface gigabitethernet 0/0
```

### Verificatie

```
show ipv6 protocols
show ipv6 eigrp neighbors
show ipv6 route
```
