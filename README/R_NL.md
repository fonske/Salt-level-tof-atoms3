# Zoutniveau meting met AtomS3 lite en TOF sensor

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

### LED
De LED op de AtomS3 lite is in of uit te schakelen. Helderheid op 0 is ook LED uit.
De LED verspringt van kleur bij:

0-25% zoutniveau in de tank = ROOD

25-75% zoutniveau in de tank = BLAUW

75-100% zoutniveau in de tank = GROEN

### DRUK KNOP
De drukknop heeft twee functies:
kort ingedrukt (led gaat uit): stop de niveaumeting, handig om bij te vullen van zout.
kort ingedrukt (led gaat aam): zet de niveaumeting voort.

Lang ingedrukt (voor 3 sec.). Registreer tijd en datum. Handig om te zien wanneer voor het laatst bijgevuld is.
Succes!

## Noot:
Er is een 3d print bestand bijgevoegd om zelf de behuizing te printen.
De behuizing dient met dubbelzijdige tape op het zoutreservoir aan de bovenkant gemonteerd te worden.




