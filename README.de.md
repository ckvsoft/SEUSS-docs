![Logo](views/static/images/logo-seuss.png?raw=true "SEUSS")

# SEUSS

#### [SEUSS -> Smart Ess Unit Spotmarket Switcher]

# Einstellungen

## Allgemein

| Einstellung     | Bedeutung                                                                                                                                                                |
| --------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `time_zone`     | Unverzichtbar für die korrekte zeitliche Abstimmung von Einsätzen basierend auf Ihrem geografischen Standort.<br/>Formatieren wie`Europe/Vienna`,`Europe/Amsterdam`, ... |
| `log_file_path` | Legt einen alternativen Pfad fest, in dem die Protokolldateien gespeichert werden.                                                                                       |
| `log_level`     | Verwendete Loglevel sind: INFO, WARNING, ERROR und DEBUG. sehen[Protokollebenen](#loglevels)                                                                             |

## Preise

| Setting                                    | Bedeutung                                                                                                                                                                                                                                                                                                |
| ------------------------------------------ | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `use_second_day`                           | Aktivieren/deaktivieren Sie den Vergleich der Preise von heute und morgen, sofern diese verfügbar sind<br/>Hinweis: Wenn Sie dies aktivieren und die Preise über mehrere Tage sinken, kann es sein, dass mehrere Tage lang nicht geladen oder geschaltet wird, bis die niedrigsten Preise erreicht sind. |
| `number_of_lowest_prices_for_charging`     | die Anzahl der günstigsten Preise, zu denen verladen werden soll/darf                                                                                                                                                                                                                                    |
| `number_of_highest_prices_for_discharging` | die Anzahl der teuersten Preise, zu denen entladen werden soll/darf                                                                                                                                                                                                                                      |
| `charging_price_limit`                     | Unterhalb dieses Preises ist das Laden immer aktiviert<br/>die Anzahl der teuersten Preise, zu denen entladen werden soll/darf                                                                                                                                                                           |

## ESS-Einheiten

### Victron

| Einstellung  | Bedeutung                                                                                                                                                                                        |
| :----------- | :----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `use_vrm`    | Wenn dieser Punkt aktiviert ist (true), wird versucht, über das VRM-Portal eine Verbindung zum Victron herzustellen.<br/>Hierzu ist ein Benutzer/Passwort im VRM-Portal erforderlich             |
| `ip_address` | Die lokale IP-Adresse des Victron.<br/>Dies ist erforderlich, wenn „use_vrm“ deaktiviert (false) ist.<br/>Ansonsten bleibt dieses Feld leer                                                      |
| `unit_id`    | VRM-Portal-ID<br/>finden Sie unter Einstellungen / VRM-Onlineportal / VRM-Portal-ID.<br/>Hinweis: Diese ID ist für den Zugriff auf Victron erforderlich, auch wenn Sie kein VRM-Portal verwenden |
| `user`       | E-Mail-Adresse, mit der Sie sich mit dem VRM-Portal verbinden                                                                                                                                    |
| `password`   | Passwort, mit dem Sie sich mit dem VRM-Portal verbinden                                                                                                                                          |

## Märkte

### Antwort

| Einstellung | Bedeutung                                                                              |
| :---------- | :------------------------------------------------------------------------------------- |
| `country`   | Wählen Sie Standort AT oder DE                                                         |
| `primary`   | Wenn dieser Markt aktiviert ist, wird er durch diesen Punkt als Primärmarkt festgelegt |
| `enabled`   | Stellen Sie Ihren Markt auf aktiviert/deaktiviert ein                                  |

### Enzo ist

| Einstellung  | Bedeutung                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
| :----------- | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `api_token`  | So erhalten Sie das kostenlose API-Sicherheitstoken:<br/>1. Gehen Sie zu<https://transparency.entsoe.eu/>-> registrieren und ein Konto erstellen<br/>2. Senden Sie eine E-Mail an[transparency@entsoe.eu](mailto:transparency@entsoe.eu)mit „Restful API access“ in der Betreffzeile<br/>3. Der ENTSO-E Helpdesk wird Ihre Anfrage innerhalb von 3 Werktagen beantworten.<br/>4. Generieren Sie ein Sicherheitstoken unter<https://transparency.entsoe.eu/usrm/user/myAccountSettings> |
| `in_domain`  | Um Ihren In- und Out-Domain-Schlüssel herauszufinden, gehen Sie zu:<br/><https://www.entsoe.eu/data/energy-identification-codes-eic/eic-area-codes-map/>                                                                                                                                                                                                                                                                                                                               |
| `out_domain` | wie in_domain                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| `primary`    | Wenn dieser Markt aktiviert ist, wird er durch diesen Punkt als Primärmarkt festgelegt                                                                                                                                                                                                                                                                                                                                                                                                 |
| `enabled`    | Stellen Sie Ihren Markt auf aktiviert/deaktiviert ein                                                                                                                                                                                                                                                                                                                                                                                                                                  |

### Tibber

| Einstellung  | Bedeutung                                                                                                                                                                                                                                                                                                                                                                                        |
| :----------- | :----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `api_token`  | So erhalten Sie den tibber_api_key:<br/>1. Melden Sie sich mit einem kostenlosen oder Kundenkonto bei Tibber an<https://developer.tibber.com/settings/access-token><br/>2. Erstellen Sie einen Token, indem Sie die benötigten Bereiche auswählen (wählen Sie „Preis“).<br/>3. Über diesen Link erstellen Sie ein kostenloses Konto mit Ihrem Smartphone:<https://tibber.com/de/invite/ojgfbx2e> |
| `price_unit` | Einstellen:<br/>„Energie“, um die Spotmarktpreise zu verwenden (Standard),<br/>„total“, um die Gesamtpreise inklusive Steuern und Gebühren zu verwenden,<br/>„Steuer“, um nur die Steuern und Gebühren zu verwenden                                                                                                                                                                              |
| `primary`    | Wenn dieser Markt aktiviert ist, wird er durch diesen Punkt als Primärmarkt festgelegt                                                                                                                                                                                                                                                                                                           |
| `enabled`    | Stellen Sie Ihren Markt auf aktiviert/deaktiviert ein                                                                                                                                                                                                                                                                                                                                            |

* * *

# Protokollebenen

### `ERROR`

Der`ERROR`Die Protokollebene weist auf Fehlerbedingungen innerhalb einer Anwendung hin, die die Ausführung eines bestimmten Vorgangs behindern. Die Anwendung kann zwar weiterhin mit eingeschränkter Funktionalität oder Leistung funktionieren,<br/>`ERROR`Protokolle weisen auf Probleme hin, die umgehend untersucht werden sollten.

### `WARN`

Am protokollierte Ereignisse`WARN`Ebene weist normalerweise darauf hin, dass etwas Unerwartetes passiert ist
aufgetreten, aber die Anwendung kann vorerst weiterhin normal funktionieren.
Es wird auch verwendet, um Bedingungen zu kennzeichnen, die umgehend behoben werden sollten, bevor sie auftreten
zu Problemen für die Anwendung führen.

### `INFO`

Der`INFO`Die Ebene erfasst Ereignisse im System, die für das System von Bedeutung sind
Geschäftszweck der Anwendung. Solche Ereignisse werden protokolliert, um zu zeigen, dass das System in Ordnung ist
normal funktioniert. Produktionssysteme protokollieren normalerweise standardmäßig auf dieser Ebene
sodass eine Zusammenfassung des normalen Verhaltens der Anwendung für jeden sichtbar ist
 Überprüfung der Protokolle.

### `DEBUG`

Der`DEBUG`Die Ebene wird zum Protokollieren von Nachrichten verwendet, die Entwicklern bei der Identifizierung helfen
Probleme während einer Debugging-Sitzung. Der Inhalt der beim DEBUG protokollierten Nachrichten
Der Füllstand hängt von Ihrer Anwendung ab, enthält jedoch in der Regel Folgendes
detaillierte Informationen, die den Entwicklern bei der Fehlerbehebung helfen
effizient. Dies kann den Status von Variablen innerhalb des umgebenden Bereichs umfassen oder
relevante Fehlercodes. |
