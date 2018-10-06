# Cisco IOS Basic

## Modus veranderen

### Commando modes
Wanneer je connecteert met een apparaat, kom je in USER EXEC mode:

Voorbeeld prompt:
```
Switch>
```

Schakelen naar de PRIVILEGED EXEC mode met het commando `enable`:

```
Switch> enable
Switch#
```

Terugschakelen naar USER EXEC mode kan met het commando `disable`.

### Configuratie modes

We onderscheiden volgende configuratie modes:

| Modus                        | Commando           | Prompt               |
| :----                        | :-------           | ------               |
| Global configuration mode    | configure terminal | Switch(config)#      |
| Line configuration mode      | line console 0     | Switch(config-line)# |
| Interface configuration mode | interface vlan 1   | Switch(config-if)#   |

Voor line en interface configuration mode te gebruiken dien je te vertrekken vanuit global configuration mode en de corresponderende line/interface mee te geven met het commando.

Om een bepaalde modus te verlaten gebruiken we het commando `exit`.

## Basisconfiguratie

### Naam instellen

Uit te voeren in global configuration mode:

```
hostname naam-van-apparaat
```

### Wachtwoorden instellen

#### Privileged exec mode wachtwoord:

Uit te voeren in privileged exec mode:

```
enable secret wachtwoord
```

#### Wachtwoord voor bepaalde lijn:

Uit te voeren in line configuration mode voor respectievelijke line:

```
password wachtwoord
login
```
Het login commando zorgt ervoor dat het wachtwoord gevraagd wordt bij het verbinden met het apparaat.


#### Alle wachtwoorden encrypteren
Uit te voeren in privileged exec mode:

```
service password-encryption
```

### Banner instellen

Bij het instellen van een banner moet je steeds een symbool kiezen dat zal dienen als begin- en eindmarkering voor de banner. In onderstaande voorbeelden maken wij gebruik van het dollar-teken ($)

Uit te voeren in global configuration mode:

```
banner motd $ your-text-message $
```

#### Voorbeeld enkele regel:

```
banner motd $ Warning, no unautohrized access allowed! $
```

#### Voorbeeld meerdere regels:

Merk op dat de '{ENTER}' duidt op het fysiek indrukken van de enter-toets

```
banner motd ${ENTER}
############################################{ENTER}
# Warning, no unauthorized access allowed! #{ENTER}
############################################{ENTER}
${ENTER}
```

### IP-adres instellen

Uit te voeren in interface configuration mode voor respectievelijke interface:

```
ip address ip subnetmask
```

Bijvoorbeeld:

```
ip address 0.0.0.0 255.255.255.0
```

### Klok en datum instellen

#### Klok tonen

Kan worden uitgevoerd vanuit user exec mode:
```
show clock
```

#### Klok instellen

Moet worden uitgevoerd vanuit privileged exec mode:
```
clock set tijd maand dag jaar
```

Extra informatie kan worden getoond door het commando `clock set ?`.

### Descriptie interface instellen

Uit te voeren in interface configuration mode voor respectievelijke interface:

```
description beschrijving
```

### Interface inschakelen

Uit te voeren in interface configuration mode voor respectievelijke interface:

```
no shutdown
```

### Configuratie opslaan

Uit te voeren in privileged exec mode:

```
copy running-config startup-config
```

## Hardware en software info tonen

```
show version
```

## IP-lookup uitschakelen

Af en toe komt het voor dat je een commando verkeerd intypt, waardoor de router/switch automatisch een IP-lookup probeert te doen. Dit kan uitgeschakeld worden door:

```
no ip domain-lookup
```
