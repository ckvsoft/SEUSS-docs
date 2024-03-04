![Logo](views/static/images/logo-seuss.png?raw=true "SEUSS")

# SEUSS

### [SEUSS -> Smart Ess Unit Spotmarketswitcher]

#### Rapporteer de bugs en stel verbeteringen voor. Bedankt aan iedereen die al heeft deelgenomen.

###### Als u hieraan uitbreidingen wilt bijdragen, dient u het pull-verzoek in de dev branch in. Voor bugfixes kan het pull-verzoek ook op de hoofdtak worden gedaan

### Wat doet deze software?

Dit is een Python 3-applicatie die uw ESS-unit (controller) op het juiste moment inschakelt wanneer uw dynamische energieprijzen per uur laag zijn. Of gebruikt voor het lossen als de prijzen extreem hoog zijn.

#### Momenteel ondersteunde systemen zijn:

### ESS-eenheden

* * *

-   **_Victron Venus OS energieopslagsystemen zoals de MultiPlus II-serie_**

* * *

### Spotmarkten

* * *

-   **_antwoord_**
-   **_Enzo-E_**
-   **_Geklets_**

* * *

De aansturing van de ESS-unit (controller) gebeurt via mqtt. Het voordeel van deze controle is:
dat deze applicatie niet rechtstreeks op VenusOS hoeft te draaien. Directe besturing met D-BUS is in de maak

# Getest

Deze versie was succesvol met

* * *

-   **_Linux Ubuntu >= 22.04_**
-   **_Venus OS Frambozen >= vz.12_**

* * *

getest

# Installeren

Download het installatiescript uit de GitHub-repository en voer de volgende opdracht uit in uw terminal:

    wget -O seuss_install.sh https://raw.githubusercontent.com/ckvsoft/SEUSS/dev/scripts/seuss_install.sh`

Voer het installatiescript uit met extra opties om alles in een submap voor te bereiden voor uw inspectie. Bijvoorbeeld:

    bash seuss_install.sh`

De standaardmap is /data/seuss (Venus OS). Maar u kunt optioneel een andere map opgeven door de omgevingsvariabele TARGET_DIRECTORY te gebruiken, bijvoorbeeld:

    TARGET_DIRECTORY=/opt/seuss bash seuss_install.sh`

Op een Cerbo GX is het bestandssysteem alleen-lezen aangekoppeld. Zien<https://www.victronenergy.com/live/ccgx:root_access>.
Om het bestandssysteem schrijfbaar te maken, moet u de volgende opdracht uitvoeren voordat u het installatiescript uitvoert:

    /opt/victronenergy/swupdate-scripts/resize2fs.sh

# Configuratie

Na`SEUSS`is succesvol geïnstalleerd, er is een website beschikbaar op het IP-adres en poort 5000 van de`Computer/VenusOS`waarop`SEUSS`was geïnstalleerd.

-   U kunt het logbestand bekijken of downloaden.
-   Bovendien kan de configuratie worden uitgevoerd met behulp van de[Configuratieeditor] menu item.
-   Tooltips voor de meeste punten worden hier weergegeven.

#### Logboekviewer

-   ![Logo](views/static/images/logviewer.png?raw=true "SEUSS Log Viewer")

#### Configuratie-editor - ESS-eenheden

-   ![Logo](views/static/images/configeditor_ess.png?raw=true "SEUSS Config Editor")

#### Configuratie-editor - PV-panelen

-   ![Logo](views/static/images/configeditor_panels.png?raw=true "SEUSS Config Editor")

Deze zijn ook te vinden in de beschrijving van Instellingen.
Voor degenen die liever in een configuratiebestand werken, is er config.json

# Instellingen

## Algemeen

| Instelling      | Betekenis                                                                                                                                        |
| --------------- | ------------------------------------------------------------------------------------------------------------------------------------------------ |
| `time_zone`     | Essentieel voor de juiste timing van activiteiten op basis van uw geografische locatie.<br/>Formaat zoals`Europe/Vienna`,`Europe/Amsterdam`, ... |
| `log_file_path` | Stelt een alternatief pad in waarnaar de logbestanden worden opgeslagen.                                                                         |
| `log_level`     | Gebruikte Loglevel zijn:`INFO`,`WARNING`,`ERROR`En`DEBUG`. zien[Logniveaus](#loglevels)                                                          |

## Prijzen

#### Wijzig de prijzen (gebruik altijd Cent/kWh, ongeacht of u Awattar (geeft Cent/kWh weer) of Entsoe API (geeft EUR/MWh weer) / netto prijzen excl. belasting).

| Instelling                                 | Betekenis                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| ------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `use_second_day`                           | `enable/disable`om de prijzen van vandaag en morgen te vergelijken als deze beschikbaar komen<br/>Let op: Als u dit activeert en de prijzen dalen over meerdere dagen, kan het zijn dat er meerdere dagen niet wordt geladen of geschakeld totdat de laagste prijzen zijn bereikt.                                                                                                                                                                                                                                                                                                                           |
| `number_of_lowest_prices_for_charging`     | Hier kunnen twee modi worden gebruikt.<br/>modus1:<br/>_het aantal goedkoopste prijzen waartegen gefactureerd moet/mag worden. Hier vult u hele getallen in<br/>modus2:<br/>_Hierbij wordt het aantal prijzen bepaald op basis van de gemiddelde prijs. Voor deze modus voert u decimale getallen in. Bijvoorbeeld 0,85 om alle prijzen te ontvangen die 85% onder het gemiddelde liggen. Wat hier relevant is, is de specificatie van een kommawaarde. Bij 1.0 wordt aangenomen dat 100% van de gemiddelde prijs wordt genomen (heeft geen enkele zin) maar als 1 wordt ingevuld is het 1 goedkoopste prijs |
| `number_of_highest_prices_for_discharging` | Hier kunnen twee modi worden gebruikt.<br/>modus1:<br/>_het aantal duurste prijzen waartegen geloosd moet/mag worden. Hier vult u hele getallen in<br/>modus2:<br/>_Hierbij wordt het aantal prijzen bepaald op basis van de gemiddelde prijs. Voor deze modus voert u decimale getallen in. Bijvoorbeeld 1,25 om alle prijzen te ontvangen die 25% boven het gemiddelde liggen.<br/>Wat hier relevant is, is de specificatie van een kommawaarde. Bij 1.0 wordt aangenomen dat 100% van de gemiddelde prijs wordt afgenomen (heeft geen enkele zin) maar als er 1 wordt ingevuld is dit de 1 duurste prijs  |
| `charging_price_limit`                     | Laden is altijd mogelijk onder deze prijs<br/>het aantal van de duurste prijzen waartegen geloosd moet/mag worden                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |

## ESS-eenheden

### Victron

| Instelling            | Betekenis                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| :-------------------- | :---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `use_vrm`             | Als dit punt is ingeschakeld (waar), wordt er geprobeerd verbinding te maken met de Victron via het VRM-portaal.<br/>Hiervoor is een gebruiker/wachtwoord in de VRM-portal vereist                                                                                                                                                                                                                                                                                      |
| `ip_address`          | Het lokale IP-adres van de Victron.<br/>Dit is vereist als`use_vrm`is uitgeschakeld (onwaar).<br/>Anders blijft dit veld leeg                                                                                                                                                                                                                                                                                                                                           |
| `unit_id`             | VRM-portal-ID<br/>is te vinden in de`Settings / VRM online portal / VRM Portal Id`.<br/>Let op: Deze ID is vereist om toegang te krijgen tot de Victron, zelfs als u geen VRM-portaal gebruikt                                                                                                                                                                                                                                                                          |
| `user`                | e-mailadres dat u gebruikt om verbinding te maken met de VRM-portal                                                                                                                                                                                                                                                                                                                                                                                                     |
| `password`            | wachtwoord dat u gebruikt om verbinding te maken met de VRM-portal                                                                                                                                                                                                                                                                                                                                                                                                      |
| `max_discharge_power` | Standaard: -1<br/>Als je gebruikt`Limit inverter power`in het ESS-menu, dan moet deze waarde hier worden ingevoerd.<br/>Als de omvormer is ingesteld op`Discharge false`door deze app wordt deze waarde in de ESS overschreven.<br/>Deze limiet wordt hier ingesteld in de ontladingsmodus in de ESS.<br/>Als er geen limiet is ingesteld, laat de waarde dan staan`-1`.<br/>Voorbeeld: Voer in`1000`de afvoer te beperken`1000W`, Binnenkomen`-1`voor volledige kracht |
| `only_observation`    | Als`only observation`wordt geactiveerd, wordt de essunit alleen gebruikt voor statistische doeleinden. De essunit voert geen voorwaarden uit                                                                                                                                                                                                                                                                                                                            |
| `enabled`             | Om dit item te gebruiken, moet dit het geval zijn`enabled`. Anders`disabled`                                                                                                                                                                                                                                                                                                                                                                                            |

## Spotmarkten

### antwoord

| Instelling | Betekenis                                                                                     |
| :--------- | :-------------------------------------------------------------------------------------------- |
| `country`  | Kies locatie AT of DE                                                                         |
| `primary`  | Als deze markt mogelijk wordt gemaakt, wordt deze op dit punt ingesteld als de primaire markt |
| `enabled`  | Om dit item te gebruiken, moet dit het geval zijn`enabled`. Anders`disabled`                  |

### Enzo wel

| Instelling   | Betekenis                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| :----------- | :----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `api_token`  | Hoe u het gratis API-beveiligingstoken kunt verkrijgen:<br/>1. Ga naar<https://transparency.entsoe.eu/>--> registreer en maak een account aan<br/>2. Stuur een e-mail naar[transparency@entsoe.eu](mailto:transparency@entsoe.eu)met ‘Rustgevende API-toegang’ in de onderwerpregel<br/>3. De ENTSO-E Helpdesk zal binnen 3 werkdagen op uw verzoek reageren.<br/>4. Genereer een beveiligingstoken op<https://transparency.entsoe.eu/usrm/user/myAccountSettings> |
| `in_domain`  | Om uw in- en uit-domeinsleutel te achterhalen, gaat u naar:<br/><https://www.entsoe.eu/data/energy-identification-codes-eic/eic-area-codes-map/>                                                                                                                                                                                                                                                                                                                   |
| `out_domain` | leuk vinden`in_domain`                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| `primary`    | Als deze markt mogelijk wordt gemaakt, wordt deze op dit punt ingesteld als de primaire markt                                                                                                                                                                                                                                                                                                                                                                      |
| `enabled`    | Om dit item te gebruiken, moet dit het geval zijn`enabled`. Anders`disabled`                                                                                                                                                                                                                                                                                                                                                                                       |

### Geklets

| Instelling   | Betekenis                                                                                                                                                                                                                                                                                                                                                            |
| :----------- | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `api_token`  | Om de tibber_api_key te verkrijgen:<br/>1. log in met een gratis of klant Tibber-account op<https://developer.tibber.com/settings/access-token><br/>2. Maak een token aan door de scopes te selecteren die je nodig hebt (selecteer "prijs")<br/>3. Gebruik deze link om een ​​gratis account aan te maken met je smartphone:<https://tibber.com/de/invite/ojgfbx2e> |
| `price_unit` | Instellen op:<br/>"energie" om de spotmarktprijzen te gebruiken (standaard),<br/>"totaal" om de totale prijzen inclusief belastingen en toeslagen te gebruiken,<br/>"belasting" om alleen de belastingen en toeslagen te gebruiken                                                                                                                                   |
| `primary`    | Als deze markt mogelijk wordt gemaakt, wordt deze op dit punt ingesteld als de primaire markt                                                                                                                                                                                                                                                                        |
| `enabled`    | Om dit item te gebruiken, moet dit het geval zijn`enabled`. Anders`disabled`                                                                                                                                                                                                                                                                                         |

## PV-panelen

| Instelling        | Betekenis                                                                                       |
| :---------------- | :---------------------------------------------------------------------------------------------- |
| `locLat`          | Breedtegraad                                                                                    |
| `locLong`         | Lengtegraad                                                                                     |
| `angle`           | Hoek van uw panelen 0 (horizontaal) … 90 (verticaal)                                            |
| `direction`       | Vliegtuigazimut, -180 … 180 (-180 = noord, -90 = oost, 0 = zuid, 90 = west, 180 = noord)        |
| `totPower`        | geïnstalleerde modules vermogen in kilowatt                                                     |
| `total_area`      | Totale oppervlakte van de panelen in vierkante meters                                           |
| `damping_morning` | Met deze parameter kunt u het resultaat in de ochtend aanpassen. Waarde float 0..1, standaard 0 |
| `damping_evening` | Met deze parameter kunt u 's avonds het resultaat aanpassen. Waarde float 0..1, standaard 0     |
| `enabled`         | Om dit item te gebruiken, moet dit het geval zijn`enabled`. Anders`disabled`                    |

* * *

## Logniveaus

### `ERROR`

De`ERROR`logniveau geeft foutcondities binnen een applicatie aan die de uitvoering van een specifieke bewerking belemmeren. Hoewel de applicatie kan blijven functioneren met een lager functionaliteit- of prestatieniveau,<br/>`ERROR`logboeken duiden op problemen die onmiddellijk moeten worden onderzocht.

### `WARN`

Gebeurtenissen geregistreerd bij de`WARN`niveau geeft doorgaans aan dat er iets onverwachts is gebeurd
opgetreden, maar de applicatie kan voorlopig normaal blijven functioneren.
Het wordt ook gebruikt om omstandigheden aan te duiden die onmiddellijk moeten worden aangepakt voordat ze zich voordoen
escaleren tot problemen voor de toepassing.

### `INFO`

De`INFO`niveau legt gebeurtenissen in het systeem vast die belangrijk zijn voor de
het zakelijke doel van de applicatie. Dergelijke gebeurtenissen worden geregistreerd om aan te tonen dat het systeem dat doet
normaal functioneren. Productiesystemen zijn doorgaans standaard ingesteld op logboekregistratie op dit niveau
zodat een samenvatting van het normale gedrag van de applicatie voor iedereen zichtbaar is
 het bekijken van de logboeken.

### `DEBUG`

De`DEBUG`niveau wordt gebruikt voor het loggen van berichten die ontwikkelaars helpen bij het identificeren
problemen tijdens een foutopsporingssessie. De inhoud van de berichten die zijn vastgelegd bij DEBUG
niveau varieert afhankelijk van uw toepassing, maar bevat doorgaans
gedetailleerde informatie die de ontwikkelaars helpt bij het oplossen van problemen
efficiënt. Dit kan de status van variabelen binnen het omringende bereik omvatten
relevante foutcodes. |

## Inspiratie

Het idee is geïnspireerd op het @christian1980nrw-project dat hieronder wordt gelinkt. Dit project is mijn eerste met het Victron Venus OS, dus ik heb enkele ideeën en benaderingen overgenomen van de volgende projecten. De aanpak is hetzelfde en voor zeer smalle systemen is de implementatie met een bash-script waarschijnlijk beter

##### – hartelijk dank voor het doorgeven van de kennis:

-   [Spotmarktswitcher](https://github.com/christian1980nrw/Spotmarket-Switcher)
-   [dynamisch-ess](https://github.com/tfranssen/dynamic-ess)
