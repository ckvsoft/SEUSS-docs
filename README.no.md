![Logo](views/static/images/logo-seuss.png?raw=true "SEUSS")

# SEUSS

#### [SEUSS -> Smart Ess Unit Spotmarket Switcher]

# Innstillinger

## Generell

| Innstilling     | Betydning                                                                                                                              |
| --------------- | -------------------------------------------------------------------------------------------------------------------------------------- |
| `time_zone`     | Viktig for korrekt timing av operasjoner basert på din geografiske plassering.<br/>Formater som`Europe/Vienna`,`Europe/Amsterdam`, ... |
| `log_file_path` | Angir en alternativ bane som loggfilene lagres til.                                                                                    |
| `log_level`     | Brukte loggnivå er: INFO, ADVARSEL, FEIL og DEBUG. se[Loggnivåer](#loglevels)                                                          |

## Priser

| Innstilling                                | Betydning                                                                                                                                                                                                                                                                   |
| ------------------------------------------ | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `use_second_day`                           | aktiver/deaktiver for å sammenligne dagens og morgendagens priser hvis de blir tilgjengelige<br/>Merk: Hvis du aktiverer dette og prisene synker over flere dager, er det mulig at det ikke vil være noen lading eller bytte på flere dager før de laveste prisene er nådd. |
| `number_of_lowest_prices_for_charging`     | antall billigste priser som lasting bør/kan foretas til                                                                                                                                                                                                                     |
| `number_of_highest_prices_for_discharging` | antall dyreste priser som utslipp bør/kan foretas til                                                                                                                                                                                                                       |
| `charging_price_limit`                     | lading er alltid aktivert under denne prisen<br/>antall dyreste priser som utslipp bør/kan foretas til                                                                                                                                                                      |

## ESS-enheter

### Victron

| Innstilling  | Betydning                                                                                                                                                                            |
| :----------- | :----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `use_vrm`    | Hvis dette punktet er aktivert (sant), gjøres det et forsøk på å koble til Victron via VRM-portalen.<br/>Dette krever bruker/passord i VRM-portalen                                  |
| `ip_address` | Den lokale IP-adressen til Victron.<br/>Dette er nødvendig hvis "use_vrm" er deaktivert (false).<br/>Ellers forblir dette feltet tomt                                                |
| `unit_id`    | VRM-portal-ID<br/>finner du i Innstillinger / VRM online portal / VRM Portal Id.<br/>Merk: Denne IDen er nødvendig for å få tilgang til Victron selv om du ikke bruker en VRM-portal |
| `user`       | e-postadresse du bruker for å koble til VRM-portalen                                                                                                                                 |
| `password`   | passordet du bruker for å koble til VRM-portalen                                                                                                                                     |

## Markeder

### svar

| Innstilling | Betydning                                                                          |
| :---------- | :--------------------------------------------------------------------------------- |
| `country`   | Velg plassering AT eller DE                                                        |
| `primary`   | Hvis dette markedet er aktivert, setter dette punktet det som det primære markedet |
| `enabled`   | angi markedet som aktivert/deaktivert                                              |

### Enzo er

| Innstilling  | Betydning                                                                                                                                                                                                                                                                                                                                                                                                                           |
| :----------- | :---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `api_token`  | Slik får du det gratis api-sikkerhetstokenet:<br/>1. Gå til<https://transparency.entsoe.eu/>--> registrer deg og opprett en konto<br/>2. Send en e-post til[transparency@entsoe.eu](mailto:transparency@entsoe.eu)med "Restful API access" i emnelinjen<br/>3. ENTSO-E Helpdesk vil svare på forespørselen din innen 3 virkedager.<br/>4. Generer et sikkerhetstoken på<https://transparency.entsoe.eu/usrm/user/myAccountSettings> |
| `in_domain`  | For å finne inn og ut domenenøkkelen din, gå til:<br/><https://www.entsoe.eu/data/energy-identification-codes-eic/eic-area-codes-map/>                                                                                                                                                                                                                                                                                              |
| `out_domain` | som in_domene                                                                                                                                                                                                                                                                                                                                                                                                                       |
| `primary`    | Hvis dette markedet er aktivert, setter dette punktet det som det primære markedet                                                                                                                                                                                                                                                                                                                                                  |
| `enabled`    | angi markedet som aktivert/deaktivert                                                                                                                                                                                                                                                                                                                                                                                               |

### Tibber

| Innstilling  | Betydning                                                                                                                                                                                                                                                                                                                    |
| :----------- | :--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `api_token`  | For å få tibber_api_key:<br/>1. logg inn med gratis eller kunde Tibber-konto på<https://developer.tibber.com/settings/access-token><br/>2. Lag et token ved å velge omfanget du trenger (velg "pris")<br/>3. Bruk denne lenken for å opprette en gratis konto med smarttelefonen din:<https://tibber.com/de/invite/ojgfbx2e> |
| `price_unit` | Satt til:<br/>"energi" for å bruke spotmarkedsprisene (standard),<br/>"total" to use the total prices including taxes and fees,<br/>"skatt" for å bruke bare skatter og avgifter                                                                                                                                             |
| `primary`    | Hvis dette markedet er aktivert, setter dette punktet det som det primære markedet                                                                                                                                                                                                                                           |
| `enabled`    | angi markedet som aktivert/deaktivert                                                                                                                                                                                                                                                                                        |

* * *

# Loggnivåer

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

De`DEBUG` level is used for logging messages that aid developers in identifying
issues during a debugging session. The content of the messages logged at the DEBUG
level will vary depending on your application, but they typically contain
detailed information that assists its developers in troubleshooting problems
efficiently. This can include variables' state within the surrounding scope or
relevant error codes.                                                                                                                                    |
