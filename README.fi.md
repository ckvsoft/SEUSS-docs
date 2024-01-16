![Logo](views/static/images/logo-seuss.png?raw=true "SEUSS")

# SEUSS

#### [SEUSS -> Smart Ess Unit Spotmarket Switcher]

# asetukset

## Kenraali

| Asetus          | Merkitys                                                                                                                                |
| --------------- | --------------------------------------------------------------------------------------------------------------------------------------- |
| `time_zone`     | Olennainen toimintojen oikea ajoitus maantieteellisen sijaintisi perusteella.<br/>Muotoile kuten`Europe/Vienna`,`Europe/Amsterdam`, ... |
| `log_file_path` | Asettaa vaihtoehtoisen polun, johon lokitiedostot tallennetaan.                                                                         |
| `log_level`     | Käytetyt lokitasot ovat: INFO, WARNING, ERROR ja DEBUG. katso[Lokitasot](#loglevels)                                                    |

## hinnat

| Asetus                                     | Merkitys                                                                                                                                                                                                                                                                                       |
| ------------------------------------------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `use_second_day`                           | Ota käyttöön tai poista käytöstä tämän päivän ja huomisen hintojen vertailu, jos ne tulevat saataville<br/>Huomaa: Jos aktivoit tämän ja hinnat laskevat useiden päivien aikana, on mahdollista, että laskutusta tai vaihtoa ei tapahdu useaan päivään, kunnes alhaisimmat hinnat saavutetaan. |
| `number_of_lowest_prices_for_charging`     | halvimpien hintojen määrä, jolla lastaus pitäisi/voidaan tehdä                                                                                                                                                                                                                                 |
| `number_of_highest_prices_for_discharging` | kalleimpien hintojen lukumäärä, joilla tyhjennys pitäisi/voidaan suorittaa                                                                                                                                                                                                                     |
| `charging_price_limit`                     | lataus on aina käytössä tämän hinnan alapuolella<br/>kalleimpien hintojen lukumäärä, joilla tyhjennys pitäisi/voidaan suorittaa                                                                                                                                                                |

## ESS-yksiköt

### Victron

| Asetus       | Merkitys                                                                                                                                                                             |
| :----------- | :----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `use_vrm`    | Jos tämä piste on käytössä (tosi), Victroniin yritetään muodostaa yhteys VRM-portaalin kautta.<br/>This requires a user/password in the VRM portal                                   |
| `ip_address` | Victronin paikallinen IP-osoite.<br/>Tämä on pakollinen, jos "use_vrm" on poistettu käytöstä (false).<br/>Muuten tämä kenttä jää tyhjäksi                                            |
| `unit_id`    | VRM-portaalin tunnus<br/>löytyy kohdasta Asetukset / VRM online-portaali / VRM Portal Id.<br/>Huomautus: Tämä tunnus vaaditaan Victroniin pääsyyn, vaikka et käyttäisi VRM-portaalia |
| `user`       | sähköpostiosoite, jota käytät yhteyden muodostamiseen VRM-portaaliin                                                                                                                 |
| `password`   | salasana, jota käytät yhteyden muodostamiseen VRM-portaaliin                                                                                                                         |

## Markkinat

### vastaus

| Asetus    | Merkitys                                                                         |
| :-------- | :------------------------------------------------------------------------------- |
| `country` | Valitse sijainti AT tai DE                                                       |
| `primary` | Jos tämä markkina on käytössä, tämä kohta asettaa sen ensisijaiseksi markkinaksi |
| `enabled` | aseta markkinasi käyttöön/pois käytöstä                                          |

### Enzo on

| Asetus       | Merkitys                                                                                                                                                                                                                                                                                                                                                                                                                     |
| :----------- | :--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `api_token`  | Kuinka saada ilmainen api-suojaustunnus:<br/>1. Siirry kohtaan<https://transparency.entsoe.eu/>--> rekisteröidy ja luo tili<br/>2. Lähetä sähköposti osoitteeseen[transparency@entsoe.eu](mailto:transparency@entsoe.eu)otsikkorivillä "Restful API access".<br/>3. ENTSO-E Helpdesk vastaa pyyntöösi 3 työpäivän kuluessa.<br/>4. Luo suojaustunnus osoitteessa<https://transparency.entsoe.eu/usrm/user/myAccountSettings> |
| `in_domain`  | Voit selvittää verkkotunnuksesi sisään- ja ulostuloavaimesi osoitteessa:<br/><https://www.entsoe.eu/data/energy-identification-codes-eic/eic-area-codes-map/>                                                                                                                                                                                                                                                                |
| `out_domain` | kuten in_domain                                                                                                                                                                                                                                                                                                                                                                                                              |
| `primary`    | Jos tämä markkina on käytössä, tämä kohta asettaa sen ensisijaiseksi markkinaksi                                                                                                                                                                                                                                                                                                                                             |
| `enabled`    | aseta markkinasi käyttöön/pois käytöstä                                                                                                                                                                                                                                                                                                                                                                                      |

### Tibber

| Asetus       | Merkitys                                                                                                                                                                                                                                                                                                                           |
| :----------- | :--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `api_token`  | Näin saat tibber_api_keyn:<br/>1. kirjaudu sisään ilmaisella tai asiakkaan Tibber-tilillä osoitteessa<https://developer.tibber.com/settings/access-token><br/>2. Luo tunnus valitsemalla tarvitsemasi laajuudet (valitse "hinta")<br/>3. Luo ilmainen tili älypuhelimellasi tästä linkistä:<https://tibber.com/de/invite/ojgfbx2e> |
| `price_unit` | Asetettu:<br/>"energiaa" spotmarket-hintojen käyttämiseen (oletus),<br/>"yhteensä" käyttää kokonaishintoja, mukaan lukien verot ja maksut,<br/>"vero" käyttää vain veroja ja maksuja                                                                                                                                               |
| `primary`    | Jos tämä markkina on käytössä, tämä kohta asettaa sen ensisijaiseksi markkinaksi                                                                                                                                                                                                                                                   |
| `enabled`    | aseta markkinasi käyttöön/pois käytöstä                                                                                                                                                                                                                                                                                            |

* * *

# Lokitasot

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
