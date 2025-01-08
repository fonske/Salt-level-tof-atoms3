# Zoutniveau meting met AtomS3 lite en TOF sensor

## Hardware
Er wordt gebruik gemaakt van 
- de [Atom S3 lite](https://www.tinytronics.nl/shop/nl/development-boards/microcontroller-boards/met-wi-fi/m5stack-atom-s3-lite-esp32-s3-development-board) van M5stack
- de [TOF sensor](https://www.tinytronics.nl/shop/nl/platformen-en-systemen/m5stack/unit/m5stack-tof-unit) van M5stack
- optie: [5cm kabeltje](https://www.tinytronics.nl/shop/nl/kabels-en-connectoren/kabels-en-adapters/grove-compatible/m5stack-grove-kabel-5cm-10-stuks) (net iets korter dan meegeleverd wordt met de TOF sensor, per 10st helaas)
- [3D printed](../README/Saltlevel_Atoms3_TOF.stl)  behuizing welke met twee rvs M4 boutjes en moertjes vast gezet kan worden op het deksel van het zout reservoir.

## Software
Alles is in ESPHOME geprogrammeerd.
Eigen wifi gegevens invullen via wifi hotspot met als wachtwoord: configesp

## Lovelace menu
Om het lovelace menu volledig te benutten met de zoutniveau simulatie zoals hieronder in het dashboard te zien is, 
dient er een map /www/images aangemaakt te worden in je home assistant directory.
Kopieer daar alle plaatjes in van [/www/images](../www/images)

Voorbeeld dashboard: 
![Example](Printscreen_NL.jpg)

Het dashboard zelf kan geplaatst worden via home assistant drie puntjes - dashboard bewerken - ruwe configuratie editor
Tekst uit [lovelace_menu_nl.yaml](../home_assistant/lovelace_menu_nl.yaml) daar aan toevoegen en opslaan.
U heeft nu een extra menu Zoutniveau

## Automations
[automation_saltalarm_nl.yaml](../home_assistant/automation_saltalarm_nl.yaml) samenvoegen met automations.yaml (let op inspringingen) of beter:

### Bestand op eigen lokatie: 
[automation_saltalarm_nl.yaml](../home_assistant/automation_saltalarm_nl) op een eigen lokatie zetten:
configuration.yaml aanpassen naar:

```yml
homeassistant:
  packages: !include_dir_named packages
```

Dan directory /packages aanmaken in /config en daar de automation_saltalarm_nl.yaml in kopieren
HA opnieuw starten

## Uitleg werking

Met de schuifregelaars de juiste hoogtes instellen.
Voorbeeld van de minimale en maximale hoogte vind u [hier.](../README/min_max_NL.jpg) 
Zout bijvullen afstand is de afstand vanaf wanneer er een alarm (automation) zal verstuurd worden (waarde van Bijvullen wordt dan "ja")
Dit is gemeten vanaf de onderkant van de tank, dus vanaf de maximale afstand naar boven toe.

Omdat er veel waterontharders zijn waar het water boven het zout staat (klein zoutreservoir), zit er een slimme functie ingebouwd in de afstandmeting
Namelijk, de sensor meet de afstand naar beneden toe. De te meten afstand wordt dan alleen maar groter als het zout op raakt.
Kortere afstanden worden dan ook niet geregistreerd als laatste waarde, enkel langere afstanden. Zo heeft water wat boven het zout uitkomt geen meet invloed meer.
Er zijn 2 registratie: Afstand en Afstand TOF.
Afstand is de meting met de slimme functie. Afstand TOF meet nog steeds continu elke 10 sec maar heeft geen invloed op de procent schaal of berekeningen daaraan.

### LED
De LED op de AtomS3 lite is in of uit te schakelen. Helderheid op 0 is ook LED uit.
De LED verspringt van kleur bij:

0-25% zoutniveau in de tank = ROOD

25-75% zoutniveau in de tank = BLAUW

75-100% zoutniveau in de tank = GROEN

### DRUKKNOP
De drukknop heeft twee functies:
kort ingedrukt (led gaat uit): stop de niveaumeting, handig om zelf even te kijken in het zoutvat.
kort ingedrukt (led gaat aan): zet de niveaumeting weer voort.

Lang ingedrukt (voor 3 sec.). Registreer tijd en datum. Handig om te zien wanneer voor het laatst zout bijgevuld is.
En om de slimme afstand weer te resetten naar 0 en werkelijke meting. Het zout is immers weer bijgevuld

## Noot:
Er is een  [3d print](../README/Saltlevel_Atoms3_TOF.stl)  bestand bijgevoegd om zelf de behuizing te printen.
De behuizing dient met dubbelzijdige tape op het zoutreservoir aan de bovenkant gemonteerd te worden.

