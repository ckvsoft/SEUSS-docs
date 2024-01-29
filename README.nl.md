![Logo](views/static/images/logo-seuss.png?raw=true "SEUSS")

# SEUSS

#### [SEUSS -> Smart Ess Unit Spotmarketswitcher]

# Instellingen

## Algemeen

| Instelling      | Betekenis                                                                                                                                        |
| --------------- | ------------------------------------------------------------------------------------------------------------------------------------------------ |
| `time_zone`     | Essentieel voor de juiste timing van activiteiten op basis van uw geografische locatie.<br/>Formaat zoals`Europe/Vienna`,`Europe/Amsterdam`, ... |
| `log_file_path` | Stelt een alternatief pad in waarnaar de logbestanden worden opgeslagen.                                                                         |
| `log_level`     | Gebruikte Loglevel zijn: INFO, WAARSCHUWING, ERROR en DEBUG. zien[Logniveaus](#loglevels)                                                        |

## Prijzen

| Instelling                                 | Betekenis                                                                                                                                                                                                                                                                           |
| ------------------------------------------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `use_second_day`                           | in-/uitschakelen om de prijzen van vandaag en morgen te vergelijken als deze beschikbaar komen<br/>Let op: Als u dit activeert en de prijzen dalen over meerdere dagen, kan het zijn dat er meerdere dagen niet wordt geladen of geschakeld totdat de laagste prijzen zijn bereikt. |
| `number_of_lowest_prices_for_charging`     | het aantal goedkoopste prijzen waartegen geladen moet/mag worden                                                                                                                                                                                                                    |
| `number_of_highest_prices_for_discharging` | het aantal van de duurste prijzen waartegen geloosd moet/mag worden                                                                                                                                                                                                                 |
| `charging_price_limit`                     | Onder deze prijs is opladen altijd mogelijk<br/>het aantal van de duurste prijzen waartegen geloosd moet/mag worden                                                                                                                                                                 |

## ESS-eenheden

### Victron

| Instelling   | Betekenis                                                                                                                                                                                 |
| :----------- | :---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `use_vrm`    | Als dit punt is ingeschakeld (waar), wordt er geprobeerd verbinding te maken met de Victron via het VRM-portaal.<br/>Hiervoor is een gebruiker/wachtwoord in de VRM-portal vereist        |
| `ip_address` | Het lokale IP-adres van de Victron.<br/>Dit is vereist als "use_vrm" is uitgeschakeld (false).<br/>Anders blijft dit veld leeg                                                            |
| `unit_id`    | VRM-portal-ID<br/>vindt u in Instellingen / VRM online portal / VRM Portal Id.<br/>Let op: Deze ID is vereist om toegang te krijgen tot de Victron, zelfs als u geen VRM-portaal gebruikt |
| `user`       | e-mailadres dat u gebruikt om verbinding te maken met de VRM-portal                                                                                                                       |
| `password`   | wachtwoord dat u gebruikt om verbinding te maken met de VRM-portal                                                                                                                        |

## Markten

### antwoord

| Instelling | Betekenis                                                                                     |
| :--------- | :-------------------------------------------------------------------------------------------- |
| `country`  | Kies locatie AT of DE                                                                         |
| `primary`  | Als deze markt mogelijk wordt gemaakt, wordt deze op dit punt ingesteld als de primaire markt |
| `enabled`  | stel uw markt in als ingeschakeld/uitgeschakeld                                               |

### Enzo wel

| Instelling   | Betekenis                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| :----------- | :----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `api_token`  | Hoe u het gratis API-beveiligingstoken kunt verkrijgen:<br/>1. Ga naar<https://transparency.entsoe.eu/>--> registreer en maak een account aan<br/>2. Stuur een e-mail naar[transparency@entsoe.eu](mailto:transparency@entsoe.eu)met ‘Rustgevende API-toegang’ in de onderwerpregel<br/>3. De ENTSO-E Helpdesk zal binnen 3 werkdagen op uw verzoek reageren.<br/>4. Genereer een beveiligingstoken op<https://transparency.entsoe.eu/usrm/user/myAccountSettings> |
| `in_domain`  | Om uw in- en uit-domeinsleutel te achterhalen, gaat u naar:<br/><https://www.entsoe.eu/data/energy-identification-codes-eic/eic-area-codes-map/>                                                                                                                                                                                                                                                                                                                   |
| `out_domain` | zoals in_domein                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| `primary`    | Als deze markt mogelijk wordt gemaakt, wordt deze op dit punt ingesteld als de primaire markt                                                                                                                                                                                                                                                                                                                                                                      |
| `enabled`    | stel uw markt in als ingeschakeld/uitgeschakeld                                                                                                                                                                                                                                                                                                                                                                                                                    |

### Geklets

| Instelling   | Betekenis                                                                                                                                                                                                                                                                                                                                                            |
| :----------- | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `api_token`  | Om de tibber_api_key te verkrijgen:<br/>1. log in met een gratis of klant-Tibber-account op<https://developer.tibber.com/settings/access-token><br/>2. Maak een token aan door de scopes te selecteren die je nodig hebt (selecteer "prijs")<br/>3. Gebruik deze link om een ​​gratis account aan te maken met je smartphone:<https://tibber.com/de/invite/ojgfbx2e> |
| `price_unit` | Instellen op:<br/>"energie" om de spotmarktprijzen te gebruiken (standaard),<br/>"totaal" om de totale prijzen inclusief belastingen en toeslagen te gebruiken,<br/>"belasting" om alleen de belastingen en toeslagen te gebruiken                                                                                                                                   |
| `primary`    | Als deze markt mogelijk wordt gemaakt, wordt deze op dit punt ingesteld als de primaire markt                                                                                                                                                                                                                                                                        |
| `enabled`    | stel uw markt in als ingeschakeld/uitgeschakeld                                                                                                                                                                                                                                                                                                                      |

* * *

# Logniveaus

### `ERROR`

De`ERROR`logniveau geeft foutcondities binnen een applicatie aan die de uitvoering van een specifieke bewerking belemmeren. Hoewel de applicatie kan blijven functioneren met een lager functionaliteit- of prestatieniveau,<br/>`ERROR`logboeken duiden op problemen die onmiddellijk moeten worden onderzocht.

### `WARN`

Gebeurtenissen geregistreerd bij de`WARN`niveau geeft doorgaans aan dat er iets onverwachts is gebeurd
opgetreden, maar de applicatie kan voorlopig normaal blijven functioneren.
Het wordt ook gebruikt om omstandigheden aan te duiden die onmiddellijk moeten worden aangepakt voordat ze zich voordoen
escaleren tot problemen voor de toepassing.

### `INFO`

De`INFO`niveau legt gebeurtenissen in het systeem vast die van belang zijn voor de
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
