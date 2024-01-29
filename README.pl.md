![Logo](views/static/images/logo-seuss.png?raw=true "SEUSS")

# SEUSS

### [SEUSS -> Inteligentny przełącznik Spotmarket jednostki Ess]

#### Prosimy o zgłaszanie błędów i proponowanie ulepszeń. Dziękujemy wszystkim, którzy już wzięli udział.

###### Jeśli chcesz wnieść do tego rozszerzenia, prześlij żądanie ściągnięcia w gałęzi deweloperów. Aby naprawić błędy, żądanie ściągnięcia można również wykonać w głównej gałęzi

### Co robi to oprogramowanie?

Jest to aplikacja w języku Python 3, która włącza jednostkę ESS (sterownik) we właściwym czasie, gdy godzinowe dynamiczne ceny energii są niskie. Lub używany do rozładunku, gdy ceny są wyjątkowo wysokie.

#### Obecnie obsługiwane systemy to:

### Jednostki ESS

* * *

-   **_Systemy magazynowania energii Victron Venus OS, takie jak seria MultiPlus II_**

* * *

### Rynki spotowe

* * *

-   **_odpowiedź_**
-   **_Enzo-E_**
-   **_Tibbera_**

* * *

Sterowanie jednostką ESS (kontrolerem) odbywa się poprzez mqtt. Zaletą tej kontroli jest:
że ta aplikacja nie musi działać bezpośrednio na VenusOS. Trwają prace nad bezpośrednim sterowaniem za pomocą D-BUS

# Przetestowany

Ta wersja odniosła sukces

* * *

-   **_Linux Ubuntu >= 22.04_**
-   **_Maliny Venus OS >= vz.12_**

* * *

przetestowany

# zainstalować

Pobierz skrypt instalacyjny z repozytorium GitHub, wykonaj w terminalu następujące polecenie:

    wget -O seuss_install.sh https://raw.githubusercontent.com/ckvsoft/SEUSS/dev/scripts/seuss_install.sh`

Uruchom skrypt instalacyjny z dodatkowymi opcjami, aby przygotować wszystko w podkatalogu do kontroli. Na przykład:

    bash seuss_install.sh`

Domyślnym katalogiem jest /data/seuss (Venus OS). Opcjonalnie możesz określić inny katalog, używając zmiennej środowiskowej TARGET_DIRECTORY, np.

    TARGET_DIRECTORY=/opt/seuss bash seuss_install.sh`

Na Cerbo GX system plików jest montowany tylko do odczytu. Widzieć<https://www.victronenergy.com/live/ccgx:root_access>.
Aby umożliwić zapis w systemie plików, przed uruchomieniem skryptu instalacyjnego należy wykonać następującą komendę:

    /opt/victronenergy/swupdate-scripts/resize2fs.sh

# Konfiguracja

Po`SEUSS`został pomyślnie zainstalowany, strona internetowa jest dostępna pod adresem IP i portem 5000`Computer/VenusOS`na którym`SEUSS`został zainstalowany.

-   Możesz wyświetlić lub pobrać plik dziennika.
-   Ponadto konfigurację można przeprowadzić za pomocą[Edytor konfiguracji]pozycja w menu.
-   Tutaj wyświetlane są podpowiedzi dotyczące większości punktów.

#### Przeglądarka dziennika

-   ![Logo](views/static/images/logviewer.png?raw=true "SEUSS Log Viewer")

#### Edytor konfiguracji — jednostki ESS

-   ![Logo](views/static/images/configeditor_ess.png?raw=true "SEUSS Config Editor")

#### Edytor konfiguracji - Panele fotowoltaiczne

-   ![Logo](views/static/images/configeditor_panels.png?raw=true "SEUSS Config Editor")

Można je również znaleźć w opisie ustawień.
Dla tych, którzy wolą pracować w pliku konfiguracyjnym, dostępny jest plik config.toml

# Ustawienia

## Ogólny

| Ustawienie      | Oznaczający                                                                                                                                          |
| --------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------- |
| `time_zone`     | Niezbędne do prawidłowego harmonogramu operacji w oparciu o Twoją lokalizację geograficzną.<br/>Sformatuj jak`Europe/Vienna`,`Europe/Amsterdam`, ... |
| `log_file_path` | Ustawia alternatywną ścieżkę, w której zapisywane są pliki dziennika.                                                                                |
| `log_level`     | Używane Loglevel to:`INFO`,`WARNING`,`ERROR`I`DEBUG`. Widzieć[Poziomy dziennika](#loglevels)                                                         |

## Ceny

#### Zmień ceny (zawsze używaj Cent/kWh, niezależnie od tego, czy używasz Awattar (wyświetlający Cent/kWh) czy Entsoe API (wyświetlający EUR/MWh) / ceny netto bez podatku).

| Ustawienie                                 | Oznaczający                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| ------------------------------------------ | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `use_second_day`                           | `enable/disable`porównać dzisiejsze i przyszłe ceny, jeśli będą dostępne<br/>Uwaga: jeśli aktywujesz tę opcję, a ceny będą spadać przez kilka dni, możliwe, że przez kilka dni nie będzie ładowania ani przełączania, aż do osiągnięcia najniższych cen.                                                                                                                                                                                                                                                                                                       |
| `number_of_lowest_prices_for_charging`     | Można tu zastosować dwa tryby.<br/>tryb 1:<br/>_liczba najniższych cen, po których powinno/może odbywać się pobieranie opłat. Tutaj wprowadzasz liczby całkowite<br/>tryb 2:<br/>_Tutaj liczbę cen określa się na podstawie średniej ceny. W tym trybie wprowadza się liczby dziesiętne. Np. 0,85, aby otrzymać wszystkie ceny o 85% niższe od średniej. Istotne jest tutaj podanie wartości przecinka. Przy wartości 1.0 zakłada się, że pobierane jest 100% średniej ceny (nie ma to sensu), natomiast wpisanie 1 oznacza 1 najtańszą cenę                   |
| `number_of_highest_prices_for_discharging` | Można tu zastosować dwa tryby.<br/>tryb 1:<br/>_liczba najdroższych cen, po których powinien/może odbywać się rozładunek. Tutaj wprowadzasz liczby całkowite<br/>tryb 2:<br/>_Tutaj liczbę cen określa się na podstawie średniej ceny. W tym trybie wprowadza się liczby dziesiętne. Np. 1,25, aby otrzymać wszystkie ceny o 25% wyższe od średniej.<br/>Istotne jest tutaj określenie wartości przecinka. Przy wartości 1.0 zakłada się, że pobierane jest 100% średniej ceny (nie ma to sensu), natomiast wpisanie 1 oznacza, że ​​jest to 1 najdroższa cena |
| `charging_price_limit`                     | poniżej tej ceny ładowanie jest zawsze włączone<br/>liczba najdroższych cen, po jakich należy/można dokonywać rozładunku                                                                                                                                                                                                                                                                                                                                                                                                                                       |

## Jednostki ESS

### Victron

| Ustawienie            | Oznaczający                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| :-------------------- | :--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `use_vrm`             | Jeśli ten punkt jest włączony (true), podejmowana jest próba połączenia z Victronem za pośrednictwem portalu VRM.<br/>Wymaga to użytkownika/hasła w portalu VRM                                                                                                                                                                                                                                                                                            |
| `ip_address`          | Lokalny adres IP Victron.<br/>Jest to wymagane, jeśli`use_vrm`jest wyłączony (false).<br/>W przeciwnym razie to pole pozostaje puste                                                                                                                                                                                                                                                                                                                       |
| `unit_id`             | Identyfikator portalu VRM<br/>można znaleźć w`Settings / VRM online portal / VRM Portal Id`.<br/>Uwaga: ten identyfikator jest wymagany, aby uzyskać dostęp do Victron, nawet jeśli nie korzystasz z portalu VRM                                                                                                                                                                                                                                           |
| `user`                | adres e-mail, którego używasz do łączenia się z portalem VRM                                                                                                                                                                                                                                                                                                                                                                                               |
| `password`            | hasło, którego używasz do łączenia się z portalem VRM                                                                                                                                                                                                                                                                                                                                                                                                      |
| `max_discharge_power` | Wartość domyślna: -1<br/>Jeśli użyjesz`Limit inverter power`w menu ESS, należy tutaj wprowadzić tę wartość.<br/>Jeśli falownik jest ustawiony na`Discharge false`przez tę aplikację, wartość ta zostanie nadpisana w ESS.<br/>Limit ten jest tutaj ustawiony w trybie rozładowania w ESS.<br/>Jeśli nie ustawiono żadnego limitu, pozostaw wartość na poziomie`-1`.<br/>Przykład: Enter`1000`ograniczyć wyładowanie do`1000W`, Wchodzić`-1`dla pełnej Mocy |
| `primary`             | Jeśli ten rynek jest włączony, ten punkt ustawia go jako rynek pierwotny                                                                                                                                                                                                                                                                                                                                                                                   |
| `enabled`             | Aby skorzystać z tego wpisu, musi tak być`enabled`. W przeciwnym razie`disabled`                                                                                                                                                                                                                                                                                                                                                                           |

## Rynki spotowe

### odpowiedź

| Ustawienie | Oznaczający                                                                      |
| :--------- | :------------------------------------------------------------------------------- |
| `country`  | Wybierz lokalizację AT lub DE                                                    |
| `primary`  | Jeśli ten rynek jest włączony, ten punkt ustawia go jako rynek pierwotny         |
| `enabled`  | Aby skorzystać z tego wpisu, musi tak być`enabled`. W przeciwnym razie`disabled` |

### Enzo jest

| Ustawienie   | Oznaczający                                                                                                                                                                                                                                                                                                                                                                                                                                |
| :----------- | :----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `api_token`  | Jak zdobyć darmowy token bezpieczeństwa API:<br/>1. Przejdź do<https://transparency.entsoe.eu/>--> zarejestruj się i utwórz konto<br/>2. Wyślij e-mail do[transparency@entsoe.eu](mailto:transparency@entsoe.eu)z tematem „Restful API Access”.<br/>3. Helpdesk ENTSO-E odpowie na Twoją prośbę w terminie 3 dni roboczych.<br/>4. Wygeneruj token zabezpieczający pod adresem<https://transparency.entsoe.eu/usrm/user/myAccountSettings> |
| `in_domain`  | Aby znaleźć klucz domeny wejściowej i wyjściowej, przejdź do:<br/><https://www.entsoe.eu/data/energy-identification-codes-eic/eic-area-codes-map/>                                                                                                                                                                                                                                                                                         |
| `out_domain` | tak jak`in_domain`                                                                                                                                                                                                                                                                                                                                                                                                                         |
| `primary`    | Jeśli ten rynek jest włączony, ten punkt ustawia go jako rynek pierwotny                                                                                                                                                                                                                                                                                                                                                                   |
| `enabled`    | Aby skorzystać z tego wpisu, musi tak być`enabled`. W przeciwnym razie`disabled`                                                                                                                                                                                                                                                                                                                                                           |

### Tibbera

| Ustawienie   | Oznaczający                                                                                                                                                                                                                                                                                                                                      |
| :----------- | :----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `api_token`  | Aby uzyskać tibber_api_key:<br/>1. zaloguj się za pomocą bezpłatnego lub klienta konta Tibber pod adresem<https://developer.tibber.com/settings/access-token><br/>2. Utwórz token wybierając potrzebne zakresy (wybierz „cena”)<br/>3. Użyj tego linku, aby utworzyć bezpłatne konto na swoim smartfonie:<https://tibber.com/de/invite/ojgfbx2e> |
| `price_unit` | Ustawić:<br/>"energia" aby skorzystać z cen rynkowych spot (domyślnie),<br/>„total”, aby zastosować ceny całkowite zawierające podatki i opłaty,<br/>„podatek”, aby używać wyłącznie podatków i opłat                                                                                                                                            |
| `primary`    | Jeśli ten rynek jest włączony, ten punkt ustawia go jako rynek pierwotny                                                                                                                                                                                                                                                                         |
| `enabled`    | Aby skorzystać z tego wpisu, musi tak być`enabled`. W przeciwnym razie`disabled`                                                                                                                                                                                                                                                                 |

## Panele fotowoltaiczne

| Ustawienie  | Oznaczający                                                                                           |
| :---------- | :---------------------------------------------------------------------------------------------------- |
| `LocLat`    | Szerokość                                                                                             |
| `LocLon`    | Długość geograficzna                                                                                  |
| `angle`     | Kąt paneli 0 (w poziomie) … 90 (w pionie)                                                             |
| `direction` | Azymut płaszczyzny, -180 … 180 (-180 = północ, -90 = wschód, 0 = południe, 90 = zachód, 180 = północ) |
| `totPower`  | Moc zainstalowanych modułów w kilowatach                                                              |
| `enabled`   | Aby skorzystać z tego wpisu, musi tak być`enabled`. W przeciwnym razie`disabled`                      |

* * *

## Poziomy logowania

### `ERROR`

The`ERROR`poziom dziennika wskazuje warunki błędów w aplikacji, które utrudniają wykonanie określonej operacji. Chociaż aplikacja może nadal działać z obniżonym poziomem funkcjonalności lub wydajności,<br/>`ERROR`dzienniki oznaczają problemy, które należy niezwłocznie zbadać.

### `WARN`

Zdarzenia rejestrowane w`WARN`poziom zazwyczaj wskazuje, że wydarzyło się coś nieoczekiwanego
wystąpił, ale aplikacja może na razie normalnie działać.
Używa się go również do określenia warunków, którymi należy się niezwłocznie zająć przed ich wystąpieniem
przerodzić się w problemy z aplikacją.

### `INFO`

The`INFO`Poziom rejestruje zdarzenia w systemie, które są istotne dla
cel biznesowy aplikacji. Takie zdarzenia są rejestrowane, aby wykazać, że system tak jest
działa normalnie. Systemy produkcyjne zazwyczaj domyślnie rejestrują na tym poziomie
tak, aby podsumowanie normalnego zachowania aplikacji było widoczne dla każdego
 przeglądanie logów.

### `DEBUG`

The`DEBUG`Poziom służy do rejestrowania komunikatów, które pomagają programistom w identyfikacji
problemy podczas sesji debugowania. Treść komunikatów logowanych w pliku DEBUG
Poziom będzie się różnić w zależności od aplikacji, ale zazwyczaj zawierają
szczegółowe informacje, które pomagają programistom w rozwiązywaniu problemów
wydajnie. Może to obejmować stan zmiennych w otaczającym zakresie lub
odpowiednie kody błędów. |

## Inspiracja

Pomysł inspirowany jest projektem @christian1980nrw, do którego link znajduje się poniżej. Ten projekt jest moim pierwszym projektem z systemem operacyjnym Victron Venus, dlatego przejąłem pewne pomysły i podejścia z następujących projektów. Podejście jest takie samo, a w przypadku bardzo wąskich systemów prawdopodobnie lepsza jest implementacja za pomocą skryptu bash

##### – bardzo dziękujemy za przekazanie wiedzy:

-   [Przełącznik rynku spot](https://github.com/christian1980nrw/Spotmarket-Switcher)
-   [dynamiczny](https://github.com/tfranssen/dynamic-ess)
