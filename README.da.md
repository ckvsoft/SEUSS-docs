![Logo](views/static/images/logo-seuss.png?raw=true "SEUSS")

# SEUSS

### [SEUSS -> Smart Ess Unit Spotmarket Switcher]

#### Rapportér venligst fejlene og foreslå forbedringer. Tak til alle, der allerede har deltaget.

###### Hvis du gerne vil bidrage med udvidelser til dette, bedes du indsende pull-anmodningen i dev-grenen. Til fejlrettelser kan pull-anmodningen også laves på hovedgrenen

### Hvad gør denne software?

Dette er en Python 3-applikation, der tænder din ESS-enhed (controller) på det rigtige tidspunkt, når dine dynamiske energipriser pr. time er lave. Eller bruges til udtømning, når priserne er ekstremt høje.

#### Aktuelt understøttede systemer er:

### ESS-enheder

* * *

-   **_Victron Venus OS energilagringssystemer såsom MultiPlus II-serien_**

* * *

### Spotmarkeder

* * *

-   **_svar_**
-   **_Enzo-E_**
-   **_Tibber_**

* * *

Styringen af ​​ESS-enheden (controlleren) sker via mqtt. Fordelen ved denne kontrol er:
at denne applikation ikke skal køre direkte på VenusOS. Direkte styring med D-BUS er undervejs

# Testet

This version was successful with

* * *

-   **_Linux Ubuntu >= 22.04_**
-   **_Venus OS Hindbær >= vz.12_**

* * *

testet

# Installere

Download installationsscriptet fra GitHub-lageret, udfør følgende kommando i din terminal:

    wget -O seuss_install.sh https://raw.githubusercontent.com/ckvsoft/SEUSS/dev/scripts/seuss_install.sh`

Kør installationsscriptet med yderligere muligheder for at forberede alt i en undermappe til din inspektion. For eksempel:

    bash seuss_install.sh`

Standardbiblioteket er /data/seuss (Venus OS) Men du kan valgfrit angive en anden mappe ved at bruge miljøvariablen TARGET_DIRECTORY, f.eks.

    TARGET_DIRECTORY=/opt/seuss bash seuss_install.sh`

På en Cerbo GX er filsystemet monteret skrivebeskyttet. Se<https://www.victronenergy.com/live/ccgx:root_access>.
For at gøre filsystemet skrivbart skal du udføre følgende kommando, før du kører installationsscriptet:

    /opt/victronenergy/swupdate-scripts/resize2fs.sh

# Konfiguration

Efter`SEUSS`er blevet installeret, er et websted tilgængeligt på IP-adressen og port 5000 på`Computer/VenusOS`hvor`SEUSS`blev installeret.

-   You can view or download the log file.
-   Desuden kan konfigurationen udføres ved hjælp af[Config Editor]menupunkt.
-   Værktøjstip til de fleste punkter vises her.

#### Log Viewer

-   ![Logo](views/static/images/logviewer.png?raw=true "SEUSS Log Viewer")

#### Config Editor - ESS-enheder

-   ![Logo](views/static/images/configeditor_ess.png?raw=true "SEUSS Config Editor")

#### Config Editor - PV paneler

-   ![Logo](views/static/images/configeditor_panels.png?raw=true "SEUSS Config Editor")

Disse kan også findes i indstillingsbeskrivelsen.
For dem, der foretrækker at arbejde i en konfigurationsfil, er der config.json

# Indstillinger

## Generel

| Indstilling     | Betyder                                                                                                                                   |
| --------------- | ----------------------------------------------------------------------------------------------------------------------------------------- |
| `time_zone`     | Vigtigt for korrekt timing af operationer baseret på din geografiske placering.<br/>Formater gerne`Europe/Vienna`,`Europe/Amsterdam`, ... |
| `log_file_path` | Indstiller en alternativ sti, som logfilerne gemmes til.                                                                                  |
| `log_level`     | Brugte Loglevel er:`INFO`,`WARNING`,`ERROR`og`DEBUG`. se[Log niveauer](#loglevels)                                                        |

## Priser

#### Ændr venligst priserne (brug altid Cent/kWh, uanset om du bruger Awattar (viser Cent/kWh) eller Entsoe API (viser EUR/MWh) / nettopriser ekskl. moms).

| Indstilling                                | Betyder                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| ------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `use_second_day`                           | `enable/disable`at sammenligne priserne i dag og i morgen, hvis de bliver tilgængelige<br/>Bemærk: Hvis du aktiverer dette og priserne falder over flere dage, er det muligt, at der ikke vil være nogen opkrævning eller skift i flere dage, indtil de laveste priser er nået.                                                                                                                                                                                                                                                                   |
| `number_of_lowest_prices_for_charging`     | To tilstande kan bruges her.<br/>tilstand 1:<br/>_antallet af billigste priser, som opkrævning skal/må finde sted til. Her indtaster du hele tal<br/>mode2:<br/>_Her bestemmes antallet af priser ud fra gennemsnitsprisen. I denne tilstand indtaster du decimaltal. F.eks. 0,85 for at modtage alle priser, der er 85 % under gennemsnittet. Det, der er relevant her, er specifikationen af ​​en kommaværdi. Med 1.0 antages det, at 100% af gennemsnitsprisen er taget (giver ingen mening), men hvis 1 er indtastet, er det 1 billigste pris |
| `number_of_highest_prices_for_discharging` | To tilstande kan bruges her.<br/>tilstand 1:<br/>_antallet af dyreste priser, som udledning skal/kan ske til. Her indtaster du hele tal<br/>mode2:<br/>_Her bestemmes antallet af priser ud fra gennemsnitsprisen. I denne tilstand indtaster du decimaltal. F.eks. 1,25 for at modtage alle priser, der er 25 % over gennemsnittet.<br/>Det, der er relevant her, er angivelsen af ​​en kommaværdi. Med 1.0 antages det, at 100% af gennemsnitsprisen er taget (giver ingen mening), men hvis 1 er indtastet, er det 1 dyreste pris              |
| `charging_price_limit`                     | opladning er altid aktiveret under denne pris<br/>antallet af de dyreste priser, hvortil udtømning skal/kan ske                                                                                                                                                                                                                                                                                                                                                                                                                                   |

## ESS-enheder

### Victron

| Indstilling           | Betyder                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| :-------------------- | :-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `use_vrm`             | Hvis dette punkt er aktiveret (sandt), gøres der et forsøg på at oprette forbindelse til Victron via VRM-portalen.<br/>Dette kræver en bruger/adgangskode i VRM-portalen                                                                                                                                                                                                                                                                |
| `ip_address`          | Den lokale IP-adresse på Victron.<br/>Dette er påkrævet hvis`use_vrm`er deaktiveret (falsk).<br/>Ellers forbliver dette felt tomt                                                                                                                                                                                                                                                                                                       |
| `unit_id`             | VRM-portal-id<br/>kan findes i`Settings / VRM online portal / VRM Portal Id`.<br/>Bemærk: Dette ID er påkrævet for at få adgang til Victron, selvom du ikke bruger en VRM-portal                                                                                                                                                                                                                                                        |
| `user`                | e-mailadresse, du bruger til at oprette forbindelse til VRM-portalen                                                                                                                                                                                                                                                                                                                                                                    |
| `password`            | adgangskode, du bruger til at oprette forbindelse til VRM-portalen                                                                                                                                                                                                                                                                                                                                                                      |
| `max_discharge_power` | Default: -1<br/>Hvis du bruger`Limit inverter power`i ESS menuen så skal denne værdi indtastes her.<br/>Hvis inverteren er indstillet til`Discharge false`af denne app, vil denne værdi blive overskrevet i ESS.<br/>Denne grænse er her indstillet i afladningstilstand i ESS.<br/>Hvis der ikke er sat nogen grænse, så lad værdien stå på`-1`.<br/>Eksempel: Enter`1000`at begrænse udledningen til`1000W`, Gå ind`-1`for fuld kraft |
| `only_observation`    | Hvis`only observation`er aktiveret vil essunit kun blive brugt til statistiske formål. Essent-enheden udfører ingen betingelser                                                                                                                                                                                                                                                                                                         |
| `enabled`             | For at bruge denne post skal den være`enabled`. Ellers`disabled`                                                                                                                                                                                                                                                                                                                                                                        |

## Spotmarkeder

### svar

| Indstilling | Betyder                                                                        |
| :---------- | :----------------------------------------------------------------------------- |
| `country`   | Vælg lokation AT eller DE                                                      |
| `primary`   | Hvis dette marked er aktiveret, angiver dette punkt det som det primære marked |
| `enabled`   | For at bruge denne post skal den være`enabled`. Ellers`disabled`               |

### Enzo er

| Indstilling  | Betyder                                                                                                                                                                                                                                                                                                                                                                                                                         |
| :----------- | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `api_token`  | Sådan får du det gratis api-sikkerhedstoken:<br/>1. Gå til<https://transparency.entsoe.eu/>--> tilmeld dig og opret en konto<br/>2. Send en e-mail til[transparency@entsoe.eu](mailto:transparency@entsoe.eu)med "Restful API access" i emnelinjen<br/>3. ENTSO-E Helpdesk vil svare på din anmodning inden for 3 arbejdsdage.<br/>4. Generer et sikkerhedstoken kl<https://transparency.entsoe.eu/usrm/user/myAccountSettings> |
| `in_domain`  | For at finde ud af din ind- og ud-domænenøgle gå til:<br/><https://www.entsoe.eu/data/energy-identification-codes-eic/eic-area-codes-map/>                                                                                                                                                                                                                                                                                      |
| `out_domain` | synes godt om`in_domain`                                                                                                                                                                                                                                                                                                                                                                                                        |
| `primary`    | Hvis dette marked er aktiveret, angiver dette punkt det som det primære marked                                                                                                                                                                                                                                                                                                                                                  |
| `enabled`    | For at bruge denne post skal den være`enabled`. Ellers`disabled`                                                                                                                                                                                                                                                                                                                                                                |

### Tibber

| Indstilling  | Betyder                                                                                                                                                                                                                                                                                                                                |
| :----------- | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `api_token`  | For at hente tibber_api_key:<br/>1. log ind med en gratis eller kunde Tibber konto på<https://developer.tibber.com/settings/access-token><br/>2. Opret et token ved at vælge de omfang, du har brug for (vælg "pris")<br/>3. Brug dette link til at oprette en gratis konto med din smartphone:<https://tibber.com/de/invite/ojgfbx2e> |
| `price_unit` | Indstillet til:<br/>"energi" til at bruge spotmarkedspriserne (standard),<br/>"i alt" for at bruge de samlede priser inklusive skatter og afgifter,<br/>"skat" for kun at bruge skatter og afgifter                                                                                                                                    |
| `primary`    | Hvis dette marked er aktiveret, angiver dette punkt det som det primære marked                                                                                                                                                                                                                                                         |
| `enabled`    | For at bruge denne post skal den være`enabled`. Ellers`disabled`                                                                                                                                                                                                                                                                       |

## PV paneler

| Indstilling       | Betyder                                                                                 |
| :---------------- | :-------------------------------------------------------------------------------------- |
| `locLat`          | Breddegrad                                                                              |
| `locLong`         | Længde                                                                                  |
| `angle`           | Vinkel på dine paneler 0 (vandret) … 90 (lodret)                                        |
| `direction`       | Plan azimut, -180 … 180 (-180 = nord, -90 = øst, 0 = syd, 90 = vest, 180 = nord)        |
| `totPower`        | installerede modulers effekt i kilowatt                                                 |
| `total_area`      | Samlet areal af panelerne i kvadratmeter                                                |
| `damping_morning` | Med denne parameter kan du justere resultatet om morgenen. Værdi float 0..1, standard 0 |
| `damping_evening` | Med denne parameter kan du justere resultatet om aftenen. Værdi float 0..1, standard 0  |
| `enabled`         | For at bruge denne post skal den være`enabled`. Ellers`disabled`                        |

* * *

## Logniveauer

### `ERROR`

Det`ERROR`log-niveau angiver fejltilstande i en applikation, der hindrer udførelsen af ​​en specifik operation. Selvom applikationen kan fortsætte med at fungere på et reduceret niveau af funktionalitet eller ydeevne,<br/>`ERROR`logs betyder problemer, der bør undersøges omgående.

### `WARN`

Begivenheder logget på`WARN`niveau indikerer typisk, at noget uventet har
opstod, men applikationen kan fortsætte med at fungere normalt indtil videre.
Det bruges også til at markere forhold, der skal behandles omgående, før de
eskalere til problemer for applikationen.

### `INFO`

Det`INFO`niveau fanger hændelser i systemet, der er væsentlige for
applikationens forretningsmæssige formål. Sådanne hændelser logges for at vise, at systemet er det
fungerer normalt. Produktionssystemer bruger typisk som standard logning på dette niveau
så en oversigt over applikationens normale adfærd er synlig for enhver
 gennemgang af loggene.

### `DEBUG`

Det`DEBUG`niveau bruges til at logge beskeder, der hjælper udviklere med at identificere
problemer under en fejlretningssession. Indholdet af de meddelelser, der er logget på DEBUG
niveau vil variere afhængigt af din ansøgning, men de indeholder typisk
detaljerede oplysninger, der hjælper udviklerne med fejlfinding af problemer
effektivt. Dette kan omfatte variables tilstand inden for det omgivende område eller
relevante fejlkoder. |

## Inspiration

Idéen er inspireret af @christian1980nrw-projektet, der er linket nedenfor. Dette projekt er mit første med Victron Venus OS, så jeg overtog nogle ideer og tilgange fra følgende projekter. Fremgangsmåden er den samme, og for meget smalle systemer er implementeringen med et bash-script sandsynligvis bedre

##### – mange tak for at videregive viden:

-   [Spotmarkedsskifter](https://github.com/christian1980nrw/Spotmarket-Switcher)
-   [dynamisk-ess](https://github.com/tfranssen/dynamic-ess)
