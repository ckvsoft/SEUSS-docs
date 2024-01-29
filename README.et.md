![Logo](views/static/images/logo-seuss.png?raw=true "SEUSS")

# SEUSS

### [SEUSS -> Smart Ess Unit Spotmarket Switcher]

#### Teatage vigadest ja soovitage parandusi. Aitäh kõigile, kes on juba osa võtnud.

###### Kui soovite sellesse laiendusi panustada, esitage tõmbetaotlus arendusharus. Veaparandusteks saab tõmbetaotluse teha ka põhiharus

### Mida see tarkvara teeb?

See on Python 3 rakendus, mis lülitab teie ESS-seadme (kontrolleri) sisse õigel ajal, kui teie tunnipõhised dünaamilised energiahinnad on madalad. Või kasutatakse tühjendamiseks, kui hinnad on väga kõrged.

#### Praegu toetatud süsteemid on:

### ESS üksused

* * *

-   **_Victron Venus OS-i energiasalvestussüsteemid, näiteks MultiPlus II seeria_**

* * *

### Kohalikud turud

* * *

-   **_vastama_**
-   **_Enzo-E_**
-   **_Tibber_**

* * *

ESS üksuse (kontrolleri) juhtimine toimub mqtt kaudu. Selle kontrolli eelised on järgmised:
et see rakendus ei pea töötama otse VenusOS-is. Töös on otsejuhtimine D-BUSiga

# Testitud

See versioon oli edukas

* * *

-   **_Linux Ubuntu >= 22.04_**
-   **_Venus OS Vaarikad >= vz.12_**

* * *

testitud

# Installige

Laadige GitHubi hoidlast alla installiskript ja käivitage terminalis järgmine käsk:

    wget -O seuss_install.sh https://raw.githubusercontent.com/ckvsoft/SEUSS/dev/scripts/seuss_install.sh`

Käivitage installiskript koos lisavalikutega, et alamkataloogis kõik kontrollimiseks ette valmistada. Näiteks:

    bash seuss_install.sh`

Vaikekataloog on /data/seuss (Venus OS) Kuid valikuliselt saate määrata ka teistsuguse kataloogi, kasutades keskkonnamuutujat TARGET_DIRECTORY nt.

    TARGET_DIRECTORY=/opt/seuss bash seuss_install.sh`

Cerbo GX-ile on failisüsteem ühendatud ainult lugemiseks. Vaata<https://www.victronenergy.com/live/ccgx:root_access>.
Failisüsteemi kirjutatavaks muutmiseks peate enne installiskripti käivitamist käivitama järgmise käsu:

    /opt/victronenergy/swupdate-scripts/resize2fs.sh

# Seadistamine

Pärast`SEUSS`on edukalt installitud, on veebisait saadaval IP-aadressil ja pordil 5000`Computer/VenusOS`mille peal`SEUSS`paigaldati.

-   Saate logifaili vaadata või alla laadida.
-   Lisaks saab konfiguratsiooni teostada kasutades[Konfiguratsiooniredaktor]menüüelement.
-   Siin kuvatakse enamiku punktide tööriistanäpunäiteid.

#### Logi vaataja

-   ![Logo](views/static/images/logviewer.png?raw=true "SEUSS Log Viewer")

#### Konfiguratsiooniredaktor – ESS-i üksused

-   ![Logo](views/static/images/configeditor_ess.png?raw=true "SEUSS Config Editor")

#### Konfiguratsiooniredaktor – PV-paneelid

-   ![Logo](views/static/images/configeditor_panels.png?raw=true "SEUSS Config Editor")

Need leiate ka seadete kirjeldusest.
Neile, kes eelistavad töötada konfiguratsioonifailis, on olemas config.toml

# Seaded

## Kindral

| Seadistamine    | Tähendus                                                                                                                                     |
| --------------- | -------------------------------------------------------------------------------------------------------------------------------------------- |
| `time_zone`     | Teie geograafilisest asukohast lähtuvate toimingute õige ajastamise jaoks hädavajalik.<br/>Vormi nagu`Europe/Vienna`,`Europe/Amsterdam`, ... |
| `log_file_path` | Määrab alternatiivse tee, kuhu logifailid salvestatakse.                                                                                     |
| `log_level`     | Kasutatud logitasemed on:`INFO`,`WARNING`,`ERROR`ja`DEBUG`. see[Logi tasemed](#loglevels)                                                    |

## Hinnad

#### Palun muutke hindu (kasutage alati senti/kWh, olenemata sellest, kas kasutate Awattari (kuvab senti/kWh) või Entsoe API-d (kuvatakse EUR/MWh) / netohinnad ilma käibemaksuta).

| Seadistamine                               | Tähendus                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| ------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `use_second_day`                           | `enable/disable`võrrelda tänaseid ja homseid hindu, kui need saadavale tulevad<br/>Märkus: Kui aktiveerite selle ja hinnad langevad mitme päeva jooksul, on võimalik, et mitu päeva ei võeta tasu ega lülituta kuni madalaimate hindadeni.                                                                                                                                                                                                                                                              |
| `number_of_lowest_prices_for_charging`     | Siin saab kasutada kahte režiimi.<br/>režiim1:<br/>_odavaimate hindade arv, millega laadimine peaks/võib toimuda. Siin sisestate täisarvud<br/>režiim2:<br/>_Siin määratakse hindade arv keskmise hinna alusel. Selle režiimi jaoks sisestate kümnendarvud. Nt. 0,85, et saada kõik hinnad, mis on 85% keskmisest madalamad. Siin on asjakohane koma väärtuse täpsustamine. 1.0 puhul eeldatakse, et võetakse 100% keskmisest hinnast (pole mõtet) aga kui sisestada 1 on 1 odavaim hind                |
| `number_of_highest_prices_for_discharging` | Siin saab kasutada kahte režiimi.<br/>režiim1:<br/>_kõige kallimate hindade arv, millega tühjendamine peaks/võib toimuda. Siin sisestate täisarvud<br/>režiim2:<br/>_Siin määratakse hindade arv keskmise hinna alusel. Selle režiimi jaoks sisestate kümnendarvud. Nt. 1.25, et saada kõik hinnad, mis on 25% keskmisest kõrgemad.<br/>Siin on asjakohane komaväärtuse täpsustamine. 1.0 puhul eeldatakse, et võetakse 100% keskmisest hinnast (pole mõtet) aga kui 1 sisestada on 1 kõige kallim hind |
| `charging_price_limit`                     | laadimine on alati lubatud alla selle hinna<br/> the number of the most expensive prices at which discharging should/may be carried out                                                                                                                                                                                                                                                                                                                                                                 |

## ESS üksused

### Victron

| Seadistamine          | Tähendus                                                                                                                                                                                                                                                                                                                                                                                                                |
| :-------------------- | :---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `use_vrm`             | Kui see punkt on lubatud (tõene), üritatakse VRM-i portaali kaudu Victroniga ühendust luua.<br/>Selleks on vaja VRM-i portaalis kasutajat/parooli                                                                                                                                                                                                                                                                       |
| `ip_address`          | Victroni kohalik IP-aadress.<br/>See on vajalik, kui`use_vrm`on keelatud (false).<br/>Vastasel juhul jääb see väli tühjaks                                                                                                                                                                                                                                                                                              |
| `unit_id`             | VRM-i portaali ID<br/>leiate aadressilt`Settings / VRM online portal / VRM Portal Id`.<br/>Märkus. See ID on vajalik Victroni juurdepääsuks isegi siis, kui te ei kasuta VRM-i portaali                                                                                                                                                                                                                                 |
| `user`                | meiliaadress, mida kasutate VRM-i portaaliga ühenduse loomiseks                                                                                                                                                                                                                                                                                                                                                         |
| `password`            | parool, mida kasutate VRM-i portaaliga ühenduse loomiseks                                                                                                                                                                                                                                                                                                                                                               |
| `max_discharge_power` | Vaikimisi: -1<br/>Kui kasutate`Limit inverter power`ESS menüüs siis tuleb see väärtus siia sisestada.<br/>Kui inverter on seatud`Discharge false`selle rakendusega kirjutatakse see väärtus ESS-is üle.<br/>See piirang on siin seatud ESS-i tühjendusrežiimis.<br/>Kui piirangut pole määratud, jätke väärtus väärtusele`-1`.<br/>Näide: sisestage`1000`tühjenemise piiramiseks`1000W`, Sisenema`-1`täisvõimsuse jaoks |
| `primary`             | Kui see turg on lubatud, määrab see punkt selle esmaseks turuks                                                                                                                                                                                                                                                                                                                                                         |
| `enabled`             | Selle kirje kasutamiseks peab see olema`enabled`. Muidu`disabled`                                                                                                                                                                                                                                                                                                                                                       |

## Kohalikud turud

### vastama

| Seadistamine | Tähendus                                                          |
| :----------- | :---------------------------------------------------------------- |
| `country`    | Valige asukoht AT või DE                                          |
| `primary`    | Kui see turg on lubatud, määrab see punkt selle esmaseks turuks   |
| `enabled`    | Selle kirje kasutamiseks peab see olema`enabled`. Muidu`disabled` |

### Enzo on

| Seadistamine | Tähendus                                                                                                                                                                                                                                                                                                                                                                                                              |
| :----------- | :-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `api_token`  | Kuidas hankida tasuta API turvamärk:<br/>1. Mine lehele<https://transparency.entsoe.eu/>--> registreeru ja loo konto<br/>2. Saada meil aadressile[transparency@entsoe.eu](mailto:transparency@entsoe.eu)teemareal on "Rahulik API juurdepääs".<br/>3. ENTSO-E kasutajatugi vastab teie päringule 3 tööpäeva jooksul.<br/>4. Genereeri turvamärk aadressil<https://transparency.entsoe.eu/usrm/user/myAccountSettings> |
| `in_domain`  | Sisse- ja väljamineku domeenivõtme leidmiseks minge aadressile:<br/><https://www.entsoe.eu/data/energy-identification-codes-eic/eic-area-codes-map/>                                                                                                                                                                                                                                                                  |
| `out_domain` | meeldib`in_domain`                                                                                                                                                                                                                                                                                                                                                                                                    |
| `primary`    | Kui see turg on lubatud, määrab see punkt selle esmaseks turuks                                                                                                                                                                                                                                                                                                                                                       |
| `enabled`    | Selle kirje kasutamiseks peab see olema`enabled`. Muidu`disabled`                                                                                                                                                                                                                                                                                                                                                     |

### Tibber

| Seadistamine | Tähendus                                                                                                                                                                                                                                                                                                                                     |
| :----------- | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `api_token`  | Tibber_api_key hankimiseks tehke järgmist.<br/>1. logige sisse tasuta või kliendi Tibberi kontoga aadressil<https://developer.tibber.com/settings/access-token><br/>2. Looge tunnus, valides vajalikud ulatused (valige "hind")<br/>3. Kasutage seda linki oma nutitelefoniga tasuta konto loomiseks:<https://tibber.com/de/invite/ojgfbx2e> |
| `price_unit` | Seatud:<br/>"energia", et kasutada hetketuru hindu (vaikimisi),<br/>"kokku", et kasutada koguhindu koos maksude ja lõivudega,<br/>"maks", et kasutada ainult makse ja tasusid                                                                                                                                                                |
| `primary`    | Kui see turg on lubatud, määrab see punkt selle esmaseks turuks                                                                                                                                                                                                                                                                              |
| `enabled`    | Selle kirje kasutamiseks peab see olema`enabled`. Muidu`disabled`                                                                                                                                                                                                                                                                            |

## PV paneelid

| Seadistamine | Tähendus                                                                                    |
| :----------- | :------------------------------------------------------------------------------------------ |
| `LocLat`     | Laiuskraad                                                                                  |
| `LocLon`     | Pikkuskraad                                                                                 |
| `angle`      | Teie paneelide nurk 0 (horisontaalne) … 90 (vertikaalne)                                    |
| `direction`  | Tasapinna asimuut, -180 … 180 (-180 = põhja, -90 = ida, 0 = lõuna, 90 = lääne, 180 = põhja) |
| `totPower`   | paigaldatud moodulite võimsus kilovattides                                                  |
| `enabled`    | Selle kirje kasutamiseks peab see olema`enabled`. Muidu`disabled`                           |

* * *

## Logitasemed

### `ERROR`

The`ERROR`logi tase näitab veatingimusi rakenduses, mis takistavad konkreetse toimingu täitmist. Kuigi rakendus võib jätkata töötamist vähendatud funktsionaalsuse või jõudluse tasemel,<br/>`ERROR`logid tähistavad probleeme, mida tuleks kiiresti uurida.

### `WARN`

Sündmused, mis on logitud aadressil`WARN`tase näitab tavaliselt midagi ootamatut
juhtus, kuid rakendus võib esialgu normaalselt edasi töötada.
Seda kasutatakse ka tingimuste tähistamiseks, millega tuleks enne nende tegemist viivitamatult tegeleda
areneda rakendusega seotud probleemideks.

### `INFO`

The`INFO`tase hõlmab sündmusi, mis on süsteemi jaoks olulised
rakenduse äriline eesmärk. Sellised sündmused logitakse, et näidata, et süsteem on
töötab normaalselt. Tootmissüsteemid logivad tavaliselt sellel tasemel vaikimisi
nii et rakenduse tavapärase käitumise kokkuvõte oleks kõigile nähtav
 logide ülevaatamine.

### `DEBUG`

The`DEBUG`taset kasutatakse sõnumite logimiseks, mis aitavad arendajatel tuvastada
probleemid silumisseansi ajal. SILUMISEL logitud sõnumite sisu
tase varieerub olenevalt teie rakendusest, kuid tavaliselt sisaldavad need
üksikasjalik teave, mis aitab selle arendajatel probleeme tõrkeotsingul teha
tõhusalt. See võib hõlmata muutujate olekut ümbritsevas ulatuses või
asjakohased veakoodid. |

## Inspiratsioon

Idee on inspireeritud allpool lingitud projektist @christian1980nrw. See projekt on minu esimene Victron Venus OS-iga, seega võtsin kasutusele mõned ideed ja lähenemisviisid järgmistest projektidest. Lähenemisviis on sama ja väga kitsaste süsteemide puhul on bash-skriptiga realiseerimine ilmselt parem

##### – suur tänu teadmiste edasiandmise eest:

-   [Kohtturu vahetaja](https://github.com/christian1980nrw/Spotmarket-Switcher)
-   [dünaamiline-ess](https://github.com/tfranssen/dynamic-ess)
