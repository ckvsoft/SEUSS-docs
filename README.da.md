[tjekkisk](README.cs.md)-[Dansk](README.da.md)-[tysk](README.de.md)-[engelsk](README.md)-[spansk](README.es.md)-[estisk](README.et.md)-[finsk](README.fi.md)-[fransk](README.fr.md)-[græsk](README.el.md)-[italiensk](README.it.md)-[hollandsk](README.nl.md)-[Norsk](README.no.md)-[Polere](README.pl.md)-[portugisisk](README.pt.md)-[svensk](README.sv.md)-[japansk](README.ja.md)

![Logo](views/static/images/logo-seuss.png?raw=true "SEUSS")

# SEUSS

#### [SEUSS -> Smart Ess Unit Spotmarket Switcher]

\#Prøve

# Indstillinger

## Generel

| Indstilling     | Betyder                                                                                                                             |
| --------------- | ----------------------------------------------------------------------------------------------------------------------------------- |
| `time_zone`     | Vigtigt for korrekt timing af operationer baseret på din geografiske placering.<br/>Formater som Europa/Wien, Europa/Amsterdam, ... |
| `log_file_path` | Indstiller en alternativ sti, som logfilerne gemmes til.                                                                            |
| `log_level`     | Brugte Logniveau er: INFO, ADVARSEL, FEJL og DEBUG. se[Log niveauer](#loglevels)                                                    |

## Priser

| Indstilling                                | Betyder                                                                                                                                                                                                                                                                                 |
| ------------------------------------------ | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `use_second_day`                           | aktivere/deaktivere for at sammenligne priserne i dag og i morgen, hvis de bliver tilgængelige<br/>Bemærk: Hvis du aktiverer dette og priserne falder over flere dage, er det muligt, at der ikke vil være nogen opkrævning eller skift i flere dage, indtil de laveste priser er nået. |
| `number_of_lowest_prices_for_charging`     | antallet af billigste priser, som lastning skal/kan ske til                                                                                                                                                                                                                             |
| `number_of_highest_prices_for_discharging` | antallet af de dyreste priser, hvortil udtømning skal/kan ske                                                                                                                                                                                                                           |
| `charging_price_limit`                     | opladning er altid aktiveret under denne pris<br/>antallet af de dyreste priser, hvortil udtømning skal/kan ske                                                                                                                                                                         |

## ESS-enheder

### Victron

| Indstilling  | Betyder                                                                                                                                                                              |
| :----------- | :----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `use_vrm`    | Hvis dette punkt er aktiveret (sandt), gøres der et forsøg på at oprette forbindelse til Victron via VRM-portalen.<br/>Dette kræver en bruger/adgangskode i VRM-portalen             |
| `ip_address` | Den lokale IP-adresse på Victron.<br/>Dette er påkrævet, hvis "use_vrm" er deaktiveret (falsk).<br/>Ellers forbliver dette felt tomt                                                 |
| `unit_id`    | VRM-portal-id<br/>kan findes i Indstillinger / VRM online portal / VRM Portal Id.<br/>Bemærk: Dette ID er påkrævet for at få adgang til Victron, selvom du ikke bruger en VRM-portal |
| `user`       | e-mailadresse, du bruger til at oprette forbindelse til VRM-portalen                                                                                                                 |
| `password`   | adgangskode, du bruger til at oprette forbindelse til VRM-portalen                                                                                                                   |

## Markeder

### svar

| Indstilling | Betyder                                                                        |
| :---------- | :----------------------------------------------------------------------------- |
| `country`   | Vælg lokation AT eller DE                                                      |
| `primary`   | Hvis dette marked er aktiveret, angiver dette punkt det som det primære marked |
| `enabled`   | sæt dit marked som aktiveret/deaktiveret                                       |

### Enzo er

| Indstilling  | Betyder                                                                                                                                                                                                                                                                                                                                                                                                                         |
| :----------- | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `api_token`  | Sådan får du det gratis api-sikkerhedstoken:<br/>1. Gå til<https://transparency.entsoe.eu/>--> tilmeld dig og opret en konto<br/>2. Send en e-mail til[transparency@entsoe.eu](mailto:transparency@entsoe.eu)med "Restful API access" i emnelinjen<br/>3. ENTSO-E Helpdesk vil svare på din anmodning inden for 3 arbejdsdage.<br/>4. Generer et sikkerhedstoken kl<https://transparency.entsoe.eu/usrm/user/myAccountSettings> |
| `in_domain`  | For at finde ud af din ind- og ud-domænenøgle gå til:<br/><https://www.entsoe.eu/data/energy-identification-codes-eic/eic-area-codes-map/>                                                                                                                                                                                                                                                                                      |
| `out_domain` | som in_domain                                                                                                                                                                                                                                                                                                                                                                                                                   |
| `primary`    | Hvis dette marked er aktiveret, angiver dette punkt det som det primære marked                                                                                                                                                                                                                                                                                                                                                  |
| `enabled`    | sæt dit marked som aktiveret/deaktiveret                                                                                                                                                                                                                                                                                                                                                                                        |

### Tibber

| Indstilling  | Betyder                                                                                                                                                                                                                                                                                                                                |
| :----------- | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `api_token`  | For at hente tibber_api_key:<br/>1. log ind med en gratis eller kunde Tibber konto på<https://developer.tibber.com/settings/access-token><br/>2. Opret et token ved at vælge de omfang, du har brug for (vælg "pris")<br/>3. Brug dette link til at oprette en gratis konto med din smartphone:<https://tibber.com/de/invite/ojgfbx2e> |
| `price_unit` | Indstillet til:<br/>"energi" til at bruge spotmarkedspriserne (standard),<br/>"total" for at bruge de samlede priser inklusive skatter og afgifter,<br/>"skat" for kun at bruge skatter og afgifter                                                                                                                                    |
| `primary`    | Hvis dette marked er aktiveret, angiver dette punkt det som det primære marked                                                                                                                                                                                                                                                         |
| `enabled`    | sæt dit marked som aktiveret/deaktiveret                                                                                                                                                                                                                                                                                               |

* * *

# Logniveauer

### FEJL

ERROR-logniveauet angiver fejltilstande i en applikation, der hindrer udførelsen af ​​en specifik handling. Selvom applikationen kan fortsætte med at fungere på et reduceret niveau af funktionalitet eller ydeevne,<br/>FEJL-logs angiver problemer, der bør undersøges omgående.

### ADVARE

Hændelser logget på WARN-niveau indikerer typisk, at noget uventet har gjort det
opstod, men applikationen kan fortsætte med at fungere normalt indtil videre.
Det bruges også til at markere forhold, der skal behandles omgående, før de
eskalere til problemer for applikationen.

### INFO

INFO-niveauet fanger hændelser i systemet, der er væsentlige for
applikationens forretningsmæssige formål. Sådanne hændelser logges for at vise, at systemet er det
fungerer normalt. Produktionssystemer bruger typisk som standard logning på dette niveau
så en oversigt over applikationens normale adfærd er synlig for enhver
 gennemgang af loggene.

### FEJLFINDE

DEBUG-niveauet bruges til at logge meddelelser, der hjælper udviklere med at identificere
problemer under en fejlretningssession. Indholdet af meddelelserne logget på DEBUG
niveau vil variere afhængigt af din ansøgning, men de indeholder typisk
detaljerede oplysninger, der hjælper udviklerne med fejlfinding af problemer
effektivt. Dette kan omfatte variables tilstand inden for det omgivende område eller
relevante fejlkoder. |
