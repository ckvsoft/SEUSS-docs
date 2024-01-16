[tjeckiska](README.cs.md)-[danska](README.da.md)-[tysk](README.de.md)-[engelsk](README.md)-[spanska](README.es.md)-[estniska](README.et.md)-[finska](README.fi.md)-[franska](README.fr.md)-[grekisk](README.el.md)-[italienska](README.it.md)-[holländska](README.nl.md)-[norska](README.no.md)-[putsa](README.pl.md)-[portugisiska](README.pt.md)-[Svenska](README.sv.md)-[japanska](README.ja.md)

![Logo](views/static/images/logo-seuss.png?raw=true "SEUSS")

# SEUSS

#### [SEUSS -> Smart Ess Unit Spotmarket Switcher]

# inställningar

## Allmän

| Miljö           | Menande                                                                                                                       |
| --------------- | ----------------------------------------------------------------------------------------------------------------------------- |
| `time_zone`     | Viktigt för korrekt timing av operationer baserat på din geografiska plats.<br/>Format som Europa/Wien, Europa/Amsterdam, ... |
| `log_file_path` | Ställer in en alternativ sökväg till vilken loggfilerna sparas.                                                               |
| `log_level`     | Använda Loglevel är: INFO, VARNING, ERROR och DEBUG. ser[Logga nivåer](#loglevels)                                            |

## Priser

| Miljö                                      | Menande                                                                                                                                                                                                                                                                      |
| ------------------------------------------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `use_second_day`                           | aktivera/inaktivera för att jämföra dagens och morgondagens priser om de blir tillgängliga<br/>Obs: Om du aktiverar detta och priserna sjunker under flera dagar, är det möjligt att det inte blir någon laddning eller byte på flera dagar tills de lägsta priserna uppnås. |
| `number_of_lowest_prices_for_charging`     | antalet billigaste priser till vilka lastning bör/får ske                                                                                                                                                                                                                    |
| `number_of_highest_prices_for_discharging` | antalet dyraste priser till vilka lossning bör/får ske                                                                                                                                                                                                                       |
| `charging_price_limit`                     | laddning är alltid aktiverad under detta pris<br/>antalet dyraste priser till vilka lossning bör/får ske                                                                                                                                                                     |

## ESS-enheter

### Victron

| Miljö        | Menande                                                                                                                                                             |
| :----------- | :------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `use_vrm`    | Om denna punkt är aktiverad (true) görs ett försök att ansluta till Victron via VRM-portalen.<br/>Detta kräver en användare/lösenord i VRM-portalen                 |
| `ip_address` | Den lokala IP-adressen för Victron.<br/>Detta krävs om "use_vrm" är inaktiverat (false).<br/>Annars förblir detta fält tomt                                         |
| `unit_id`    | VRM Portal ID<br/>finns i Inställningar / VRM onlineportal / VRM Portal Id.<br/>Obs: Detta ID krävs för att komma åt Victron även om du inte använder en VRM-portal |
| `user`       | e-postadress som du använder för att ansluta till VRM-portalen                                                                                                      |
| `password`   | lösenord som du använder för att ansluta till VRM-portalen                                                                                                          |

## Marknader

### svar

| Miljö     | Menande                                                                       |
| :-------- | :---------------------------------------------------------------------------- |
| `country` | Välj plats AT eller DE                                                        |
| `primary` | Om denna marknad är aktiverad anger denna punkt den som den primära marknaden |
| `enabled` | ställ in din marknad som aktiverad/inaktiverad                                |

### Enzo är

| Miljö        | Menande                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| :----------- | :---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `api_token`  | Så här får du den gratis api-säkerhetstoken:<br/>1. Gå till<https://transparency.entsoe.eu/>--> registrera dig och skapa ett konto<br/>2. Skicka ett e-postmeddelande till[transparency@entsoe.eu](mailto:transparency@entsoe.eu)med "Restful API access" i ämnesraden<br/>3. ENTSO-E Helpdesk kommer att svara på din förfrågan inom 3 arbetsdagar.<br/>4. Generera en säkerhetstoken på<https://transparency.entsoe.eu/usrm/user/myAccountSettings> |
| `in_domain`  | För att ta reda på din in- och utdomännyckel, gå till:<br/><https://www.entsoe.eu/data/energy-identification-codes-eic/eic-area-codes-map/>                                                                                                                                                                                                                                                                                                           |
| `out_domain` | som in_domän                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| `primary`    | Om denna marknad är aktiverad anger denna punkt den som den primära marknaden                                                                                                                                                                                                                                                                                                                                                                         |
| `enabled`    | ställ in din marknad som aktiverad/inaktiverad                                                                                                                                                                                                                                                                                                                                                                                                        |

### Tibber

| Miljö        | Menande                                                                                                                                                                                                                                                                                                                                           |
| :----------- | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `api_token`  | För att hämta tibber_api_key:<br/>1. logga in med ett gratis eller kund Tibber-konto på<https://developer.tibber.com/settings/access-token><br/>2. Skapa en token genom att välja de omfattningar du behöver (välj "pris")<br/>3. Använd den här länken för att skapa ett gratis konto med din smartphone:<https://tibber.com/de/invite/ojgfbx2e> |
| `price_unit` | Satt till:<br/>"energi" för att använda spotmarknadspriserna (standard),<br/>"totalt" för att använda de totala priserna inklusive skatter och avgifter,<br/>"skatt" för att endast använda skatter och avgifter                                                                                                                                  |
| `primary`    | Om denna marknad är aktiverad anger denna punkt den som den primära marknaden                                                                                                                                                                                                                                                                     |
| `enabled`    | ställ in din marknad som aktiverad/inaktiverad                                                                                                                                                                                                                                                                                                    |

* * *

# Loggnivåer

### FEL

ERROR-loggnivån indikerar feltillstånd inom en applikation som hindrar exekvering av en specifik operation. Även om applikationen kan fortsätta att fungera med en reducerad funktionalitet eller prestanda,<br/>FELloggar betyder problem som bör undersökas omgående.

### VARNA

Händelser som loggas på WARN-nivå indikerar vanligtvis att något oväntat har gjort det
inträffade, men applikationen kan fortsätta att fungera normalt tills vidare.
Det används också för att beteckna villkor som bör åtgärdas omgående innan de
eskalera till problem för applikationen.

### INFO

INFO-nivån fångar upp händelser i systemet som är viktiga för
applikationens affärsändamål. Sådana händelser loggas för att visa att systemet är det
fungerar normalt. Produktionssystem loggar vanligtvis som standard på denna nivå
så att en sammanfattning av programmets normala beteende är synlig för alla
 granska loggarna.

### DEBUGA

DEBUG-nivån används för att logga meddelanden som hjälper utvecklare att identifiera
problem under en felsökningssession. Innehållet i meddelandena som loggas vid DEBUG
nivå kommer att variera beroende på din applikation, men de innehåller vanligtvis
detaljerad information som hjälper sina utvecklare att felsöka problem
effektivt. Detta kan inkludera variablers tillstånd inom det omgivande omfånget eller
relevanta felkoder. |
