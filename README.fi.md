![Logo](views/static/images/logo-seuss.png?raw=true "SEUSS")

# SEUSS

### [SEUSS -> Smart Ess Unit Spotmarket Switcher]

#### Ilmoita virheistä ja ehdota parannuksia. Kiitos kaikille jo osallistuneille.

###### Jos haluat osallistua tähän laajennuksiin, lähetä vetopyyntö kehittäjähaarassa. Virheenkorjauksia varten vetopyyntö voidaan tehdä myös päähaarassa

### Mitä tämä ohjelmisto tekee?

Tämä on Python 3 -sovellus, joka käynnistää ESS-yksikön (ohjaimen) oikeaan aikaan, kun tunnin dynaamiset energiahinnat ovat alhaiset. Tai käytetään purkamiseen, kun hinnat ovat erittäin korkeat.

#### Tällä hetkellä tuettuja järjestelmiä ovat:

### ESS-yksiköt

* * *

-   **_Victron Venus OS -energian varastointijärjestelmät, kuten MultiPlus II -sarja_**

* * *

### Spot-markkinat

* * *

-   **_vastaus_**
-   **_Enzo-E_**
-   **_Tibber_**

* * *

ESS-yksikön (ohjaimen) ohjaus tapahtuu mqtt:n kautta. Tämän ohjauksen etu on:
että tämän sovelluksen ei tarvitse toimia suoraan VenusOS:ssä. Suora ohjaus D-BUS:lla on työn alla

# Testattu

Tämä versio onnistui

* * *

-   **_Linux Ubuntu >= 22.04_**
-   **_Venus OS Raspberries >= vz.12_**

* * *

testattu

# Asentaa

Lataa asennusskripti GitHub-arkistosta ja suorita seuraava komento päätteessäsi:

    wget -O seuss_install.sh https://raw.githubusercontent.com/ckvsoft/SEUSS/dev/scripts/seuss_install.sh`

Suorita asennuskomentosarja lisäasetuksineen valmistaaksesi kaiken alihakemistossa tarkastusta varten. Esimerkiksi:

    bash seuss_install.sh`

Oletushakemisto on /data/seuss (Venus OS) Mutta voit halutessasi määrittää toisen hakemiston käyttämällä ympäristömuuttujaa TARGET_DIRECTORY esim.

    TARGET_DIRECTORY=/opt/seuss bash seuss_install.sh`

Cerbo GX:ssä tiedostojärjestelmä on asennettu vain luku -tilassa. Katso<https://www.victronenergy.com/live/ccgx:root_access>.
Jotta tiedostojärjestelmästä tulee kirjoitettava, sinun on suoritettava seuraava komento ennen asennuskomentosarjan suorittamista:

    /opt/victronenergy/swupdate-scripts/resize2fs.sh

# Kokoonpano

Jälkeen`SEUSS`on asennettu onnistuneesti, verkkosivusto on saatavilla IP-osoitteessa ja portissa 5000`Computer/VenusOS`jonka päällä`SEUSS`asennettiin.

-   Voit tarkastella tai ladata lokitiedoston.
-   Lisäksi konfigurointi voidaan suorittaa käyttämällä[Asetuseditori]valikon kohta.
-   Tässä näkyvät työkaluvinkit useimpiin pisteisiin.

#### Lokin katseluohjelma

-   ![Logo](views/static/images/logviewer.png?raw=true "SEUSS Log Viewer")

#### Konfigurointieditori - ESS-yksiköt

-   ![Logo](views/static/images/configeditor_ess.png?raw=true "SEUSS Config Editor")

#### Konfigurointieditori - PV-paneelit

-   ![Logo](views/static/images/configeditor_panels.png?raw=true "SEUSS Config Editor")

Ne löytyvät myös Asetukset-kuvauksesta.
Niille, jotka haluavat työskennellä asetustiedostossa, on config.json

# asetukset

## Kenraali

| Asetus          | Merkitys                                                                                                                                |
| --------------- | --------------------------------------------------------------------------------------------------------------------------------------- |
| `time_zone`     | Olennainen toimintojen oikea ajoitus maantieteellisen sijaintisi perusteella.<br/>Muotoile kuten`Europe/Vienna`,`Europe/Amsterdam`, ... |
| `log_file_path` | Asettaa vaihtoehtoisen polun, johon lokitiedostot tallennetaan.                                                                         |
| `log_level`     | Käytetyt lokitasot ovat:`INFO`,`WARNING`,`ERROR`ja`DEBUG`. katso[Lokitasot](#loglevels)                                                 |

## hinnat

#### Muuta hintoja (käytä aina senttiä/kWh, riippumatta siitä, käytätkö Awattaria (näyttö Cent/kWh) vai Entsoe API:ta (näyttö EUR/MWh) / nettohinnat ilman veroja).

| Asetus                                     | Merkitys                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
| ------------------------------------------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `use_second_day`                           | `enable/disable`vertailla tämän päivän ja huomisen hintoja, jos niitä tulee saataville<br/>Huomaa: Jos aktivoit tämän ja hinnat laskevat useiden päivien aikana, on mahdollista, että maksua tai vaihtoa ei tapahdu useisiin päiviin, kunnes alhaisimmat hinnat saavutetaan.                                                                                                                                                                                                                                                  |
| `number_of_lowest_prices_for_charging`     | Tässä voidaan käyttää kahta tilaa.<br/>tila1:<br/>_halvimpien hintojen määrä, joilla latauksen pitäisi/voi tapahtua. Tässä syötetään kokonaislukuja<br/>tila2:<br/>_Tässä hintojen lukumäärä määräytyy keskihinnan perusteella. Tässä tilassa syötät desimaalilukuja. Esim. 0,85 saadaksesi kaikki hinnat, jotka ovat 85 % keskiarvon alapuolella. Tässä on merkitystä pilkkuarvon määrittelyllä. Arvolla 1.0 oletetaan, että keskihinnasta otetaan 100 % (ei mitään järkeä), mutta jos syötetään 1, se on 1 halvin hinta     |
| `number_of_highest_prices_for_discharging` | Tässä voidaan käyttää kahta tilaa.<br/>tila1:<br/>_kalleimpien hintojen määrä, joilla purkaminen pitäisi/voi tapahtua. Tässä syötetään kokonaislukuja<br/>tila2:<br/>_Tässä hintojen lukumäärä määräytyy keskihinnan perusteella. Tässä tilassa syötät desimaalilukuja. Esim. 1,25 saadaksesi kaikki hinnat, jotka ovat 25 % keskiarvon yläpuolella.<br/>Tässä on olennaista pilkkuarvon määrittely. Arvolla 1.0 oletetaan, että keskihinnasta otetaan 100 % (ei mitään järkeä), mutta jos syötetään 1, se on 1 kallein hinta |
| `charging_price_limit`                     | lataus on aina käytössä tämän hinnan alapuolella<br/>kalleimpien hintojen lukumäärä, joilla tyhjennys pitäisi/voidaan suorittaa                                                                                                                                                                                                                                                                                                                                                                                               |

## ESS-yksiköt

### Victron

| Asetus                | Merkitys                                                                                                                                                                                                                                                                                                                                                                                                            |
| :-------------------- | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `use_vrm`             | Jos tämä piste on käytössä (tosi), Victroniin yritetään muodostaa yhteys VRM-portaalin kautta.<br/>Tämä vaatii käyttäjän/salasanan VRM-portaalissa                                                                                                                                                                                                                                                                  |
| `ip_address`          | Victronin paikallinen IP-osoite.<br/>Tämä vaaditaan, jos`use_vrm`on poistettu käytöstä (false).<br/>Muuten tämä kenttä jää tyhjäksi                                                                                                                                                                                                                                                                                 |
| `unit_id`             | VRM-portaalin tunnus<br/>löytyy osoitteesta`Settings / VRM online portal / VRM Portal Id`.<br/>Huomautus: Tämä tunnus vaaditaan Victroniin pääsyyn, vaikka et käyttäisi VRM-portaalia                                                                                                                                                                                                                               |
| `user`                | sähköpostiosoite, jota käytät yhteyden muodostamiseen VRM-portaaliin                                                                                                                                                                                                                                                                                                                                                |
| `password`            | salasana, jota käytät yhteyden muodostamiseen VRM-portaaliin                                                                                                                                                                                                                                                                                                                                                        |
| `max_discharge_power` | Oletus: -1<br/>Jos käytät`Limit inverter power`ESS-valikossa, tämä arvo on syötettävä tähän.<br/>Jos invertteri on asetettu asentoon`Discharge false`Tämän sovelluksen avulla tämä arvo korvataan ESS:ssä.<br/>Tämä raja tässä asetetaan purkaustilassa ESS:ssä.<br/>Jos rajaa ei ole asetettu, jätä arvo arvoon`-1`.<br/>Esimerkki: Enter`1000`purkamisen rajoittamiseksi`1000W`, Tulla sisään`-1`täydelle teholle |
| `only_observation`    | Jos`only observation`on aktivoitu, yksikköä käytetään vain tilastollisiin tarkoituksiin. Essunit ei täytä mitään ehtoja                                                                                                                                                                                                                                                                                             |
| `enabled`             | Jotta voit käyttää tätä merkintää, sen on oltava`enabled`. Muuten`disabled`                                                                                                                                                                                                                                                                                                                                         |

## Spot-markkinat

### vastaus

| Asetus    | Merkitys                                                                         |
| :-------- | :------------------------------------------------------------------------------- |
| `country` | Valitse sijainti AT tai DE                                                       |
| `primary` | Jos tämä markkina on käytössä, tämä kohta asettaa sen ensisijaiseksi markkinaksi |
| `enabled` | Jotta voit käyttää tätä merkintää, sen on oltava`enabled`. Muuten`disabled`      |

### Enzo on

| Asetus       | Merkitys                                                                                                                                                                                                                                                                                                                                                                                                                            |
| :----------- | :---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `api_token`  | Kuinka saada ilmainen api-suojaustunnus:<br/>1. Siirry kohtaan<https://transparency.entsoe.eu/> --> register and create an account<br/>2. Lähetä sähköposti osoitteeseen[transparency@entsoe.eu](mailto:transparency@entsoe.eu)otsikkorivillä "Restful API access".<br/>3. ENTSO-E Helpdesk vastaa pyyntöösi 3 työpäivän kuluessa.<br/>4. Luo suojaustunnus osoitteessa<https://transparency.entsoe.eu/usrm/user/myAccountSettings> |
| `in_domain`  | Voit selvittää verkkotunnuksesi sisään- ja ulostuloavaimesi osoitteessa:<br/><https://www.entsoe.eu/data/energy-identification-codes-eic/eic-area-codes-map/>                                                                                                                                                                                                                                                                       |
| `out_domain` | Kuten`in_domain`                                                                                                                                                                                                                                                                                                                                                                                                                    |
| `primary`    | Jos tämä markkina on käytössä, tämä kohta asettaa sen ensisijaiseksi markkinaksi                                                                                                                                                                                                                                                                                                                                                    |
| `enabled`    | Jotta voit käyttää tätä merkintää, sen on oltava`enabled`. Muuten`disabled`                                                                                                                                                                                                                                                                                                                                                         |

### Tibber

| Asetus       | Merkitys                                                                                                                                                                                                                                                                                                                           |
| :----------- | :--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `api_token`  | Näin saat tibber_api_keyn:<br/>1. kirjaudu sisään ilmaisella tai asiakkaan Tibber-tilillä osoitteessa<https://developer.tibber.com/settings/access-token><br/>2. Luo tunnus valitsemalla tarvitsemasi laajuudet (valitse "hinta")<br/>3. Luo ilmainen tili älypuhelimellasi tästä linkistä:<https://tibber.com/de/invite/ojgfbx2e> |
| `price_unit` | Asetettu:<br/>"energiaa" spotmarket-hintojen käyttämiseen (oletus),<br/>"yhteensä" käyttää kokonaishintoja, mukaan lukien verot ja maksut,<br/>"vero" käyttää vain veroja ja maksuja                                                                                                                                               |
| `primary`    | Jos tämä markkina on käytössä, tämä kohta asettaa sen ensisijaiseksi markkinaksi                                                                                                                                                                                                                                                   |
| `enabled`    | Jotta voit käyttää tätä merkintää, sen on oltava`enabled`. Muuten`disabled`                                                                                                                                                                                                                                                        |

## PV-paneelit

| Asetus            | Merkitys                                                                                           |
| :---------------- | :------------------------------------------------------------------------------------------------- |
| `locLat`          | Leveysaste                                                                                         |
| `locLong`         | Pituusaste                                                                                         |
| `angle`           | Paneeleidesi kulma 0 (vaaka) … 90 (pysty)                                                          |
| `direction`       | Tason atsimuutti, -180 … 180 (-180 = pohjoinen, -90 = itä, 0 = etelä, 90 = länsi, 180 = pohjoinen) |
| `totPower`        | asennettujen moduulien teho kilowatteina                                                           |
| `total_area`      | Paneeleiden kokonaispinta-ala neliömetrinä                                                         |
| `damping_morning` | Tällä parametrilla voit säätää tulosta aamulla. Kelluva arvo 0..1, oletusarvo 0                    |
| `damping_evening` | Tällä parametrilla voit säätää tulosta illalla. Kelluva arvo 0..1, oletusarvo 0                    |
| `enabled`         | Jotta voit käyttää tätä merkintää, sen on oltava`enabled`. Muuten`disabled`                        |

* * *

## Lokitasot

### `ERROR`

The`ERROR`lokitaso ilmaisee sovelluksen virhetilanteita, jotka estävät tietyn toiminnon suorittamisen. Vaikka sovellus voi jatkaa toimintaansa alentuneella toiminnallisuuden tai suorituskyvyn tasolla,<br/>`ERROR`lokit merkitsevät ongelmia, jotka tulisi tutkia viipymättä.

### `WARN`

Tapahtumat kirjattu osoitteessa`WARN`taso viittaa tyypillisesti siihen, että jotain odottamatonta on
tapahtui, mutta sovellus voi jatkaa toimintaansa normaalisti toistaiseksi.
Sitä käytetään myös merkitsemään ehtoja, jotka tulisi käsitellä viipymättä ennen niitä
kasvaa sovelluksen ongelmiksi.

### `INFO`

The`INFO`taso kaappaa järjestelmän tapahtumat, jotka ovat tärkeitä
sovelluksen liiketoiminnallinen tarkoitus. Tällaiset tapahtumat kirjataan osoittamaan, että järjestelmä on
toimivat normaalisti. Tuotantojärjestelmät kirjaavat yleensä oletuksena tällä tasolla
jotta yhteenveto sovelluksen normaalista toiminnasta näkyy kaikille
 lokien tarkistaminen.

### `DEBUG`

The`DEBUG`tasoa käytetään sellaisten viestien kirjaamiseen, jotka auttavat kehittäjiä tunnistamaan
ongelmia virheenkorjausistunnon aikana. DEBUGissa kirjattujen viestien sisältö
taso vaihtelee sovelluksesi mukaan, mutta ne sisältävät yleensä
yksityiskohtaisia ​​tietoja, jotka auttavat sen kehittäjiä vianmäärityksessä
tehokkaasti. Tämä voi sisältää muuttujien tilan ympäröivässä laajuudessa tai
asiaankuuluvat virhekoodit. |

## Inspiraatiota

Idea on saanut inspiraationsa alla linkitetystä @christian1980nrw-projektista. Tämä projekti on ensimmäinen Victron Venus OS -käyttöjärjestelmän kanssa, joten otin käyttöön joitain ideoita ja lähestymistapoja seuraavista projekteista. Lähestymistapa on sama ja erittäin kapeille järjestelmille toteutus bash-skriptillä on luultavasti parempi

##### – kiitos kovasti tiedon välittämisestä:

-   [Spot-markkinoiden vaihtaja](https://github.com/christian1980nrw/Spotmarket-Switcher)
-   [dynaaminen-ess](https://github.com/tfranssen/dynamic-ess)
