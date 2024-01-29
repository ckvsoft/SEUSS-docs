![Logo](views/static/images/logo-seuss.png?raw=true "SEUSS")

# SEUSS

#### [SEUSS -> Inteligentny przełącznik Spotmarket jednostki Ess]

# Ustawienia

## Ogólny

| Ustawienie      | Oznaczający                                                                                                                                          |
| --------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------- |
| `time_zone`     | Niezbędne do prawidłowego harmonogramu operacji w oparciu o Twoją lokalizację geograficzną.<br/>Sformatuj jak`Europe/Vienna`,`Europe/Amsterdam`, ... |
| `log_file_path` | Ustawia alternatywną ścieżkę, w której zapisywane są pliki dziennika.                                                                                |
| `log_level`     | Używane poziomy dziennika to: INFO, WARNING, ERROR i DEBUG. Widzieć[Poziomy dziennika](#loglevels)                                                   |

## Ceny

| Ustawienie                                 | Oznaczający                                                                                                                                                                                                                                                  |
| ------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `use_second_day`                           | włącz/wyłącz porównywanie dzisiejszych i przyszłych cen, jeśli będą dostępne<br/>Uwaga: jeśli aktywujesz tę opcję, a ceny będą spadać przez kilka dni, możliwe, że przez kilka dni nie będzie ładowania ani przełączania, aż do osiągnięcia najniższych cen. |
| `number_of_lowest_prices_for_charging`     | liczba najniższych cen, po jakich powinien/może odbywać się załadunek                                                                                                                                                                                        |
| `number_of_highest_prices_for_discharging` | liczba najdroższych cen, po jakich należy/można dokonywać rozładunku                                                                                                                                                                                         |
| `charging_price_limit`                     | poniżej tej ceny ładowanie jest zawsze włączone<br/>liczba najdroższych cen, po jakich należy/można dokonywać rozładunku                                                                                                                                     |

## Jednostki ESS

### Victron

| Ustawienie   | Oznaczający                                                                                                                                                                                                                              |
| :----------- | :--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `use_vrm`    | Jeśli ten punkt jest włączony (true), podejmowana jest próba połączenia z Victronem za pośrednictwem portalu VRM.<br/>Wymaga to użytkownika/hasła w portalu VRM                                                                          |
| `ip_address` | Lokalny adres IP Victron.<br/>Jest to wymagane, jeśli opcja „use_vrm” jest wyłączona (false).<br/>W przeciwnym razie to pole pozostaje puste                                                                                             |
| `unit_id`    | Identyfikator portalu VRM<br/>można znaleźć w Ustawieniach / portalu internetowym VRM / Identyfikatorze portalu VRM.<br/>Uwaga: ten identyfikator jest wymagany, aby uzyskać dostęp do Victron, nawet jeśli nie korzystasz z portalu VRM |
| `user`       | adres e-mail, którego używasz do łączenia się z portalem VRM                                                                                                                                                                             |
| `password`   | hasło, którego używasz do łączenia się z portalem VRM                                                                                                                                                                                    |

## Rynki

### odpowiedź

| Ustawienie | Oznaczający                                                              |
| :--------- | :----------------------------------------------------------------------- |
| `country`  | Wybierz lokalizację AT lub DE                                            |
| `primary`  | Jeśli ten rynek jest włączony, ten punkt ustawia go jako rynek pierwotny |
| `enabled`  | ustaw swój rynek jako włączony/wyłączony                                 |

### Enzo jest

| Ustawienie   | Oznaczający                                                                                                                                                                                                                                                                                                                                                                                                                                |
| :----------- | :----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `api_token`  | Jak zdobyć darmowy token bezpieczeństwa API:<br/>1. Przejdź do<https://transparency.entsoe.eu/>--> zarejestruj się i utwórz konto<br/>2. Wyślij e-mail do[transparency@entsoe.eu](mailto:transparency@entsoe.eu)z tematem „Restful API Access”.<br/>3. Helpdesk ENTSO-E odpowie na Twoją prośbę w terminie 3 dni roboczych.<br/>4. Wygeneruj token zabezpieczający pod adresem<https://transparency.entsoe.eu/usrm/user/myAccountSettings> |
| `in_domain`  | Aby znaleźć klucz domeny wejściowej i wyjściowej, przejdź do:<br/><https://www.entsoe.eu/data/energy-identification-codes-eic/eic-area-codes-map/>                                                                                                                                                                                                                                                                                         |
| `out_domain` | jak w_domenie                                                                                                                                                                                                                                                                                                                                                                                                                              |
| `primary`    | Jeśli ten rynek jest włączony, ten punkt ustawia go jako rynek pierwotny                                                                                                                                                                                                                                                                                                                                                                   |
| `enabled`    | ustaw swój rynek jako włączony/wyłączony                                                                                                                                                                                                                                                                                                                                                                                                   |

### Tibbera

| Ustawienie   | Meaning                                                                                                                                                                                                                                                                                                                                          |
| :----------- | :----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `api_token`  | Aby uzyskać tibber_api_key:<br/>1. zaloguj się za pomocą bezpłatnego lub klienta konta Tibber pod adresem<https://developer.tibber.com/settings/access-token><br/>2. Utwórz token wybierając potrzebne zakresy (wybierz „cena”)<br/>3. Użyj tego linku, aby utworzyć bezpłatne konto na swoim smartfonie:<https://tibber.com/de/invite/ojgfbx2e> |
| `price_unit` | Ustawić:<br/>"energia" aby skorzystać z cen rynkowych spot (domyślnie),<br/>„total”, aby zastosować ceny całkowite zawierające podatki i opłaty,<br/>„podatek”, aby używać wyłącznie podatków i opłat                                                                                                                                            |
| `primary`    | Jeśli ten rynek jest włączony, ten punkt ustawia go jako rynek pierwotny                                                                                                                                                                                                                                                                         |
| `enabled`    | ustaw swój rynek jako włączony/wyłączony                                                                                                                                                                                                                                                                                                         |

* * *

# Poziomy logowania

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
