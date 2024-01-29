![Logo](views/static/images/logo-seuss.png?raw=true "SEUSS")

# SEUSS

### [SEUSS -> Smart Ess Unit Spotmarket Switcher]

#### Rapporter feilene og foreslå forbedringer. Takk til alle som allerede har deltatt.

###### Hvis du ønsker å bidra med utvidelser til dette, vennligst send inn pull-forespørselen i dev-grenen. For feilrettinger kan pull-forespørselen også gjøres på hovedgrenen

### Hva gjør denne programvaren?

Dette er en Python 3-applikasjon som slår på ESS-enheten (kontrolleren) til rett tid når dine dynamiske energipriser per time er lave. Eller brukes til tømming når prisene er ekstremt høye.

#### For øyeblikket støttede systemer er:

### ESS-enheter

* * *

-   **_Victron Venus OS energilagringssystemer som MultiPlus II-serien_**

* * *

### Spot Markets

* * *

-   **_svar_**
-   **_Enzo-E_**
-   **_Tibber_**

* * *

Styringen av ESS-enheten (kontrolleren) gjøres via mqtt. Fordelen med denne kontrollen er:
at denne applikasjonen ikke trenger å kjøre direkte på VenusOS. Direkte styring med D-BUS er under arbeid

# Testet

Denne versjonen var vellykket med

* * *

-   **_Linux Ubuntu >= 22.04_**
-   **_Venus OS bringebær >= vz.12_**

* * *

testet

# Installere

Last ned installasjonsskriptet fra GitHub-depotet, utfør følgende kommando i terminalen din:

    wget -O seuss_install.sh https://raw.githubusercontent.com/ckvsoft/SEUSS/dev/scripts/seuss_install.sh`

Kjør installasjonsskriptet med flere alternativer for å forberede alt i en underkatalog for inspeksjonen din. For eksempel:

    bash seuss_install.sh`

Standardkatalogen er /data/seuss (Venus OS) Men du kan eventuelt spesifisere en annen katalog ved å bruke miljøvariabelen TARGET_DIRECTORY, f.eks.

    TARGET_DIRECTORY=/opt/seuss bash seuss_install.sh`

På en Cerbo GX er filsystemet montert skrivebeskyttet. Se<https://www.victronenergy.com/live/ccgx:root_access>.
For å gjøre filsystemet skrivbart må du utføre følgende kommando før du kjører installasjonsskriptet:

    /opt/victronenergy/swupdate-scripts/resize2fs.sh

# Konfigurasjon

Etter`SEUSS`har blitt installert, er et nettsted tilgjengelig på IP-adressen og port 5000 til`Computer/VenusOS`på hvilken`SEUSS`ble installert.

-   Du kan se eller laste ned loggfilen.
-   Videre kan konfigurasjonen utføres ved hjelp av[Konfigurasjonsredigering]menyelement.
-   Verktøytips for de fleste punktene vises her.

#### Loggviser

-   ![Logo](views/static/images/logviewer.png?raw=true "SEUSS Log Viewer")

#### Config Editor - ESS-enheter

-   ![Logo](views/static/images/configeditor_ess.png?raw=true "SEUSS Config Editor")

#### Config Editor - PV-paneler

-   ![Logo](views/static/images/configeditor_panels.png?raw=true "SEUSS Config Editor")

Disse finnes også i Innstillinger-beskrivelsen.
For de som foretrekker å jobbe i en konfigurasjonsfil, er det config.toml

# Innstillinger

## Generell

| Innstilling     | Betydning                                                                                                                              |
| --------------- | -------------------------------------------------------------------------------------------------------------------------------------- |
| `time_zone`     | Viktig for korrekt timing av operasjoner basert på din geografiske plassering.<br/>Formater som`Europe/Vienna`,`Europe/Amsterdam`, ... |
| `log_file_path` | Angir en alternativ bane som loggfilene lagres til.                                                                                    |
| `log_level`     | Brukte Loglevel er:`INFO`,`WARNING`,`ERROR`og`DEBUG`. se[Loggnivåer](#loglevels)                                                       |

## Priser

#### Vennligst endre prisene (bruk alltid Cent/kWh, uansett om du bruker Awattar (viser Cent/kWh) eller Entsoe API (viser EUR/MWh) / nettopriser ekskl. mva).

| Innstilling                                | Betydning                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| ------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `use_second_day`                           | `enable/disable`å sammenligne prisene i dag og i morgen hvis de blir tilgjengelige<br/>Merk: Hvis du aktiverer dette og prisene synker over flere dager, er det mulig at det ikke vil være noen lading eller bytte på flere dager før de laveste prisene er nådd.                                                                                                                                                                                                                                                   |
| `number_of_lowest_prices_for_charging`     | To moduser kan brukes her.<br/>modus 1:<br/>_antall billigste priser som lading bør/kan skje til. Her legger du inn hele tall<br/>modus 2:<br/>_Her bestemmes antall priser ut fra gjennomsnittsprisen. For denne modusen legger du inn desimaltall. f.eks. 0,85 for å motta alle priser som er 85 % under gjennomsnittet. Det som er relevant her er spesifikasjonen av en kommaverdi. Med 1.0 antas det at 100 % av gjennomsnittsprisen er tatt (gir ingen mening), men hvis 1 er angitt er det 1 billigste pris  |
| `number_of_highest_prices_for_discharging` | To moduser kan brukes her.<br/>modus 1:<br/>_antall dyreste priser som utslipp skal/kan skje til. Her legger du inn hele tall<br/>modus 2:<br/>_Her bestemmes antall priser ut fra gjennomsnittsprisen. For denne modusen legger du inn desimaltall. f.eks. 1,25 for å motta alle priser som er 25 % over gjennomsnittet.<br/>Det som er relevant her er spesifikasjonen av en kommaverdi. Med 1.0 antas det at 100 % av gjennomsnittsprisen er tatt (gir ingen mening), men hvis 1 er angitt er det 1 dyreste pris |
| `charging_price_limit`                     | lading er alltid aktivert under denne prisen<br/>antall dyreste priser som utslipp bør/kan foretas til                                                                                                                                                                                                                                                                                                                                                                                                              |

## ESS-enheter

### Victron

| Innstilling           | Betydning                                                                                                                                                                                                                                                                                                                                                                                                    |
| :-------------------- | :----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `use_vrm`             | Hvis dette punktet er aktivert (sant), gjøres det et forsøk på å koble til Victron via VRM-portalen.<br/>Dette krever bruker/passord i VRM-portalen                                                                                                                                                                                                                                                          |
| `ip_address`          | Den lokale IP-adressen til Victron.<br/>Dette kreves hvis`use_vrm`er deaktivert (false).<br/>Ellers forblir dette feltet tomt                                                                                                                                                                                                                                                                                |
| `unit_id`             | VRM-portal-ID<br/>finnes i`Settings / VRM online portal / VRM Portal Id`.<br/>Merk: Denne IDen er nødvendig for å få tilgang til Victron selv om du ikke bruker en VRM-portal                                                                                                                                                                                                                                |
| `user`                | e-postadresse du bruker for å koble til VRM-portalen                                                                                                                                                                                                                                                                                                                                                         |
| `password`            | passordet du bruker for å koble til VRM-portalen                                                                                                                                                                                                                                                                                                                                                             |
| `max_discharge_power` | Standard: -1<br/>Hvis du bruker`Limit inverter power`i ESS-menyen må denne verdien legges inn her.<br/>Hvis omformeren er satt til`Discharge false`av denne appen vil denne verdien bli overskrevet i ESS.<br/>Denne grensen her er satt i utladningsmodus i ESS.<br/>Hvis ingen grense er satt, la verdien stå på`-1`.<br/>Example: Enter `1000`å begrense utslippet til`1000W`, Tast inn`-1`for full kraft |
| `primary`             | Hvis dette markedet er aktivert, setter dette punktet det som det primære markedet                                                                                                                                                                                                                                                                                                                           |
| `enabled`             | For å bruke denne oppføringen må den være det`enabled`. Ellers`disabled`                                                                                                                                                                                                                                                                                                                                     |

## Spot Markets

### svar

| Innstilling | Betydning                                                                          |
| :---------- | :--------------------------------------------------------------------------------- |
| `country`   | Velg plassering AT eller DE                                                        |
| `primary`   | Hvis dette markedet er aktivert, setter dette punktet det som det primære markedet |
| `enabled`   | For å bruke denne oppføringen må den være det`enabled`. Ellers`disabled`           |

### Enzo er

| Innstilling  | Betydning                                                                                                                                                                                                                                                                                                                                                                                                                     |
| :----------- | :---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `api_token`  | Slik får du gratis api-sikkerhetstoken:<br/>1. Gå til<https://transparency.entsoe.eu/>--> registrer deg og opprett en konto<br/>2. Send en e-post til[transparency@entsoe.eu](mailto:transparency@entsoe.eu)med "Restful API access" i emnelinjen<br/>3. ENTSO-E Helpdesk vil svare på forespørselen din innen 3 virkedager.<br/>4. Generer et sikkerhetstoken på<https://transparency.entsoe.eu/usrm/user/myAccountSettings> |
| `in_domain`  | For å finne inn og ut domenenøkkelen din, gå til:<br/><https://www.entsoe.eu/data/energy-identification-codes-eic/eic-area-codes-map/>                                                                                                                                                                                                                                                                                        |
| `out_domain` | som`in_domain`                                                                                                                                                                                                                                                                                                                                                                                                                |
| `primary`    | Hvis dette markedet er aktivert, setter dette punktet det som det primære markedet                                                                                                                                                                                                                                                                                                                                            |
| `enabled`    | For å bruke denne oppføringen må den være det`enabled`. Ellers`disabled`                                                                                                                                                                                                                                                                                                                                                      |

### Tibber

| Innstilling  | Betydning                                                                                                                                                                                                                                                                                                                    |
| :----------- | :--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `api_token`  | For å få tibber_api_key:<br/>1. logg inn med gratis eller kunde Tibber-konto på<https://developer.tibber.com/settings/access-token><br/>2. Lag et token ved å velge omfanget du trenger (velg "pris")<br/>3. Bruk denne lenken for å opprette en gratis konto med smarttelefonen din:<https://tibber.com/de/invite/ojgfbx2e> |
| `price_unit` | Satt til:<br/>"energi" for å bruke spotmarkedsprisene (standard),<br/>"totalt" for å bruke totalprisene inkludert skatter og avgifter,<br/>"skatt" for å bruke bare skatter og avgifter                                                                                                                                      |
| `primary`    | Hvis dette markedet er aktivert, setter dette punktet det som det primære markedet                                                                                                                                                                                                                                           |
| `enabled`    | For å bruke denne oppføringen må den være det`enabled`. Ellers`disabled`                                                                                                                                                                                                                                                     |

## PV paneler

| Innstilling | Betydning                                                                       |
| :---------- | :------------------------------------------------------------------------------ |
| `LocLat`    | Breddegrad                                                                      |
| `LocLon`    | Lengdegrad                                                                      |
| `angle`     | Vinkelen på panelene dine 0 (horisontal) … 90 (vertikal)                        |
| `direction` | Planasimut, -180 … 180 (-180 = nord, -90 = øst, 0 = sør, 90 = vest, 180 = nord) |
| `totPower`  | installerte moduler effekt i kilowatt                                           |
| `enabled`   | For å bruke denne oppføringen må den være det`enabled`. Ellers`disabled`        |

* * *

## Loggnivåer

### `ERROR`

De`ERROR`loggnivå indikerer feiltilstander i en applikasjon som hindrer utførelse av en spesifikk operasjon. Selv om applikasjonen kan fortsette å fungere med redusert funksjonalitet eller ytelse,<br/>`ERROR`logger indikerer problemer som bør undersøkes umiddelbart.

### `WARN`

Hendelser logget på`WARN`nivå indikerer vanligvis at noe uventet har
skjedde, men applikasjonen kan fortsette å fungere normalt inntil videre.
Det brukes også til å angi forhold som bør tas opp umiddelbart før de
eskalere til problemer for applikasjonen.

### `INFO`

De`INFO`nivå fanger opp hendelser i systemet som er viktige for
applikasjonens forretningsformål. Slike hendelser logges for å vise at systemet er det
fungerer normalt. Produksjonssystemer bruker vanligvis logging på dette nivået
slik at et sammendrag av applikasjonens normale oppførsel er synlig for alle
 gjennomgang av loggene.

### `DEBUG`

De`DEBUG`nivå brukes til å logge meldinger som hjelper utviklere med å identifisere
problemer under en feilsøkingsøkt. Innholdet i meldingene logget på DEBUG
nivå vil variere avhengig av søknaden din, men de inneholder vanligvis
detaljert informasjon som hjelper utviklerne med å feilsøke problemer
effektivt. Dette kan inkludere variablers tilstand innenfor det omkringliggende omfanget eller
relevante feilkoder. |

## Inspirasjon

Ideen er inspirert av @christian1980nrw-prosjektet som er lenket nedenfor. Dette prosjektet er mitt første med Victron Venus OS, så jeg tok i bruk noen ideer og tilnærminger fra følgende prosjekter. Tilnærmingen er den samme, og for veldig smale systemer er implementeringen med et bash-skript sannsynligvis bedre

##### – tusen takk for at du formidlet kunnskapen:

-   [Spotmarket-Switcher](https://github.com/christian1980nrw/Spotmarket-Switcher)
-   [dynamisk-ess](https://github.com/tfranssen/dynamic-ess)
