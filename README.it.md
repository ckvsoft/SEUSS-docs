![Logo](views/static/images/logo-seuss.png?raw=true "SEUSS")

# SEUSS

### [SEUSS -> Commutatore spotmarket unità Smart Ess]

#### Si prega di segnalare i bug e suggerire miglioramenti. Grazie a tutti coloro che hanno già preso parte.

###### Se desideri contribuire con estensioni, invia la richiesta pull nel ramo dev. Per le correzioni di bug, la richiesta pull può essere effettuata anche sul ramo principale

### Cosa fa questo software?

Questa è un'applicazione Python 3 che accende la tua unità ESS (controller) al momento giusto quando i prezzi orari dinamici dell'energia sono bassi. Oppure utilizzato per lo scarico quando i prezzi sono estremamente alti.

#### I sistemi attualmente supportati sono:

### Unità ESS

* * *

-   **_Sistemi di accumulo di energia Victron Venus OS come la serie MultiPlus II_**

* * *

### Mercati spot

* * *

-   **_risposta_**
-   **_Enzo-E_**
-   **_Tibber_**

* * *

Il controllo dell'unità ESS (controller) avviene tramite mqtt. Il vantaggio di questo controllo è:
che questa applicazione non deve essere eseguita direttamente su VenusOS. Il controllo diretto con D-BUS è in lavorazione

# Testato

Questa versione ha avuto successo

* * *

-   **_LinuxUbuntu >= 22.04_**
-   **_Lamponi Venus OS >= vz.12_**

* * *

testato

# Installare

Scarica lo script di installazione dal repository GitHub ed esegui il seguente comando nel tuo terminale:

    wget -O seuss_install.sh https://raw.githubusercontent.com/ckvsoft/SEUSS/dev/scripts/seuss_install.sh`

Esegui lo script di installazione con opzioni aggiuntive per preparare tutto in una sottodirectory per l'ispezione. Per esempio:

    bash seuss_install.sh`

La directory predefinita è /data/seuss (sistema operativo Venus) Ma puoi facoltativamente specificare una directory diversa utilizzando la variabile di ambiente TARGET_DIRECTORY ad es.

    TARGET_DIRECTORY=/opt/seuss bash seuss_install.sh`

Su un Cerbo GX il filesystem è montato in sola lettura. Vedere<https://www.victronenergy.com/live/ccgx:root_access>.
Per rendere scrivibile il filesystem è necessario eseguire il seguente comando prima di eseguire lo script di installazione:

    /opt/victronenergy/swupdate-scripts/resize2fs.sh

# Configurazione

Dopo`SEUSS`è stato installato con successo, è disponibile un sito Web all'indirizzo IP e alla porta 5000 di`Computer/VenusOS`in cui`SEUSS`è stato installato.

-   È possibile visualizzare o scaricare il file di registro.
-   Inoltre la configurazione può essere effettuata utilizzando il file[Editor di configurazione]elemento del menu.
-   Qui vengono visualizzati i suggerimenti sugli strumenti per la maggior parte dei punti.

#### Visualizzatore registro

-   ![Logo](views/static/images/logviewer.png?raw=true "SEUSS Log Viewer")

#### Editor di configurazione - Unità ESS

-   ![Logo](views/static/images/configeditor_ess.png?raw=true "SEUSS Config Editor")

#### Editor di configurazione - Pannelli fotovoltaici

-   ![Logo](views/static/images/configeditor_panels.png?raw=true "SEUSS Config Editor")

Questi possono essere trovati anche nella descrizione delle Impostazioni.
Per coloro che preferiscono lavorare in un file di configurazione, c'è config.toml

# Impostazioni

## Generale

| Collocamento    | Senso                                                                                                                                                          |
| --------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `time_zone`     | Indispensabile per una corretta tempistica delle operazioni in base alla propria posizione geografica.<br/>Formato come`Europe/Vienna`,`Europe/Amsterdam`, ... |
| `log_file_path` | Imposta un percorso alternativo in cui vengono salvati i file di registro.                                                                                     |
| `log_level`     | I livelli di log utilizzati sono:`INFO`,`WARNING`,`ERROR`E`DEBUG`. Vedere[Livelli di registro](#loglevels)                                                     |

## Prezzi

#### Modifica i prezzi (utilizza sempre Cent/kWh, non importa se stai utilizzando Awattar (visualizza Cent/kWh) o Entsoe API (visualizza EUR/MWh) / prezzi netti, tasse escluse).

| Collocamento                               | Senso                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| ------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `use_second_day`                           | `enable/disable`per confrontare i prezzi di oggi e di domani se saranno disponibili<br/>Nota: se attivi questa opzione e i prezzi diminuiscono nell'arco di diversi giorni, è possibile che non venga effettuato alcun addebito o cambio per diversi giorni finché non vengono raggiunti i prezzi più bassi.                                                                                                                                                                                                                                                                                            |
| `number_of_lowest_prices_for_charging`     | Qui è possibile utilizzare due modalità.<br/>modalità1:<br/>_il numero dei prezzi più economici ai quali la tariffazione dovrebbe/potrebbe avvenire. Qui inserisci i numeri interi<br/>modalità2:<br/>_Qui il numero dei prezzi è determinato in base al prezzo medio. Per questa modalità si immettono numeri decimali. Per esempio. 0,85 per ricevere tutti i prezzi inferiori dell'85% alla media. Ciò che è rilevante qui è l'indicazione di un valore virgola. Con 1.0 si presuppone che venga preso il 100% del prezzo medio (non ha alcun senso) ma se viene inserito 1 è 1 prezzo più economico |
| `number_of_highest_prices_for_discharging` | Qui è possibile utilizzare due modalità.<br/>modalità1:<br/>_il numero dei prezzi più elevati ai quali dovrebbe/potrebbe avvenire lo scarico. Qui inserisci i numeri interi<br/>modalità2:<br/>_Qui il numero dei prezzi è determinato in base al prezzo medio. Per questa modalità si immettono numeri decimali. Per esempio. 1,25 per ricevere tutti i prezzi superiori alla media del 25%.<br/>Ciò che è rilevante qui è l'indicazione di un valore virgola. Con 1.0 si presuppone che venga preso il 100% del prezzo medio (non ha alcun senso) ma se viene inserito 1 è 1 il prezzo più caro       |
| `charging_price_limit`                     | la ricarica è sempre abilitata al di sotto di questo prezzo<br/>il numero dei prezzi più elevati ai quali lo scarico dovrebbe/potrebbe essere effettuato                                                                                                                                                                                                                                                                                                                                                                                                                                                |

## Unità ESS

### Victron

| Collocamento          | Senso                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| :-------------------- | :-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `use_vrm`             | Se questo punto è abilitato (vero), viene effettuato un tentativo di connessione al Victron tramite il portale VRM.<br/>Ciò richiede un utente/password nel portale VRM                                                                                                                                                                                                                                                                                         |
| `ip_address`          | L'indirizzo IP locale del Victron.<br/>Ciò è necessario se`use_vrm`è disabilitato (falso).<br/>Altrimenti questo campo rimane vuoto                                                                                                                                                                                                                                                                                                                             |
| `unit_id`             | ID del portale VRM<br/>può essere trovato in`Settings / VRM online portal / VRM Portal Id`.<br/>Nota: questo ID è necessario per accedere al Victron anche se non si utilizza un portale VRM                                                                                                                                                                                                                                                                    |
| `user`                | indirizzo e-mail utilizzato per connettersi al portale VRM                                                                                                                                                                                                                                                                                                                                                                                                      |
| `password`            | password utilizzata per connettersi al portale VRM                                                                                                                                                                                                                                                                                                                                                                                                              |
| `max_discharge_power` | Impostazione predefinita: -1<br/>Se usi`Limit inverter power`nel menu ESS, questo valore deve essere inserito qui.<br/>Se l'inverter è impostato su`Discharge false`da questa app, questo valore verrà sovrascritto nell'ESS.<br/>Questo limite qui è impostato in modalità di scarico nell'ESS.<br/>Se non è impostato alcun limite, lasciare il valore su`-1`.<br/>Esempio: Inserisci`1000`per limitare lo scarico a`1000W`, Accedere`-1`per la piena potenza |
| `primary`             | Se questo mercato è abilitato, questo punto lo imposta come mercato primario                                                                                                                                                                                                                                                                                                                                                                                    |
| `enabled`             | Per utilizzare questa voce deve essere`enabled`. Altrimenti`disabled`                                                                                                                                                                                                                                                                                                                                                                                           |

## Mercati spot

### risposta

| Collocamento | Senso                                                                        |
| :----------- | :--------------------------------------------------------------------------- |
| `country`    | Scegli la località AT o DE                                                   |
| `primary`    | Se questo mercato è abilitato, questo punto lo imposta come mercato primario |
| `enabled`    | Per utilizzare questa voce deve essere`enabled`. Altrimenti`disabled`        |

### Enzo lo è

| Collocamento | Senso                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| :----------- | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `api_token`  | Come ottenere il token di sicurezza API gratuito:<br/>1. Vai a<https://transparency.entsoe.eu/>--> registrati e crea un account<br/>2. Invia un'e-mail a[transparency@entsoe.eu](mailto:transparency@entsoe.eu)con "Accesso API riposante" nella riga dell'oggetto<br/>3. L'Helpdesk ENTSO-E risponderà alla tua richiesta entro 3 giorni lavorativi.<br/>4. Genera un token di sicurezza su<https://transparency.entsoe.eu/usrm/user/myAccountSettings> |
| `in_domain`  | Per conoscere la chiave del tuo dominio di entrata e uscita vai su:<br/><https://www.entsoe.eu/data/energy-identification-codes-eic/eic-area-codes-map/>                                                                                                                                                                                                                                                                                                 |
| `out_domain` | Piace`in_domain`                                                                                                                                                                                                                                                                                                                                                                                                                                         |
| `primary`    | Se questo mercato è abilitato, questo punto lo imposta come mercato primario                                                                                                                                                                                                                                                                                                                                                                             |
| `enabled`    | Per utilizzare questa voce deve essere`enabled`. Altrimenti`disabled`                                                                                                                                                                                                                                                                                                                                                                                    |

### Tibber

| Collocamento | Senso                                                                                                                                                                                                                                                                                                                                               |
| :----------- | :-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `api_token`  | Per ottenere tibber_api_key:<br/>1. accedi con un account Tibber gratuito o cliente su<https://developer.tibber.com/settings/access-token><br/>2. Crea un token selezionando gli ambiti di cui hai bisogno (seleziona "prezzo")<br/>3. Usa questo link per creare un account gratuito con il tuo smartphone:<https://tibber.com/de/invite/ojgfbx2e> |
| `price_unit` | Impostato:<br/>"energia" per utilizzare i prezzi del mercato spot (predefinito),<br/>"totale" per utilizzare i prezzi totali, comprese tasse e commissioni,<br/>"tassa" per utilizzare solo le tasse e le commissioni                                                                                                                               |
| `primary`    | Se questo mercato è abilitato, questo punto lo imposta come mercato primario                                                                                                                                                                                                                                                                        |
| `enabled`    | Per utilizzare questa voce deve essere`enabled`. Altrimenti`disabled`                                                                                                                                                                                                                                                                               |

## Pannelli fotovoltaici

| Collocamento | Senso                                                                              |
| :----------- | :--------------------------------------------------------------------------------- |
| `LocLat`     | Latitudine                                                                         |
| `LocLon`     | Longitudine                                                                        |
| `angle`      | Angolo dei pannelli 0 (orizzontale) … 90 (verticale)                               |
| `direction`  | Azimut piano, -180 … 180 (-180 = nord, -90 = est, 0 = sud, 90 = ovest, 180 = nord) |
| `totPower`   | potenza dei moduli installati in kilowatt                                          |
| `enabled`    | Per utilizzare questa voce deve essere`enabled`. Altrimenti`disabled`              |

* * *

## Livelli di registro

### `ERROR`

IL`ERROR`il livello di log indica condizioni di errore all'interno di un'applicazione che ostacolano l'esecuzione di un'operazione specifica. Sebbene l'applicazione possa continuare a funzionare a un livello ridotto di funzionalità o prestazioni,<br/>`ERROR`i log indicano problemi che dovrebbero essere esaminati tempestivamente.

### `WARN`

Eventi registrati su`WARN`il livello in genere indica che è successo qualcosa di inaspettato
si è verificato, ma per il momento l'applicazione può continuare a funzionare normalmente.
Viene anche utilizzato per indicare condizioni che dovrebbero essere prontamente affrontate prima di esse
degenerare in problemi per l'applicazione.

### `INFO`

IL`INFO`Il livello cattura gli eventi nel sistema che sono significativi per il
scopo commerciale dell'applicazione. Tali eventi vengono registrati per dimostrare che il sistema lo è
funzionando normalmente. I sistemi di produzione in genere impostano per impostazione predefinita la registrazione a questo livello
in modo che un riepilogo del normale comportamento dell'applicazione sia visibile a chiunque
 esaminando i registri.

### `DEBUG`

IL`DEBUG`level viene utilizzato per registrare messaggi che aiutano gli sviluppatori nell'identificazione
problemi durante una sessione di debug. Il contenuto dei messaggi registrati nel DEBUG
il livello varierà a seconda dell'applicazione, ma in genere contengono
informazioni dettagliate che aiutano i suoi sviluppatori nella risoluzione dei problemi
in modo efficiente. Ciò può includere lo stato delle variabili nell'ambito circostante o
relativi codici di errore. |

## Ispirazione

L'idea è ispirata al progetto @christian1980nrw collegato di seguito. Questo è il mio primo progetto con il sistema operativo Victron Venus, quindi ho adottato alcune idee e approcci dai seguenti progetti. L'approccio è lo stesso e per sistemi molto ristretti l'implementazione con uno script bash è probabilmente migliore

##### – grazie mille per aver trasmesso la conoscenza:

-   [Cambio del mercato spot](https://github.com/christian1980nrw/Spotmarket-Switcher)
-   [dinamicità](https://github.com/tfranssen/dynamic-ess)
