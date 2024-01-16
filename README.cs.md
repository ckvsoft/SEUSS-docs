[Čeština](README.cs.md)-[dánština](README.da.md)-[Němec](README.de.md)-[Angličtina](README.md)-[španělština](README.es.md)-[estonština](README.et.md)-[finština](README.fi.md)-[francouzština](README.fr.md)-[řecký](README.el.md)-[italština](README.it.md)-[holandský](README.nl.md)-[norský](README.no.md)-[polština](README.pl.md)-[portugalština](README.pt.md)-[švédský](README.sv.md)-[japonský](README.ja.md)

![Logo](views/static/images/logo-seuss.png?raw=true "SEUSS")

# SEUSS

#### [SEUSS -> Smart Ess Unit Spotmarket Switcher]

# Konfigurace

## Všeobecné

| Nastavení       | Význam                                                                                                                          |
| --------------- | ------------------------------------------------------------------------------------------------------------------------------- |
| `time_zone`     | Nezbytné pro správné načasování operací na základě vaší geografické polohy.<br/>Formát jako Evropa/Vídeň, Evropa/Amsterdam, ... |
| `log_file_path` | Nastaví alternativní cestu, do které se ukládají soubory protokolu.                                                             |
| `log_level`     | Použité Loglevel jsou: INFO, WARNING, ERROR a DEBUG. vidět[Log úrovně](#loglevels)                                              |

## Ceny

| Nastavení                                  | Význam                                                                                                                                                                                                                                                     |
| ------------------------------------------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `use_second_day`                           | povolit/zakázat porovnání dnešních a zítřejších cen, pokud budou dostupné<br/>Poznámka: Pokud toto aktivujete a ceny během několika dní klesají, je možné, že několik dní nedojde k žádnému nabíjení nebo přepínání, dokud nebudou dosaženy nejnižší ceny. |
| `number_of_lowest_prices_for_charging`     | počet nejlevnějších cen, za které by nakládka měla/může být provedena                                                                                                                                                                                      |
| `number_of_highest_prices_for_discharging` | počet nejdražších cen, za které by mělo/může být vybíjení provedeno                                                                                                                                                                                        |
| `charging_price_limit`                     | nabíjení je vždy povoleno pod touto cenou<br/>počet nejdražších cen, za které by mělo/může být vybíjení provedeno                                                                                                                                          |

## Jednotky ESS

### Victron

| Nastavení    | Význam                                                                                                                                                                   |
| :----------- | :----------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `use_vrm`    | Pokud je tento bod povolen (pravda), dojde k pokusu o připojení k Victronu přes portál VRM.<br/>To vyžaduje uživatele/heslo na portálu VRM                               |
| `ip_address` | Místní IP adresa zařízení Victron.<br/>Toto je vyžadováno, pokud je "use_vrm" zakázáno (false).<br/>Jinak toto pole zůstane prázdné                                      |
| `unit_id`    | ID portálu VRM<br/>naleznete v Nastavení / VRM online portál / ID portálu VRM.<br/>Poznámka: Toto ID je vyžadováno pro přístup k Victronu, i když nepoužíváte portál VRM |
| `user`       | e-mailovou adresu, kterou používáte k připojení k portálu VRM                                                                                                            |
| `password`   | heslo, které používáte pro připojení k portálu VRM                                                                                                                       |

## trhy

### Odpovědět

| Nastavení | Význam                                                              |
| :-------- | :------------------------------------------------------------------ |
| `country` | Vyberte umístění AT nebo DE                                         |
| `primary` | Pokud je tento trh povolen, tento bod jej nastaví jako primární trh |
| `enabled` | nastavte svůj trh jako povolený/deaktivovaný                        |

### Enzo je

| Nastavení    | Význam                                                                                                                                                                                                                                                                                                                                                                                                                                |
| :----------- | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `api_token`  | Jak získat bezplatný bezpečnostní token API:<br/>1. Přejít na<https://transparency.entsoe.eu/>--> zaregistrujte se a vytvořte si účet<br/>2. Pošlete e-mail na adresu[transparency@entsoe.eu](mailto:transparency@entsoe.eu)s „Restful API access“ v předmětu<br/>3. Helpdesk ENTSO-E odpoví na vaši žádost do 3 pracovních dnů.<br/>4. Vygenerujte bezpečnostní token na<https://transparency.entsoe.eu/usrm/user/myAccountSettings> |
| `in_domain`  | Chcete-li zjistit svůj vstupní a výstupní klíč domény, přejděte na:<br/><https://www.entsoe.eu/data/energy-identification-codes-eic/eic-area-codes-map/>                                                                                                                                                                                                                                                                              |
| `out_domain` | jako v_doméně                                                                                                                                                                                                                                                                                                                                                                                                                         |
| `primary`    | Pokud je tento trh povolen, tento bod jej nastaví jako primární trh                                                                                                                                                                                                                                                                                                                                                                   |
| `enabled`    | nastavte svůj trh jako povolený/deaktivovaný                                                                                                                                                                                                                                                                                                                                                                                          |

### Tibber

| Nastavení    | Význam                                                                                                                                                                                                                                                                                                                                                     |
| :----------- | :--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `api_token`  | Chcete-li získat tibber_api_key:<br/>1. přihlaste se pomocí bezplatného nebo zákaznického účtu Tibber na adrese<https://developer.tibber.com/settings/access-token><br/>2. Vytvořte token výběrem požadovaných rozsahů (vyberte "cena")<br/>3. Použijte tento odkaz k vytvoření bezplatného účtu pomocí smartphonu:<https://tibber.com/de/invite/ojgfbx2e> |
| `price_unit` | Nastaven na:<br/>„energie“ pro použití cen na spotovém trhu (výchozí),<br/>„celkem“ pro použití celkových cen včetně daní a poplatků,<br/>"daň" používat pouze daně a poplatky                                                                                                                                                                             |
| `primary`    | Pokud je tento trh povolen, tento bod jej nastaví jako primární trh                                                                                                                                                                                                                                                                                        |
| `enabled`    | nastavte svůj trh jako povolený/deaktivovaný                                                                                                                                                                                                                                                                                                               |

* * *

# Loglevels

### CHYBA

Úroveň protokolu ERROR označuje chybové stavy v aplikaci, které brání provedení konkrétní operace. I když aplikace může nadále fungovat se sníženou úrovní funkčnosti nebo výkonu,<br/>Protokoly ERROR označují problémy, které by měly být neprodleně prošetřeny.

### VAROVAT

Události zaznamenané na úrovni WARN obvykle naznačují, že došlo k něčemu neočekávanému
došlo, ale aplikace může prozatím normálně fungovat.
Používá se také k označení podmínek, které by měly být okamžitě vyřešeny před jejich vznikem
eskalovat do problémů aplikace.

### INFO

Úroveň INFO zachycuje události v systému, které jsou pro systém důležité
obchodní účel aplikace. Takové události jsou protokolovány, aby bylo vidět, že systém ano
normálně fungující. Produkční systémy obvykle standardně používají protokolování na této úrovni
takže souhrn běžného chování aplikace je viditelný pro každého
 revize protokolů.

### LADIT

Úroveň DEBUG se používá pro protokolování zpráv, které pomáhají vývojářům při identifikaci
problémy během relace ladění. Obsah zpráv zaznamenaných na DEBUG
úroveň se bude lišit v závislosti na vaší aplikaci, ale obvykle obsahují
podrobné informace, které pomáhají jeho vývojářům při odstraňování problémů
efektivně. To může zahrnovat stav proměnných v okolním rozsahu nebo
příslušné chybové kódy. |
