# Igang med Home Automation

Når du går hjem idag vil du kunne installere Home Assistant, opsætte Wifi på Home assistant.

Du vil også have integreret Home Assistant med en ESP Chip, vi vil have lavet noget basis automatisering så du kan se hvorfor netop Home Assistant giver værdi til dit hjem.

Du vil have prøvet at integrere ZigBee via en [CC2531 USB Dongle](https://mackabler.dk/sonoff-zigbee-cc2531-usb-dongle-3685.html?utm_source=adtraction&utm_medium=affiliate&utm_campaign=adtraction&at_gd=2687A5538131C3E8D2671FD36774C1014EAF1F91)

**BEMÆRK** - Den dongle du køber skal have rigtig firmware, dem på ovenstående link er flashed med korrekt firmware fra fabrikken. Det er også muligt at købe dem via AliExpress, men pas på du får den rigtige.

# Home Assistant
Home Assistant er bygget i Python og kan køre på alle aktuelle linux distributioner, det er dog ikke anbefalet at installere Home Assistant i hånden med mindre man er udvikler, der findes mange meget bedre løsninger.

Jeg bruger og anbefaler Home Assistant fordi systemet har en tilpas grad af muligheder samt brugervenlighed, og jeg ved projektet er meget fokuseret på at det stadigvæk skal kunne alle de lækre ting, men der er enormt meget fokus på det også skal være brugervenligt. For bare 2 år siden skulle man næsten lave alt i YAML filer, og der var stort set ingen automatisering i Web Interfacet.

## Installations metoder

Der er 4 måder man kan installere Home Assistant på og vi vil følge den 1. som jeg vil anbefale

1. Home Assistant Operating System

   * En pakke der indeholder det hele, som er tilgængelig til Raspberry og Intel NUC
2. Home Assistant Container

   * Et Docker Image som indeholder Home Assistant Core
3. Home Assistant Supervised

   * Den gamle måde at installere det på - der var en komponent der holdt styr på filerne og opdateringer etc.
4. Home Assistant Core
   
   * Installation direkte via Python (Typisk kun til udviklere)

# Installation af HomeAssistant

Når vi skal installere Home Assistant skal vi bruge et Image til vores Raspberry, der findes en [vejledning](https://www.home-assistant.io/installation/raspberrypi) på HomeAssistant's hjemmeside men herunder vil vi gå punkterne igennem

Det image som HomeAssistant stiller til rådighed hedder i daglig tale HassOS (Home Assistant Operating System) som er et speciel image der indeholder alle nødvendige pakker og som er bygget op med best practice.

## Flash tool

Vi kan bruge [balenaEtcher](https://www.balena.io/etcher/) til at flashe din firmware, og du kan enten downloade filen eller indsætte en URL direkte i programmet.

### Flash from URL
![1-etcher-1.png](https://github.com/zenturacp/hass-kursus/raw/main/Screenshots/1-etcher-1.png)

### Indsæt URL til Firmware
![1-etcher-2.png](https://github.com/zenturacp/hass-kursus/raw/main/Screenshots/1-etcher-2.png)

### Vælg Enhed
![1-etcher-3.png](https://github.com/zenturacp/hass-kursus/raw/main/Screenshots/1-etcher-3.png)
![1-etcher-4.png](https://github.com/zenturacp/hass-kursus/raw/main/Screenshots/1-etcher-4.png)

### Tryk Flash
*Det kan tage op til 10 minutter alt efter hvor hurtig din internet forbindelse er*

![1-etcher-5.png](https://github.com/zenturacp/hass-kursus/raw/main/Screenshots/1-etcher-5.png)

### Færdig
Hvis alt virker vil du få denne skærm frem når du er færdig.

![1-etcher-6.png](https://github.com/zenturacp/hass-kursus/raw/main/Screenshots/1-etcher-6.png)

Nu er din Raspberry klar til at starte 1. gang - for at komme til den Wizard som man sætter HomeAssistant op fra skal man forbinde via Ethernet, hvorfra man så kan sætte Wifi op.

*Bemærk der kan godt gå op til 20 minutter før den er klar - der sker en del opsætning 1. gang den starter op*

## Første opstart

Du har flere måder du kan åbne den på enten via IP eller via mDNS (Virker primært på Mac og Linux), jeg anbefaler Windows brugere at bruge IP adressen.

DNS Navn: http://homeassistant.local:8123

IP Adresse: http://(findip fra DHCP Server):8123 f.eks. http://192.168.1.120:8123

### Opstarts Billede
Når du starter den 1. gang vil der blive installeret alt der skal bruges - dette kan tage op til 20 minutter på en langsom Raspberry
![2-hass-1.png](https://github.com/zenturacp/hass-kursus/raw/main/Screenshots/2-hass-1.png)

### Oprette bruger
Du skal oprette dig som bruger når du logger på 1. gang, det er vigtigt at du laver en kode som er komplex hvis du på sigt skal sætte din Home Assistant på Internettet
![2-hass-2.png](https://github.com/zenturacp/hass-kursus/raw/main/Screenshots/2-hass-2.png)

### Placering
Du skal sætte en placering, det er vigtigt denne er korrekt og er der hvor dit device er, dette bruges blandt andet til at beregne hvor solen står i forhold til hvor du er.
![2-hass-3.png](https://github.com/zenturacp/hass-kursus/raw/main/Screenshots/2-hass-3.png)

### Diagnistics Data
Der er helt sikkert en masse holdninger til dette - jeg anbefaler man deler med udviklerne, de levere trods alt et gratis produkt, og jeg er ret sikker på man ikke kommer til at have GDPR data her :-) Men som sagt, så er det helt op til jer selv.
![2-hass-4.png](https://github.com/zenturacp/hass-kursus/raw/main/Screenshots/2-hass-4.png)

### Tryk Afslut
![2-hass-5.png](https://github.com/zenturacp/hass-kursus/raw/main/Screenshots/2-hass-5.png)

### Hjemmeskærm
Her kan du med fordel trykke Ja - så du ikke skal logge ind
![2-hass-6.png](https://github.com/zenturacp/hass-kursus/raw/main/Screenshots/2-hass-6.png)

## Wifi Opstæning
Det anebfales ikke man køre sin Home Assistant via Wifi, f.eks. hvis man vil lave noget automatisering på sigt der kan styre dit wifi, så er det ikke et så smart initiativ, og der er ingen problemer i at sætte sin Home Assistant direkte på din router. Men hvis du alligevel vil denne vej er der en guide her

### Gå ind i Supervisor
![3-hasswifi-1.png](https://github.com/zenturacp/hass-kursus/raw/main/Screenshots/3-hasswifi-1.png)

### Gå over i System
Tryk Ændre under IPV4
![3-hasswifi-2.png](https://github.com/zenturacp/hass-kursus/raw/main/Screenshots/3-hasswifi-2.png)

### Vælg WLAN0
Sæt IPV4 til enten DHCP eller Fast IP

Under Wifi vælg Scan for Adgangspunkter
![3-hasswifi-3.png](https://github.com/zenturacp/hass-kursus/raw/main/Screenshots/3-hasswifi-3.png)

### Vælg det Wifi du vil forbinde til og udfyld kode i WPA-PSK og tryk GEM
**OBS! Du vil få ny IP adresse på WLAN0 interface**
![3-hasswifi-4.png](https://github.com/zenturacp/hass-kursus/raw/main/Screenshots/3-hasswifi-4.png)


# Gennemgang af Interface
* Hjemmeskærm
  * Start siden - med Tabs
* Kort
  * Hvis man har lokations tjenester kan man følge personer / ting på kortet
* Logbog
  * En log bog med handlinger
* Historik
  * Historiske data f.eks. temperatur sensor data historik
* Mediebrowser
  * Ja - bruger den ikke rigtig - Home Assistant er ikke et medie center!
* Udviklerværktøjer
  * Hvis du vil ned i maven på systemet
* Supervisor
  * Opdateringer / Plugins styres herfra
* Indstillinger
  * Hvis du vil ændre opsætningen på din Home Assisiant er det her det foregår
* Notifikationer
  * Info til dig - lidt som et "besked" system fra systemet

# Installation af Zigbee
Zigbee - er den protokol som Philips Hue og Ikea Trådfri bruger, vi har mulighed for at tale direkte med en Trådfri pære via Home Assistant, uden at have en Ikea Gateway.

Det er faktisk også muligt at bibeholde sin eksisteren [Ikea Trådfri](https://www.home-assistant.io/integrations/tradfri/) eller [Philips Hue](https://www.home-assistant.io/integrations/hue/) via Integrations hvis man allerede har en nuværende løsning kørende. Man vil have præcis samme muligheder via de integrationer som at tilføje enhederne direkte via en USB nøgle.

## Installation af Zigbee dongle (ZHA)
Det er muligt at købe en [CC2531 USB Dongle](https://mackabler.dk/sonoff-zigbee-cc2531-usb-dongle-3685.html?utm_source=adtraction&utm_medium=affiliate&utm_campaign=adtraction&at_gd=2687A5538131C3E8D2671FD36774C1014EAF1F91) som er direkte kompatibel med Home Assistants integration der hedder [ZHA](https://www.home-assistant.io/integrations/zha/).

### Åben Indstillinger
Og klik på Integrationer
![4-hasszha-1.png](https://github.com/zenturacp/hass-kursus/raw/main/Screenshots/4-hasszha-1.png)

### Vælg Tilføj Integration
![4-hasszha-2.png](https://github.com/zenturacp/hass-kursus/raw/main/Screenshots/4-hasszha-2.png)

### Søg efter ZHA og tryk på **>**
![4-hasszha-3.png](https://github.com/zenturacp/hass-kursus/raw/main/Screenshots/4-hasszha-3.png)

### Vælg den serial port der indeholder CC2531 (Dette er navn på Chippen fra Texas Instruments)
Og tryk Send og Afslut
![4-hasszha-4.png](https://github.com/zenturacp/hass-kursus/raw/main/Screenshots/4-hasszha-4.png)
![4-hasszha-5.png](https://github.com/zenturacp/hass-kursus/raw/main/Screenshots/4-hasszha-5.png)
![4-hasszha-6.png](https://github.com/zenturacp/hass-kursus/raw/main/Screenshots/4-hasszha-6.png)

### Nu er integrationen på plads
Du kan nu gå igang med at pare dine enheder
![4-hasszha-7.png](https://github.com/zenturacp/hass-kursus/raw/main/Screenshots/4-hasszha-7.png)

## Paring med Ikea pære
Vi skal have vores første enhed sat op på Home Assistant

### Start med at gå ind i Indstillinger og klik på Integrationer
![5-hassikeapair-1.png](https://github.com/zenturacp/hass-kursus/raw/main/Screenshots/5-hassikeapair-1.png)

### På din Zigbee Home Automation klikker du på Konfigurere
![5-hassikeapair-2.png](https://github.com/zenturacp/hass-kursus/raw/main/Screenshots/5-hassikeapair-2.png)

### Klik på tilføj Enhed
Når du klikker på denne knap vil den sætte dit Zigbee netværk i Pair Mode og det vil søge efter nye enheder i 60 sekunder.
![5-hassikeapair-3.png](https://github.com/zenturacp/hass-kursus/raw/main/Screenshots/5-hassikeapair-3.png)

### Din controller vil nu søge efter enheder der kan tilføjes
![5-hassikeapair-4.png](https://github.com/zenturacp/hass-kursus/raw/main/Screenshots/5-hassikeapair-4.png)

### Når den finder en enhed vil denne dukke op med informationer om hvad enheden er og hedder
Hvis du har oprettet områder kan du tilføje et område
![5-hassikeapair-5.png](https://github.com/zenturacp/hass-kursus/raw/main/Screenshots/5-hassikeapair-5.png)

### Det er vigtigt at navngive sin pære, da det kan være svært at finde den efterfølgende
![5-hassikeapair-6.png](https://github.com/zenturacp/hass-kursus/raw/main/Screenshots/5-hassikeapair-6.png)

### Når din enhed er klar kan du teste den ved at gå tilbage til oversigten og trænde / slukkee / skifte farve på enheden.
![5-hassikeapair-7.png](https://github.com/zenturacp/hass-kursus/raw/main/Screenshots/5-hassikeapair-7.png)

### Her et et eksempel på at skifte pæren til rød
![5-hassikeapair-8.png](https://github.com/zenturacp/hass-kursus/raw/main/Screenshots/5-hassikeapair-8.png)

# Simpel Automatisering
I dette eksempel vil vi sætte pæren til at slukke og tænde hvert minut.



# Installation af ESPHome

Link til ESP Home / Devices etc

## Installation af integration

## Opret første device - og flash det

## Test integration

# Automatisering

## Tænd lampe når der er over 30 grader på temperatur føler

## Tænd lyset på et bestemt tidspunkt

## Optional: Pir Sensor

### Diode

### PIR Sensor

# Links

* [Home Assistant](https://www.home-assistant.io)

## Firmwares
Aktuel version som passer til dette materiale, du kan altid finde nyeste versioner [her](https://www.home-assistant.io/installation/raspberrypi).

* [haos_rpi3-64-6.1.img.xz](https://github.com/zenturacp/hass-kursus/raw/main/Firmware/haos_rpi3-64-6.1.img.xz)
* [haos_rpi4-64-6.1.img.xz](https://github.com/zenturacp/hass-kursus/raw/main/Firmware/haos_rpi4-64-6.1.img.xz)
