# Factory reset prodecure

## Soft reset

Een soft reset schoont de running- en startup-config op. Alle commando's moeten vanuit de privileged exec mode worden uitgevoerd tenzij anders aangegeven.

1. Herlaad de router/switch na de aanpassingen met het commando `reload`.

1. Verwijderen van startup config (dit commando verandert niets aan de boot variabelen, zoals config-register en boot system settings).

    ```
    erase startup-config
    ```

    Of

    ```
    write erase
    ```

## Hard reset

Een hard reset is nodig wanneer je het wachtwoord van het apparaat niet meer kent.

1. Schakel de router/switch uit door deze uit het stopcontact te halen.

1. Sluit de console kabel aan en stel een console verbinding op.

1. Hou de `mode` knop ingedrukt en steek de stekker opnieuw in het stopcontact. Laat de `mode` knop pas los eens er karakters worden weergegeven op het scherm.

1. Terwijl het bootproces bezig is, voer je de toetsencombinatie `Ctrl+Pausebreak` in.

1. Voer volgende commando's in:

    ```
    Switch: flash_init
    Switch: dir flash:
    Switch: flash:config.text flash:config.backup
    Switch: boot
    ```

1. Hernoem de configuratie files en verwijder de wachtwoorden

    ```
    Would you like to enter the inital configuration dialog? no
    Switch> enable
    SW1# renameflash:config.backup config.text
    SW1# copy flash:config.text system:running-config
    SW1# config terminal
    SW1(config)# no enable secret.
    SW1(config)# exit
    SW1(config)# wr
    ```

## Appendix

1. Boot variabelen kunnen gewijzigd worden met het `boot` commando vanuit global configuration mode.

1. Het configuratie register kan aangepast worden met het `config-register`. (Werkt niet in packet tracer)

### Reset VLAN information

1. Controleer de vlan informatie met het commando `show vlan`.

1. Controleer de vlan.dat file met het commando `dir`.

1. Delete de VLAN.dat file met het commando `delete flash:vlan.dat`.
