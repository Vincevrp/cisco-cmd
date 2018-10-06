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
