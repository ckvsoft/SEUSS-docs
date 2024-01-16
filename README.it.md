[ceco](README.cs.md)-[danese](README.da.md)-[Tedesco](README.de.md)-[Inglese](README.md)-[spagnolo](README.es.md)-[Estone](README.et.md)-[finlandese](README.fi.md)-[Francese](README.fr.md)-[greco](README.el.md)-[Italiano](README.it.md)-[Olandese](README.nl.md)-[norvegese](README.no.md)-[Polacco](README.pl.md)-[portoghese](README.pt.md)-[svedese](README.sv.md)-[giapponese](README.ja.md)

![Logo](views/static/images/logo-seuss.png?raw=true "SEUSS")

# SEUSS

#### [SEUSS -> Commutatore spotmarket unità Smart Ess]

# Impostazioni

## Generale

| Collocamento    | Senso                                                                                                                                                        |
| --------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `time_zone`     | Indispensabile per una corretta tempistica delle operazioni in base alla propria posizione geografica.<br/>Formato come Europa/Vienna, Europa/Amsterdam, ... |
| `log_file_path` | Imposta un percorso alternativo in cui vengono salvati i file di registro.                                                                                   |
| `log_level`     | I livelli di registro utilizzati sono: INFO, ATTENZIONE, ERRORE e DEBUG. Vedere[Livelli di registro](#loglevels)                                             |

## Prezzi

| Collocamento                               | Senso                                                                                                                                                                                                                                                                                                                |
| ------------------------------------------ | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `use_second_day`                           | abilitare/disabilitare il confronto dei prezzi di oggi e di domani se diventano disponibili<br/>Nota: se attivi questa opzione e i prezzi diminuiscono nell'arco di diversi giorni, è possibile che non venga effettuato alcun addebito o cambio per diversi giorni finché non vengono raggiunti i prezzi più bassi. |
| `number_of_lowest_prices_for_charging`     | il numero dei prezzi più economici ai quali il carico dovrebbe/potrebbe essere effettuato                                                                                                                                                                                                                            |
| `number_of_highest_prices_for_discharging` | il numero dei prezzi più elevati ai quali lo scarico dovrebbe/potrebbe essere effettuato                                                                                                                                                                                                                             |
| `charging_price_limit`                     | la ricarica è sempre abilitata al di sotto di questo prezzo<br/>il numero dei prezzi più elevati ai quali lo scarico dovrebbe/potrebbe essere effettuato                                                                                                                                                             |

## Unità ESS

### Victron

| Collocamento | Senso                                                                                                                                                                                    |
| :----------- | :--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `use_vrm`    | Se questo punto è abilitato (vero), viene effettuato un tentativo di connessione al Victron tramite il portale VRM.<br/>Ciò richiede un utente/password nel portale VRM                  |
| `ip_address` | L'indirizzo IP locale del Victron.<br/>Ciò è necessario se "use_vrm" è disabilitato (falso).<br/>Altrimenti questo campo rimane vuoto                                                    |
| `unit_id`    | ID del portale VRM<br/>è disponibile in Impostazioni/Portale online VRM/ID portale VRM.<br/>Nota: questo ID è necessario per accedere al Victron anche se non si utilizza un portale VRM |
| `user`       | indirizzo e-mail utilizzato per connettersi al portale VRM                                                                                                                               |
| `password`   | password utilizzata per connettersi al portale VRM                                                                                                                                       |

## Mercati

### risposta

| Collocamento | Senso                                                                        |
| :----------- | :--------------------------------------------------------------------------- |
| `country`    | Scegli la località AT o DE                                                   |
| `primary`    | Se questo mercato è abilitato, questo punto lo imposta come mercato primario |
| `enabled`    | imposta il tuo mercato come abilitato/disabilitato                           |

### Enzo lo è

| Collocamento | Senso                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| :----------- | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `api_token`  | Come ottenere il token di sicurezza API gratuito:<br/>1. Vai a<https://transparency.entsoe.eu/>--> registrati e crea un account<br/>2. Invia un'e-mail a[transparency@entsoe.eu](mailto:transparency@entsoe.eu)con "Accesso API riposante" nella riga dell'oggetto<br/>3. L'Helpdesk ENTSO-E risponderà alla tua richiesta entro 3 giorni lavorativi.<br/>4. Genera un token di sicurezza su<https://transparency.entsoe.eu/usrm/user/myAccountSettings> |
| `in_domain`  | Per conoscere la chiave del tuo dominio di entrata e uscita vai su:<br/><https://www.entsoe.eu/data/energy-identification-codes-eic/eic-area-codes-map/>                                                                                                                                                                                                                                                                                                 |
| `out_domain` | come in_dominio                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| `primary`    | Se questo mercato è abilitato, questo punto lo imposta come mercato primario                                                                                                                                                                                                                                                                                                                                                                             |
| `enabled`    | imposta il tuo mercato come abilitato/disabilitato                                                                                                                                                                                                                                                                                                                                                                                                       |

### Tibber

| Collocamento | Senso                                                                                                                                                                                                                                                                                                                                               |
| :----------- | :-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `api_token`  | Per ottenere tibber_api_key:<br/>1. accedi con un account Tibber gratuito o cliente su<https://developer.tibber.com/settings/access-token><br/>2. Crea un token selezionando gli ambiti di cui hai bisogno (seleziona "prezzo")<br/>3. Usa questo link per creare un account gratuito con il tuo smartphone:<https://tibber.com/de/invite/ojgfbx2e> |
| `price_unit` | Impostato:<br/>"energia" per utilizzare i prezzi del mercato spot (predefinito),<br/>"totale" per utilizzare i prezzi totali, comprese tasse e commissioni,<br/>"tassa" per utilizzare solo le tasse e le commissioni                                                                                                                               |
| `primary`    | Se questo mercato è abilitato, questo punto lo imposta come mercato primario                                                                                                                                                                                                                                                                        |
| `enabled`    | imposta il tuo mercato come abilitato/disabilitato                                                                                                                                                                                                                                                                                                  |

* * *

# Livelli di registro

### ERRORE

Il livello di registro ERRORE indica condizioni di errore all'interno di un'applicazione che ostacolano l'esecuzione di un'operazione specifica. Sebbene l'applicazione possa continuare a funzionare a un livello ridotto di funzionalità o prestazioni,<br/>I registri ERRORI indicano problemi che dovrebbero essere esaminati tempestivamente.

### AVVISARE

Gli eventi registrati al livello WARN in genere indicano che si è verificato qualcosa di inaspettato
si è verificato, ma per il momento l'applicazione può continuare a funzionare normalmente.
Viene anche utilizzato per indicare condizioni che dovrebbero essere prontamente affrontate prima di esse
degenerare in problemi per l'applicazione.

### INFORMAZIONI

Il livello INFO cattura gli eventi del sistema che sono significativi per il
scopo commerciale dell'applicazione. Tali eventi vengono registrati per dimostrare che il sistema lo è
funzionando normalmente. I sistemi di produzione in genere impostano per impostazione predefinita la registrazione a questo livello
in modo che un riepilogo del normale comportamento dell'applicazione sia visibile a chiunque
 esaminando i registri.

### DEBUG

Il livello DEBUG viene utilizzato per registrare messaggi che aiutano gli sviluppatori nell'identificazione
problemi durante una sessione di debug. Il contenuto dei messaggi registrati nel DEBUG
il livello varierà a seconda dell'applicazione, ma in genere contengono
informazioni dettagliate che aiutano i suoi sviluppatori nella risoluzione dei problemi
in modo efficiente. Ciò può includere lo stato delle variabili nell'ambito circostante o
relativi codici di errore. |
