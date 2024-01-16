[tšehhi](README.cs.md)-[taani keel](README.da.md)-[saksa keel](README.de.md)-[Inglise](README.md)-[hispaania keel](README.es.md)-[Estonian](README.et.md)-[soome keel](README.fi.md)-[prantsuse keel](README.fr.md)-[kreeka keel](README.el.md)-[itaalia keel](README.it.md)-[hollandi keel](README.nl.md)-[norra keel](README.no.md)-[poola keel](README.pl.md)-[portugali keel](README.pt.md)-[rootsi keel](README.sv.md)-[Jaapani](README.ja.md)

![Logo](views/static/images/logo-seuss.png?raw=true "SEUSS")

# SEUSS

#### [SEUSS -> Smart Ess Unit Spotmarket Switcher]

# Seaded

## Kindral

| Seadistamine    | Tähendus                                                                                                                                     |
| --------------- | -------------------------------------------------------------------------------------------------------------------------------------------- |
| `time_zone`     | Teie geograafilisest asukohast lähtuvate toimingute õige ajastamise jaoks hädavajalik.<br/>Vorming nagu Euroopa/Viin, Euroopa/Amsterdam, ... |
| `log_file_path` | Määrab alternatiivse tee, kuhu logifailid salvestatakse.                                                                                     |
| `log_level`     | Kasutatud logitasemed on: INFO, WARNING, ERROR ja DEBUG. vaata[Logi tasemed](#loglevels)                                                     |

## Hinnad

| Seadistamine                               | Tähendus                                                                                                                                                                                                                               |
| ------------------------------------------ | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `use_second_day`                           | lubada/keelata tänaste ja homsete hindade võrdlemine, kui need on saadaval<br/>Märkus: Kui aktiveerite selle ja hinnad langevad mitme päeva jooksul, on võimalik, et mitu päeva ei võeta tasu ega lülituta kuni madalaimate hindadeni. |
| `number_of_lowest_prices_for_charging`     | odavaimate hindade arv, millega laadimine peaks/võib toimuda                                                                                                                                                                           |
| `number_of_highest_prices_for_discharging` | kõige kallimate hindade arv, millega tühjendamine peaks/võib toimuda                                                                                                                                                                   |
| `charging_price_limit`                     | laadimine on alati lubatud alla selle hinna<br/>kõige kallimate hindade arv, millega tühjendamine peaks/võib toimuda                                                                                                                   |

## ESS üksused

### Victron

| Seadistamine | Tähendus                                                                                                                                                                                 |
| :----------- | :--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `use_vrm`    | Kui see punkt on lubatud (tõene), üritatakse VRM-i portaali kaudu Victroniga ühendust luua.<br/>Selleks on vaja VRM-i portaalis kasutajat/parooli                                        |
| `ip_address` | Victroni kohalik IP-aadress.<br/>See on vajalik, kui "use_vrm" on keelatud (false).<br/>Vastasel juhul jääb see väli tühjaks                                                             |
| `unit_id`    | VRM-i portaali ID<br/>leiate jaotisest Seaded / VRM-i võrguportaal / VRM-i portaali ID.<br/>Märkus. See ID on vajalik Victroni juurdepääsuks isegi siis, kui te ei kasuta VRM-i portaali |
| `user`       | meiliaadress, mida kasutate VRM-i portaaliga ühenduse loomiseks                                                                                                                          |
| `password`   | parool, mida kasutate VRM-i portaaliga ühenduse loomiseks                                                                                                                                |

## Turud

### vastama

| Seadistamine | Tähendus                                                        |
| :----------- | :-------------------------------------------------------------- |
| `country`    | Valige asukoht AT või DE                                        |
| `primary`    | Kui see turg on lubatud, määrab see punkt selle esmaseks turuks |
| `enabled`    | määrake oma turg lubatuks/keelatuks                             |

### Enzo on

| Seadistamine | Tähendus                                                                                                                                                                                                                                                                                                                                                                                                              |
| :----------- | :-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `api_token`  | Kuidas hankida tasuta API turvamärk:<br/>1. Mine lehele<https://transparency.entsoe.eu/>--> registreeru ja loo konto<br/>2. Saada meil aadressile[transparency@entsoe.eu](mailto:transparency@entsoe.eu)teemareal on "Rahulik API juurdepääs".<br/>3. ENTSO-E kasutajatugi vastab teie päringule 3 tööpäeva jooksul.<br/>4. Genereeri turvamärk aadressil<https://transparency.entsoe.eu/usrm/user/myAccountSettings> |
| `in_domain`  | Sisse- ja väljamineku domeenivõtme leidmiseks minge aadressile:<br/><https://www.entsoe.eu/data/energy-identification-codes-eic/eic-area-codes-map/>                                                                                                                                                                                                                                                                  |
| `out_domain` | nagu in_domain                                                                                                                                                                                                                                                                                                                                                                                                        |
| `primary`    | Kui see turg on lubatud, määrab see punkt selle esmaseks turuks                                                                                                                                                                                                                                                                                                                                                       |
| `enabled`    | määrake oma turg lubatuks/keelatuks                                                                                                                                                                                                                                                                                                                                                                                   |

### Tibber

| Seadistamine | Tähendus                                                                                                                                                                                                                                                                                                                                     |
| :----------- | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `api_token`  | Tibber_api_key hankimiseks tehke järgmist.<br/>1. logige sisse tasuta või kliendi Tibberi kontoga aadressil<https://developer.tibber.com/settings/access-token><br/>2. Looge tunnus, valides vajalikud ulatused (valige "hind")<br/>3. Kasutage seda linki oma nutitelefoniga tasuta konto loomiseks:<https://tibber.com/de/invite/ojgfbx2e> |
| `price_unit` | Seatud:<br/>"energia", et kasutada hetketuru hindu (vaikimisi),<br/>"kokku", et kasutada koguhindu koos maksude ja lõivudega,<br/>"maks", et kasutada ainult makse ja tasusid                                                                                                                                                                |
| `primary`    | Kui see turg on lubatud, määrab see punkt selle esmaseks turuks                                                                                                                                                                                                                                                                              |
| `enabled`    | määrake oma turg lubatuks/keelatuks                                                                                                                                                                                                                                                                                                          |

* * *

# Logitasemed

### VIGA

ERROR logi tase näitab rakenduses esinevaid tõrketingimusi, mis takistavad konkreetse toimingu täitmist. Kuigi rakendus võib jätkata töötamist vähendatud funktsionaalsuse või jõudluse tasemel,<br/>ERROR logid tähistavad probleeme, mida tuleks kiiresti uurida.

### HOIATUS

WARN-tasemel logitud sündmused näitavad tavaliselt, et on midagi ootamatut
juhtus, kuid rakendus võib esialgu normaalselt edasi töötada.
Seda kasutatakse ka tingimuste tähistamiseks, millega tuleks enne nende tegemist viivitamatult tegeleda
areneda rakendusega seotud probleemideks.

### INFO

INFO tase fikseerib süsteemis olevad sündmused, mis on olulised
rakenduse äriline eesmärk. Sellised sündmused logitakse, et näidata, et süsteem on
töötab normaalselt. Tootmissüsteemid logivad tavaliselt sellel tasemel vaikimisi
nii et rakenduse tavapärase käitumise kokkuvõte oleks kõigile nähtav
 logide ülevaatamine.

### SILU

SILUMISE taset kasutatakse sõnumite logimiseks, mis aitavad arendajatel tuvastada
probleemid silumisseansi ajal. SILUMISEL logitud sõnumite sisu
tase varieerub olenevalt teie rakendusest, kuid tavaliselt sisaldavad need
üksikasjalik teave, mis aitab selle arendajatel probleeme tõrkeotsingul teha
tõhusalt. See võib hõlmata muutujate olekut ümbritsevas ulatuses või
asjakohased veakoodid. |
