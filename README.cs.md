![Logo](views/static/images/logo-seuss.png?raw=true "SEUSS")

# SEUSS

### [SEUSS -> Smart Ess Unit Spotmarket Switcher]

#### Nahlaste prosím chyby a navrhněte vylepšení. Děkujeme všem, kteří se již zúčastnili.

###### Pokud byste k tomu chtěli přispět rozšířeními, odešlete žádost o stažení ve větvi dev. Pro opravy chyb lze požadavek na stažení provést také na hlavní větvi

### Co tento software umí?

Toto je aplikace Python 3, která zapne vaši jednotku ESS (ovladač) ve správný čas, když jsou vaše hodinové dynamické ceny energie nízké. Nebo se používá k vybíjení, když jsou ceny extrémně vysoké.

#### Aktuálně podporované systémy jsou:

### Jednotky ESS

* * *

-   **_Systémy ukládání energie Victron Venus OS, jako je řada MultiPlus II_**

* * *

### Spotové trhy

* * *

-   **_Odpovědět_**
-   **_Enzo-E_**
-   **_Tibber_**

* * *

Ovládání jednotky EZS (regulátoru) se provádí přes mqtt. Výhodou tohoto ovládání je:
že tato aplikace nemusí běžet přímo na VenusOS. Přímé ovládání pomocí D-BUS se připravuje

# Testováno

Tato verze byla úspěšná

* * *

-   **_Linux Ubuntu >= 22.04_**
-   **_Venus OS Maliny >= vz.12_**

* * *

testováno

# Nainstalujte

Stáhněte si instalační skript z úložiště GitHub a spusťte ve svém terminálu následující příkaz:

    wget -O seuss_install.sh https://raw.githubusercontent.com/ckvsoft/SEUSS/dev/scripts/seuss_install.sh`

Spusťte instalační skript s dalšími možnostmi, abyste připravili vše v podadresáři pro vaši kontrolu. Například:

    bash seuss_install.sh`

The default directory is /data/seuss (Venus OS) But you can optionally specify a different directory by using the environment variable TARGET_DIRECTORY e.g.

    TARGET_DIRECTORY=/opt/seuss bash seuss_install.sh`

Na Cerbo GX je souborový systém připojen pouze pro čtení. Vidět<https://www.victronenergy.com/live/ccgx:root_access>.
Aby bylo možné do souborového systému zapisovat, musíte před spuštěním instalačního skriptu provést následující příkaz:

    /opt/victronenergy/swupdate-scripts/resize2fs.sh

# Konfigurace

Po`SEUSS`byla úspěšně nainstalována, na IP adrese a portu 5000 je dostupná webová stránka`Computer/VenusOS`na kterých`SEUSS`byl nainstalován.

-   Soubor protokolu si můžete prohlédnout nebo stáhnout.
-   Kromě toho lze konfiguraci provést pomocí[Editor konfigurace]položka menu.
-   Tool tips for most points are displayed here.

#### Prohlížeč protokolů

-   ![Logo](views/static/images/logviewer.png?raw=true "SEUSS Log Viewer")

#### Editor konfigurace – jednotky ESS

-   ![Logo](views/static/images/configeditor_ess.png?raw=true "SEUSS Config Editor")

#### Editor konfigurace - PV panely

-   ![Logo](views/static/images/configeditor_panels.png?raw=true "SEUSS Config Editor")

Ty lze také nalézt v popisu Nastavení.
Pro ty, kteří raději pracují v konfiguračním souboru, je tu config.json

# Nastavení

## Všeobecné

| Nastavení       | Význam                                                                                                                             |
| --------------- | ---------------------------------------------------------------------------------------------------------------------------------- |
| `time_zone`     | Nezbytné pro správné načasování operací na základě vaší geografické polohy.<br/>Formát jako`Europe/Vienna`,`Europe/Amsterdam`, ... |
| `log_file_path` | Nastaví alternativní cestu, do které se ukládají soubory protokolu.                                                                |
| `log_level`     | Použité Loglevel jsou:`INFO`,`WARNING`,`ERROR`a`DEBUG`. vidět[Log úrovně](#loglevels)                                              |

## Ceny

#### Změňte prosím ceny (vždy použijte Cent/kWh, bez ohledu na to, zda používáte Awattar (zobrazení Cent/kWh) nebo Entsoe API (zobrazení EUR/MWh) / čisté ceny bez daně).

| Nastavení                                  | Význam                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| ------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `use_second_day`                           | `enable/disable`porovnat dnešní a zítra ceny, pokud budou dostupné<br/>Poznámka: Pokud toto aktivujete a ceny během několika dní klesají, je možné, že několik dní nedojde k žádnému nabíjení nebo přepínání, dokud nebudou dosaženy nejnižší ceny.                                                                                                                                                                                                                                                           |
| `number_of_lowest_prices_for_charging`     | Zde lze použít dva režimy.<br/>režim 1:<br/>_počet nejlevnějších cen, za které by mělo/může probíhat zpoplatnění. Zde zadáváte celá čísla<br/>režim 2:<br/>_Zde se počet cen určuje na základě průměrné ceny. V tomto režimu zadáváte desetinná čísla. Např. 0,85, abyste obdrželi všechny ceny, které jsou 85 % pod průměrem. Relevantní je zde specifikace hodnoty čárkou. S 1.0 se předpokládá, že se bere 100 % průměrné ceny (nedává to žádný smysl), ale pokud je zadáno 1, je to 1 nejlevnější cena    |
| `number_of_highest_prices_for_discharging` | Zde lze použít dva režimy.<br/>režim 1:<br/>_počet nejdražších cen, za které by vybíjení mělo/může probíhat. Zde zadáváte celá čísla<br/>režim 2:<br/>_Zde se počet cen určuje na základě průměrné ceny. V tomto režimu zadáváte desetinná čísla. Např. 1,25, abyste obdrželi všechny ceny, které jsou o 25 % nad průměrem.<br/>Co je zde důležité, je specifikace hodnoty čárky. S 1.0 se předpokládá, že se bere 100 % průměrné ceny (nedává to žádný smysl), ale pokud je zadáno 1, je to 1 nejdražší cena |
| `charging_price_limit`                     | nabíjení je vždy povoleno pod touto cenou<br/>počet nejdražších cen, za které by mělo/může být vybíjení provedeno                                                                                                                                                                                                                                                                                                                                                                                             |

## Jednotky ESS

### Victron

| Nastavení             | Význam                                                                                                                                                                                                                                                                                                                                                                                                      |
| :-------------------- | :---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `use_vrm`             | Pokud je tento bod povolen (pravda), dojde k pokusu o připojení k Victronu přes portál VRM.<br/>To vyžaduje uživatele/heslo na portálu VRM                                                                                                                                                                                                                                                                  |
| `ip_address`          | Místní IP adresa zařízení Victron.<br/>To je vyžadováno, pokud`use_vrm`je zakázáno (false).<br/>Jinak toto pole zůstane prázdné                                                                                                                                                                                                                                                                             |
| `unit_id`             | ID portálu VRM<br/>lze nalézt v`Settings / VRM online portal / VRM Portal Id`.<br/>Poznámka: Toto ID je vyžadováno pro přístup k Victronu, i když nepoužíváte portál VRM                                                                                                                                                                                                                                    |
| `user`                | e-mailovou adresu, kterou používáte k připojení k portálu VRM                                                                                                                                                                                                                                                                                                                                               |
| `password`            | heslo, které používáte pro připojení k portálu VRM                                                                                                                                                                                                                                                                                                                                                          |
| `max_discharge_power` | Výchozí: -1<br/>Pokud použijete`Limit inverter power`v menu ESS pak musí být tato hodnota zadána zde.<br/>Pokud je střídač nastaven na`Discharge false`touto aplikací bude tato hodnota přepsána v ESS.<br/>Tento limit je zde nastaven v režimu vybíjení v EZS.<br/>Pokud není nastaven žádný limit, ponechte hodnotu na`-1`.<br/>Příklad: Enter`1000`omezit vypouštění na`1000W`, Enter`-1`pro plný výkon |
| `only_observation`    | Li`only observation`je aktivován, bude essunit použit pouze pro statistické účely. essunit nesplňuje žádné podmínky                                                                                                                                                                                                                                                                                         |
| `enabled`             | Chcete-li použít tento záznam, musí být`enabled`. v opačném případě`disabled`                                                                                                                                                                                                                                                                                                                               |

## Spotové trhy

### Odpovědět

| Nastavení | Význam                                                                        |
| :-------- | :---------------------------------------------------------------------------- |
| `country` | Vyberte umístění AT nebo DE                                                   |
| `primary` | Pokud je tento trh povolen, tento bod jej nastaví jako primární trh           |
| `enabled` | Chcete-li použít tento záznam, musí být`enabled`. v opačném případě`disabled` |

### Enzo je

| Nastavení    | Význam                                                                                                                                                                                                                                                                                                                                                                                                                                |
| :----------- | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `api_token`  | Jak získat bezplatný bezpečnostní token API:<br/>1. Přejít na<https://transparency.entsoe.eu/>--> zaregistrujte se a vytvořte si účet<br/>2. Pošlete e-mail na adresu[transparency@entsoe.eu](mailto:transparency@entsoe.eu)s „Restful API access“ v předmětu<br/>3. Helpdesk ENTSO-E odpoví na vaši žádost do 3 pracovních dnů.<br/>4. Vygenerujte bezpečnostní token na<https://transparency.entsoe.eu/usrm/user/myAccountSettings> |
| `in_domain`  | Chcete-li zjistit svůj vstupní a výstupní klíč domény, přejděte na:<br/><https://www.entsoe.eu/data/energy-identification-codes-eic/eic-area-codes-map/>                                                                                                                                                                                                                                                                              |
| `out_domain` | jako`in_domain`                                                                                                                                                                                                                                                                                                                                                                                                                       |
| `primary`    | Pokud je tento trh povolen, tento bod jej nastaví jako primární trh                                                                                                                                                                                                                                                                                                                                                                   |
| `enabled`    | Chcete-li použít tento záznam, musí být`enabled`. v opačném případě`disabled`                                                                                                                                                                                                                                                                                                                                                         |

### Tibber

| Nastavení    | Význam                                                                                                                                                                                                                                                                                                                                                         |
| :----------- | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `api_token`  | Chcete-li získat tibber_api_key:<br/>1. přihlaste se pomocí bezplatného nebo zákaznického účtu Tibber na adrese<https://developer.tibber.com/settings/access-token><br/>2. Create a token by selecting the scopes you need (select "price")<br/>3. Použijte tento odkaz k vytvoření bezplatného účtu pomocí smartphonu:<https://tibber.com/de/invite/ojgfbx2e> |
| `price_unit` | Nastaven na:<br/>„energie“ pro použití cen na spotovém trhu (výchozí),<br/>„celkem“ pro použití celkových cen včetně daní a poplatků,<br/>"daň" používat pouze daně a poplatky                                                                                                                                                                                 |
| `primary`    | Pokud je tento trh povolen, tento bod jej nastaví jako primární trh                                                                                                                                                                                                                                                                                            |
| `enabled`    | Chcete-li použít tento záznam, musí být`enabled`. v opačném případě`disabled`                                                                                                                                                                                                                                                                                  |

## FV panely

| Nastavení         | Význam                                                                                   |
| :---------------- | :--------------------------------------------------------------------------------------- |
| `locLat`          | Zeměpisná šířka                                                                          |
| `locLong`         | Zeměpisná délka                                                                          |
| `angle`           | Úhel vašich panelů 0 (horizontální) … 90 (vertikální)                                    |
| `direction`       | Azimut roviny, -180 … 180 (-180 = sever, -90 = východ, 0 = jih, 90 = západ, 180 = sever) |
| `totPower`        | výkon instalovaných modulů v kilowattech                                                 |
| `total_area`      | Celková plocha panelů v metrech čtverečních                                              |
| `damping_morning` | Pomocí tohoto parametru můžete ráno upravit výsledek. Hodnota float 0..1, výchozí 0      |
| `damping_evening` | Pomocí tohoto parametru můžete večer upravit výsledek. Hodnota float 0..1, výchozí 0     |
| `enabled`         | Chcete-li použít tento záznam, musí být`enabled`. v opačném případě`disabled`            |

* * *

## Loglevels

### `ERROR`

The`ERROR`úroveň protokolu označuje chybové stavy v aplikaci, které brání provedení konkrétní operace. I když aplikace může nadále fungovat se sníženou úrovní funkčnosti nebo výkonu,<br/>`ERROR`protokoly označují problémy, které by měly být neprodleně prošetřeny.

### `WARN`

Události zaznamenané na`WARN`úroveň obvykle naznačuje, že došlo k něčemu neočekávanému
došlo, ale aplikace může prozatím normálně fungovat.
Používá se také k označení podmínek, které by měly být okamžitě vyřešeny před jejich vznikem
eskalovat do problémů aplikace.

### `INFO`

The`INFO`úroveň zachycuje události v systému, které jsou pro ni významné
obchodní účel aplikace. Takové události jsou protokolovány, aby bylo vidět, že systém ano
normálně fungující. Produkční systémy obvykle standardně používají protokolování na této úrovni
takže souhrn běžného chování aplikace je viditelný pro každého
 revize protokolů.

### `DEBUG`

The`DEBUG`úroveň se používá pro protokolování zpráv, které pomáhají vývojářům při identifikaci
problémy během relace ladění. Obsah zpráv zaznamenaných na DEBUG
úroveň se bude lišit v závislosti na vaší aplikaci, ale obvykle obsahují
podrobné informace, které pomáhají jeho vývojářům při odstraňování problémů
efektivně. To může zahrnovat stav proměnných v okolním rozsahu nebo
příslušné chybové kódy. |

## Inspirace

Myšlenka je inspirována projektem @christian1980nrw, na který odkazujeme níže. Tento projekt je můj první s OS Victron Venus, takže jsem převzal některé nápady a přístupy z následujících projektů. Přístup je stejný a pro velmi úzké systémy je pravděpodobně lepší implementace s bash skriptem

##### - moc děkuji za předání znalostí:

-   [Přepínač spotového trhu](https://github.com/christian1980nrw/Spotmarket-Switcher)
-   [dynamic-ess](https://github.com/tfranssen/dynamic-ess)
