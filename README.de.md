![Logo](views/static/images/logo-seuss.png?raw=true "SEUSS")

# SEUSS

### [SEUSS -> Smart Ess Unit Spotmarket Switcher]

#### Bitte melden Sie die Fehler und schlagen Sie Verbesserungen vor. Vielen Dank an alle, die bereits teilgenommen haben.

###### Wenn Sie Erweiterungen dazu beitragen möchten, senden Sie bitte den Pull-Request im Dev-Zweig. Für Fehlerbehebungen kann der Pull-Request auch auf dem Hauptzweig erfolgen

### Was macht diese Software?

Dies ist eine Python-3-Anwendung, die Ihre ESS-Einheit (Controller) zum richtigen Zeitpunkt einschaltet, wenn Ihre stündlichen dynamischen Energiepreise niedrig sind. Oder zum Entladen, wenn die Preise extrem hoch sind.

#### Derzeit unterstützte Systeme sind:

### ESS-Einheiten

* * *

-   **_Victron Venus OS Energiespeichersysteme wie die MultiPlus II-Serie_**

* * *

### Spotmärkte

* * *

-   **_Antwort_**
-   **_Enzo-E_**
-   **_Tibber_**

* * *

Die Steuerung der ESS-Einheit (Controller) erfolgt über mqtt. Der Vorteil dieser Steuerung ist:
dass diese Anwendung nicht direkt auf VenusOS laufen muss. Eine direkte Steuerung mit D-BUS ist in Planung

# Geprüft

Diese Version war erfolgreich mit

* * *

-   **_Linux Ubuntu >= 22.04_**
-   **_Venus OS Himbeeren >= vz.12_**

* * *

geprüft

# Installieren

Laden Sie das Installationsskript aus dem GitHub-Repository herunter und führen Sie den folgenden Befehl in Ihrem Terminal aus:

    wget -O seuss_install.sh https://raw.githubusercontent.com/ckvsoft/SEUSS/dev/scripts/seuss_install.sh`

Führen Sie das Installationsskript mit zusätzlichen Optionen aus, um alles in einem Unterverzeichnis für Ihre Inspektion vorzubereiten. Zum Beispiel:

    bash seuss_install.sh`

Das Standardverzeichnis ist /data/seuss (Venus OS). Sie können jedoch optional ein anderes Verzeichnis angeben, indem Sie die Umgebungsvariable TARGET_DIRECTORY verwenden, z. B.

    TARGET_DIRECTORY=/opt/seuss bash seuss_install.sh`

Auf einem Cerbo GX ist das Dateisystem schreibgeschützt gemountet. Sehen<https://www.victronenergy.com/live/ccgx:root_access>.
Um das Dateisystem beschreibbar zu machen, müssen Sie den folgenden Befehl ausführen, bevor Sie das Installationsskript ausführen:

    /opt/victronenergy/swupdate-scripts/resize2fs.sh

# Aufbau

Nach`SEUSS`Nach erfolgreicher Installation ist eine Website unter der IP-Adresse und dem Port 5000 verfügbar`Computer/VenusOS`auf welche`SEUSS`wurde installiert.

-   Sie können die Protokolldatei anzeigen oder herunterladen.
-   Darüber hinaus kann die Konfiguration über das durchgeführt werden[Konfigurationseditor]Menüpunkt.
-   Hier werden Tooltips für die meisten Punkte angezeigt.

#### Eintrags Ansicht

-   ![Logo](views/static/images/logviewer.png?raw=true "SEUSS Log Viewer")

#### Konfigurationseditor – ESS-Einheiten

-   ![Logo](views/static/images/configeditor_ess.png?raw=true "SEUSS Config Editor")

#### Konfigurationseditor – PV-Module

-   ![Logo](views/static/images/configeditor_panels.png?raw=true "SEUSS Config Editor")

Diese finden Sie auch in der Beschreibung der Einstellungen.
Für diejenigen, die lieber in einer Konfigurationsdatei arbeiten, gibt es config.toml

# Einstellungen

## Allgemein

| Einstellung     | Bedeutung                                                                                                                                                                |
| --------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `time_zone`     | Unverzichtbar für die korrekte zeitliche Abstimmung von Einsätzen basierend auf Ihrem geografischen Standort.<br/>Formatieren wie`Europe/Vienna`,`Europe/Amsterdam`, ... |
| `log_file_path` | Legt einen alternativen Pfad fest, in dem die Protokolldateien gespeichert werden.                                                                                       |
| `log_level`     | Verwendete Loglevel sind:`INFO`,`WARNING`,`ERROR`Und`DEBUG`. sehen[Protokollebenen](#loglevels)                                                                          |

## Preise

#### Bitte ändern Sie die Preise (verwenden Sie immer Cent/kWh, egal ob Sie Awattar (Anzeige von Cent/kWh) oder Entsoe API (Anzeige von EUR/MWh) verwenden / Nettopreise ohne Steuer).

| Einstellung                                | Bedeutung                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| ------------------------------------------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `use_second_day`                           | `enable/disable`um die Preise von heute und morgen zu vergleichen, sofern diese verfügbar sind<br/>Hinweis: Wenn Sie dies aktivieren und die Preise über mehrere Tage sinken, kann es sein, dass mehrere Tage lang nicht geladen oder geschaltet wird, bis die niedrigsten Preise erreicht sind.                                                                                                                                                                                                                                                                                                            |
| `number_of_lowest_prices_for_charging`     | Hier können zwei Modi genutzt werden.<br/>Modus1:<br/>_die Anzahl der günstigsten Preise, zu denen aufgeladen werden soll/dürfe. Hier geben Sie ganze Zahlen ein<br/>Modus2:<br/>_Dabei wird die Anzahl der Preise anhand des Durchschnittspreises ermittelt. In diesem Modus geben Sie Dezimalzahlen ein. Z.B. 0,85, um alle Preise zu erhalten, die 85 % unter dem Durchschnitt liegen. Relevant ist hier die Angabe eines Kommawertes. Bei 1,0 wird davon ausgegangen, dass 100 % des Durchschnittspreises genommen werden (macht keinen Sinn), aber wenn 1 eingegeben wird, ist es 1 günstigster Preis  |
| `number_of_highest_prices_for_discharging` | Hier können zwei Modi genutzt werden.<br/>Modus1:<br/>_die Anzahl der teuersten Preise, zu denen entladen werden soll/dürfte. Hier geben Sie ganze Zahlen ein<br/>Modus2:<br/>_Dabei wird die Anzahl der Preise anhand des Durchschnittspreises ermittelt. In diesem Modus geben Sie Dezimalzahlen ein. Z.B. 1,25, um alle Preise zu erhalten, die 25 % über dem Durchschnitt liegen.<br/>Relevant ist hier die Angabe eines Kommawertes. Bei 1,0 wird davon ausgegangen, dass 100 % des Durchschnittspreises genommen werden (macht keinen Sinn), aber wenn 1 eingegeben wird, ist es der 1 teuerste Preis |
| `charging_price_limit`                     | Unterhalb dieses Preises ist das Laden immer aktiviert<br/>die Anzahl der teuersten Preise, zu denen entladen werden soll/darf                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |

## ESS-Einheiten

### Victron

| Einstellung           | Bedeutung                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| :-------------------- | :--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `use_vrm`             | Wenn dieser Punkt aktiviert ist (true), wird versucht, über das VRM-Portal eine Verbindung zum Victron herzustellen.<br/>Hierzu ist ein Benutzer/Passwort im VRM-Portal erforderlich                                                                                                                                                                                                                                                                                         |
| `ip_address`          | Die lokale IP-Adresse des Victron.<br/>Dies ist erforderlich, wenn`use_vrm`ist deaktiviert (false).<br/>Ansonsten bleibt dieses Feld leer                                                                                                                                                                                                                                                                                                                                    |
| `unit_id`             | VRM-Portal-ID<br/>finden Sie in der`Settings / VRM online portal / VRM Portal Id`.<br/>Hinweis: Diese ID ist für den Zugriff auf Victron erforderlich, auch wenn Sie kein VRM-Portal verwenden                                                                                                                                                                                                                                                                               |
| `user`                | E-Mail-Adresse, mit der Sie sich mit dem VRM-Portal verbinden                                                                                                                                                                                                                                                                                                                                                                                                                |
| `password`            | Passwort, mit dem Sie sich mit dem VRM-Portal verbinden                                                                                                                                                                                                                                                                                                                                                                                                                      |
| `max_discharge_power` | Standard: -1<br/>Wenn du benutzt`Limit inverter power`Im ESS-Menü muss dieser Wert hier eingegeben werden.<br/>Wenn der Wechselrichter auf eingestellt ist`Discharge false`Durch diese App wird dieser Wert im ESS überschrieben.<br/>Dieser Grenzwert wird hier im Entlademodus im ESS eingestellt.<br/>Wenn kein Grenzwert festgelegt ist, belassen Sie den Wert bei`-1`.<br/>Beispiel: Geben Sie ein`1000`die Entlastung zu begrenzen`1000W`, Eingeben`-1`für volle Power |
| `primary`             | Wenn dieser Markt aktiviert ist, wird er durch diesen Punkt als Primärmarkt festgelegt                                                                                                                                                                                                                                                                                                                                                                                       |
| `enabled`             | Um diesen Eintrag nutzen zu können, muss er vorhanden sein`enabled`. Ansonsten`disabled`                                                                                                                                                                                                                                                                                                                                                                                     |

## Spotmärkte

### Antwort

| Einstellung | Bedeutung                                                                                |
| :---------- | :--------------------------------------------------------------------------------------- |
| `country`   | Wählen Sie Standort AT oder DE                                                           |
| `primary`   | Wenn dieser Markt aktiviert ist, wird er durch diesen Punkt als Primärmarkt festgelegt   |
| `enabled`   | Um diesen Eintrag nutzen zu können, muss er vorhanden sein`enabled`. Ansonsten`disabled` |

### Enzo ist

| Einstellung  | Bedeutung                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
| :----------- | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `api_token`  | So erhalten Sie das kostenlose API-Sicherheitstoken:<br/>1. Gehen Sie zu<https://transparency.entsoe.eu/>-> registrieren und ein Konto erstellen<br/>2. Senden Sie eine E-Mail an[transparency@entsoe.eu](mailto:transparency@entsoe.eu)mit „Restful API access“ in der Betreffzeile<br/>3. Der ENTSO-E Helpdesk wird Ihre Anfrage innerhalb von 3 Werktagen beantworten.<br/>4. Generieren Sie ein Sicherheitstoken unter<https://transparency.entsoe.eu/usrm/user/myAccountSettings> |
| `in_domain`  | Um Ihren In- und Out-Domain-Schlüssel herauszufinden, gehen Sie zu:<br/><https://www.entsoe.eu/data/energy-identification-codes-eic/eic-area-codes-map/>                                                                                                                                                                                                                                                                                                                               |
| `out_domain` | wie`in_domain`                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
| `primary`    | Wenn dieser Markt aktiviert ist, wird er durch diesen Punkt als Primärmarkt festgelegt                                                                                                                                                                                                                                                                                                                                                                                                 |
| `enabled`    | Um diesen Eintrag nutzen zu können, muss er vorhanden sein`enabled`. Ansonsten`disabled`                                                                                                                                                                                                                                                                                                                                                                                               |

### Tibber

| Einstellung  | Bedeutung                                                                                                                                                                                                                                                                                                                                                                                        |
| :----------- | :----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `api_token`  | So erhalten Sie den tibber_api_key:<br/>1. Melden Sie sich mit einem kostenlosen oder Kundenkonto bei Tibber an<https://developer.tibber.com/settings/access-token><br/>2. Erstellen Sie einen Token, indem Sie die benötigten Bereiche auswählen (wählen Sie „Preis“).<br/>3. Über diesen Link erstellen Sie ein kostenloses Konto mit Ihrem Smartphone:<https://tibber.com/de/invite/ojgfbx2e> |
| `price_unit` | Einstellen:<br/>„Energie“, um die Spotmarktpreise zu verwenden (Standard),<br/>„total“, um die Gesamtpreise inklusive Steuern und Gebühren zu verwenden,<br/>„Steuer“, um nur die Steuern und Gebühren zu verwenden                                                                                                                                                                              |
| `primary`    | Wenn dieser Markt aktiviert ist, wird er durch diesen Punkt als Primärmarkt festgelegt                                                                                                                                                                                                                                                                                                           |
| `enabled`    | Um diesen Eintrag nutzen zu können, muss er vorhanden sein`enabled`. Ansonsten`disabled`                                                                                                                                                                                                                                                                                                         |

## PV-Module

| Einstellung | Bedeutung                                                                                   |
| :---------- | :------------------------------------------------------------------------------------------ |
| `LocLat`    | Breite                                                                                      |
| `LocLon`    | Längengrad                                                                                  |
| `angle`     | Winkel Ihrer Paneele 0 (horizontal) … 90 (vertikal)                                         |
| `direction` | Ebenenazimut, -180 … 180 (-180 = Norden, -90 = Osten, 0 = Süden, 90 = Westen, 180 = Norden) |
| `totPower`  | installierte Modulleistung in Kilowatt                                                      |
| `enabled`   | Um diesen Eintrag nutzen zu können, muss er vorhanden sein`enabled`. Ansonsten`disabled`    |

* * *

## Protokollebenen

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

## Inspiration

Die Idee ist inspiriert von dem unten verlinkten @christian1980nrw-Projekt. Dieses Projekt ist mein erstes mit dem Victron Venus OS, daher habe ich einige Ideen und Ansätze aus den folgenden Projekten übernommen. Der Ansatz ist derselbe und für sehr schmale Systeme ist die Implementierung mit einem Bash-Skript wahrscheinlich besser

##### – vielen Dank für die Weitergabe des Wissens:

-   [Spotmarkt-Umschalter](https://github.com/christian1980nrw/Spotmarket-Switcher)
-   [dynamisch](https://github.com/tfranssen/dynamic-ess)
