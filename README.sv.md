![Logo](views/static/images/logo-seuss.png?raw=true "SEUSS")

# SEUSS

### [SEUSS -> Smart Ess Unit Spotmarket Switcher]

#### Vänligen rapportera felen och föreslå förbättringar. Tack till alla som redan har deltagit.

###### Om du vill bidra med tillägg till detta, vänligen skicka in pull-förfrågan i dev-grenen. För buggfixar kan pull-begäran också göras på huvudgrenen

### Vad gör denna programvara?

Detta är en Python 3-applikation som slår på din ESS-enhet (kontroller) vid rätt tidpunkt när dina dynamiska energipriser per timme är låga. Eller används för tömning när priserna är extremt höga.

#### System som stöds för närvarande är:

### ESS-enheter

* * *

-   **_Victron Venus OS energilagringssystem som MultiPlus II-serien_**

* * *

### Spotmarknader

* * *

-   **_svar_**
-   **_Enzo-E_**
-   **_Tibber_**

* * *

Styrningen av ESS-enheten (styrenheten) sker via mqtt. Fördelen med denna kontroll är:
att denna applikation inte behöver köras direkt på VenusOS. Direktstyrning med D-BUS är på gång

# Testad

Denna version var framgångsrik med

* * *

-   **_Linux Ubuntu >= 22.04_**
-   **_Venus OS Hallon >= vz.12_**

* * *

testat

# Installera

Ladda ner installationsskriptet från GitHub-förvaret, kör följande kommando i din terminal:

    wget -O seuss_install.sh https://raw.githubusercontent.com/ckvsoft/SEUSS/dev/scripts/seuss_install.sh`

Kör installationsskriptet med ytterligare alternativ för att förbereda allt i en underkatalog för din inspektion. Till exempel:

    bash seuss_install.sh`

Standardkatalogen är /data/seuss (Venus OS) Men du kan valfritt ange en annan katalog genom att använda miljövariabeln TARGET_DIRECTORY t.ex.

    TARGET_DIRECTORY=/opt/seuss bash seuss_install.sh`

På en Cerbo GX är filsystemet skrivskyddat monterat. Ser<https://www.victronenergy.com/live/ccgx:root_access>.
För att göra filsystemet skrivbart måste du köra följande kommando innan du kör installationsskriptet:

    /opt/victronenergy/swupdate-scripts/resize2fs.sh

# Konfiguration

Efter`SEUSS`har installerats framgångsrikt finns en webbplats tillgänglig på IP-adressen och port 5000 för`Computer/VenusOS`på vilken`SEUSS`installerades.

-   Du kan visa eller ladda ner loggfilen.
-   Dessutom kan konfigurationen utföras med hjälp av[Config Editor]menyalternativ.
-   Verktygstips för de flesta punkter visas här.

#### Loggvisare

-   ![Logo](views/static/images/logviewer.png?raw=true "SEUSS Log Viewer")

#### Config Editor - ESS-enheter

-   ![Logo](views/static/images/configeditor_ess.png?raw=true "SEUSS Config Editor")

#### Config Editor - PV-paneler

-   ![Logo](views/static/images/configeditor_panels.png?raw=true "SEUSS Config Editor")

Dessa kan också hittas i beskrivningen av Inställningar.
För de som föredrar att arbeta i en konfigurationsfil finns config.json

# inställningar

## Allmän

| Miljö           | Menande                                                                                                                           |
| --------------- | --------------------------------------------------------------------------------------------------------------------------------- |
| `time_zone`     | Viktigt för korrekt timing av operationer baserat på din geografiska plats.<br/>Format som`Europe/Vienna`,`Europe/Amsterdam`, ... |
| `log_file_path` | Ställer in en alternativ sökväg till vilken loggfilerna sparas.                                                                   |
| `log_level`     | Använda Loglevel är:`INFO`,`WARNING`,`ERROR`och`DEBUG`. ser[Logga nivåer](#loglevels)                                             |

## Priser

#### Ändra priser (använd alltid Cent/kWh, oavsett om du använder Awattar (visar Cent/kWh) eller Entsoe API (visar EUR/MWh) / nettopriser exkl. moms).

| Miljö                                      | Menande                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| ------------------------------------------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `use_second_day`                           | `enable/disable`för att jämföra dagens och morgondagens priser om de blir tillgängliga<br/>Obs: Om du aktiverar detta och priserna sjunker under flera dagar, är det möjligt att det inte blir någon laddning eller byte på flera dagar tills de lägsta priserna uppnås.                                                                                                                                                                                                                  |
| `number_of_lowest_prices_for_charging`     | Två lägen kan användas här.<br/>läge 1:<br/>_antalet billigaste priser som laddning bör/får ske. Här anger du heltal<br/>läge 2:<br/>_Här bestäms antalet priser utifrån medelpriset. För detta läge anger du decimaltal. T.ex. 0,85 för att få alla priser som ligger 85 % under genomsnittet. Det som är relevant här är specifikationen av ett kommavärde. Med 1.0 antas det att 100% av det genomsnittliga priset tas (inte meningsfullt) men om 1 anges är det 1 billigaste pris     |
| `number_of_highest_prices_for_discharging` | Två lägen kan användas här.<br/>läge 1:<br/>_antalet dyraste priser till vilka lossning bör/får ske. Här anger du heltal<br/>läge 2:<br/>_Här bestäms antalet priser utifrån medelpriset. För detta läge anger du decimaltal. T.ex. 1,25 för att få alla priser som ligger 25 % över genomsnittet.<br/>Det som är relevant här är specifikationen av ett kommavärde. Med 1.0 antas det att 100 % av det genomsnittliga priset tas (ger ingen mening) men om 1 anges är det 1 dyraste pris |
| `charging_price_limit`                     | laddning är alltid aktiverad under detta pris<br/>antalet dyraste priser till vilka lossning bör/får ske                                                                                                                                                                                                                                                                                                                                                                                  |

## ESS-enheter

### Victron

| Miljö                 | Menande                                                                                                                                                                                                                                                                                                                                                                                                               |
| :-------------------- | :-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `use_vrm`             | Om denna punkt är aktiverad (true) görs ett försök att ansluta till Victron via VRM-portalen.<br/>Detta kräver en användare/lösenord i VRM-portalen                                                                                                                                                                                                                                                                   |
| `ip_address`          | Den lokala IP-adressen för Victron.<br/>Detta krävs om`use_vrm`är inaktiverad (falskt).<br/>Annars förblir detta fält tomt                                                                                                                                                                                                                                                                                            |
| `unit_id`             | VRM Portal ID<br/>finns i`Settings / VRM online portal / VRM Portal Id`.<br/>Obs: Detta ID krävs för att komma åt Victron även om du inte använder en VRM-portal                                                                                                                                                                                                                                                      |
| `user`                | e-postadress som du använder för att ansluta till VRM-portalen                                                                                                                                                                                                                                                                                                                                                        |
| `password`            | lösenord som du använder för att ansluta till VRM-portalen                                                                                                                                                                                                                                                                                                                                                            |
| `max_discharge_power` | Standard: -1<br/>Om du använder`Limit inverter power`i ESS-menyn måste detta värde anges här.<br/>Om växelriktaren är inställd på`Discharge false`av den här appen kommer detta värde att skrivas över i ESS.<br/>Denna gräns här är inställd i urladdningsläge i ESS.<br/>Om ingen gräns är inställd lämnar du värdet på`-1`.<br/>Exempel: Enter`1000`att begränsa utsläppet till`1000W`, Stiga på`-1`för full kraft |
| `only_observation`    | Om`only observation`är aktiverad kommer essenheten endast att användas för statistiska ändamål. Studieenheten utför inga villkor                                                                                                                                                                                                                                                                                      |
| `enabled`             | För att kunna använda den här posten måste den vara det`enabled`. Annat`disabled`                                                                                                                                                                                                                                                                                                                                     |

## Spotmarknader

### svar

| Miljö     | Menande                                                                           |
| :-------- | :-------------------------------------------------------------------------------- |
| `country` | Välj plats AT eller DE                                                            |
| `primary` | Om denna marknad är aktiverad anger denna punkt den som den primära marknaden     |
| `enabled` | För att kunna använda den här posten måste den vara det`enabled`. Annat`disabled` |

### Enzo är

| Miljö        | Menande                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| :----------- | :---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `api_token`  | Så här får du den gratis api-säkerhetstoken:<br/>1. Gå till<https://transparency.entsoe.eu/>--> registrera dig och skapa ett konto<br/>2. Skicka ett e-postmeddelande till[transparency@entsoe.eu](mailto:transparency@entsoe.eu)med "Restful API access" i ämnesraden<br/>3. ENTSO-E Helpdesk kommer att svara på din förfrågan inom 3 arbetsdagar.<br/>4. Generera en säkerhetstoken på<https://transparency.entsoe.eu/usrm/user/myAccountSettings> |
| `in_domain`  | För att ta reda på din in- och utdomännyckel, gå till:<br/><https://www.entsoe.eu/data/energy-identification-codes-eic/eic-area-codes-map/>                                                                                                                                                                                                                                                                                                           |
| `out_domain` | tycka om`in_domain`                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| `primary`    | Om denna marknad är aktiverad anger denna punkt den som den primära marknaden                                                                                                                                                                                                                                                                                                                                                                         |
| `enabled`    | För att kunna använda den här posten måste den vara det`enabled`. Annat`disabled`                                                                                                                                                                                                                                                                                                                                                                     |

### Tibber

| Miljö        | Menande                                                                                                                                                                                                                                                                                                                                           |
| :----------- | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `api_token`  | För att hämta tibber_api_key:<br/>1. logga in med ett gratis eller kund Tibber-konto på<https://developer.tibber.com/settings/access-token><br/>2. Skapa en token genom att välja de omfattningar du behöver (välj "pris")<br/>3. Använd den här länken för att skapa ett gratis konto med din smartphone:<https://tibber.com/de/invite/ojgfbx2e> |
| `price_unit` | Satt till:<br/>"energi" för att använda spotmarknadspriserna (standard),<br/>"totalt" för att använda de totala priserna inklusive skatter och avgifter,<br/>"skatt" för att endast använda skatter och avgifter                                                                                                                                  |
| `primary`    | Om denna marknad är aktiverad anger denna punkt den som den primära marknaden                                                                                                                                                                                                                                                                     |
| `enabled`    | För att kunna använda den här posten måste den vara det`enabled`. Annat`disabled`                                                                                                                                                                                                                                                                 |

## PV paneler

| Miljö             | Menande                                                                                        |
| :---------------- | :--------------------------------------------------------------------------------------------- |
| `locLat`          | Latitud                                                                                        |
| `locLong`         | Longitud                                                                                       |
| `angle`           | Vinkeln på dina paneler 0 (horisontell) … 90 (vertikal)                                        |
| `direction`       | Plan azimut, -180 … 180 (-180 = norr, -90 = öst, 0 = söder, 90 = väster, 180 = norr)           |
| `totPower`        | installerade moduler effekt i kilowatt                                                         |
| `total_area`      | Panelernas totala yta i kvadratmeter                                                           |
| `damping_morning` | Med denna parameter kan du justera resultatet på morgonen. Värdeflytande 0..1, standardvärde 0 |
| `damping_evening` | Med denna parameter kan du justera resultatet på kvällen. Värdeflytande 0..1, standardvärde 0  |
| `enabled`         | För att kunna använda den här posten måste den vara det`enabled`. Annat`disabled`              |

* * *

## Loggnivåer

### `ERROR`

De`ERROR`loggnivå indikerar feltillstånd inom en applikation som hindrar exekvering av en specifik operation. Även om applikationen kan fortsätta att fungera med en reducerad funktionalitet eller prestanda,<br/>`ERROR`loggar anger problem som bör undersökas omgående.

### `WARN`

Händelser loggade på`WARN`nivå indikerar vanligtvis att något oväntat har
inträffade, men applikationen kan fortsätta att fungera normalt tills vidare.
Det används också för att beteckna villkor som bör åtgärdas omgående innan de
eskalera till problem för applikationen.

### `INFO`

De`INFO`nivå fångar upp händelser i systemet som är viktiga för
applikationens affärsändamål. Sådana händelser loggas för att visa att systemet är det
fungerar normalt. Produktionssystem loggar vanligtvis som standard på denna nivå
så att en sammanfattning av programmets normala beteende är synlig för alla
 granska loggarna.

### `DEBUG`

De`DEBUG`nivå används för att logga meddelanden som hjälper utvecklare att identifiera
problem under en felsökningssession. Innehållet i meddelandena som loggas vid DEBUG
nivå kommer att variera beroende på din applikation, men de innehåller vanligtvis
detaljerad information som hjälper sina utvecklare att felsöka problem
effektivt. Detta kan inkludera variablers tillstånd inom det omgivande omfånget eller
relevanta felkoder. |

## Inspiration

Idén är inspirerad av @christian1980nrw-projektet som länkas nedan. Det här projektet är mitt första med Victron Venus OS, så jag anammade några idéer och tillvägagångssätt från följande projekt. Tillvägagångssättet är detsamma och för mycket smala system är implementeringen med ett bash-script förmodligen bättre

##### – tack så mycket för att du förmedlar kunskapen:

-   [Spot market switcher](https://github.com/christian1980nrw/Spotmarket-Switcher)
-   [dynamisk-ess](https://github.com/tfranssen/dynamic-ess)
