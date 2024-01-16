[Čeština ](README.cs.md) - [Dansk ](README.da.md) - [Deutsch ](README.de.md) - [English ](README.md) - [Español ](README.es.md) - [Estonian ](README.et.md) - [Finnish ](README.fi.md) - [Français ](README.fr.md) - [Greek ](README.el.md) - [Italian ](README.it.md) - [Nederlands ](README.nl.md) - [Norsk ](README.no.md) - [Polski ](README.pl.md) - [Portuguese ](README.pt.md) - [Svenska ](README.sv.md) - [日本語 ](README.ja.md)

![Logo](views/static/images/logo-seuss.png?raw=true "SEUSS")
# SEUSS
#### [SEUSS -> Smart Ess Unit Spotmarket Switcher]

# Configuration
## General
| Setting           | Meaning                                                                                                                             |
|-------------------|-------------------------------------------------------------------------------------------------------------------------------------|
| `time_zone`       | Essential for correct timing of operations based on your geographic location.<br/> Format like Europe/Vienna, Europe/Amsterdam, ... |
| `log_file_path`   | Sets an alternative path to which the log files are saved.                                                                          |
| `log_level`       | Used Loglevel are: INFO, WARNING, ERROR and DEBUG. see [Log Levels](#loglevels)                                                     |

## Prices
| Setting                                     | Meaning                                                                                                                                                                                                                                                                |
|---------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `use_second_day`                            | enable/disable to compare today and tomorrow prices if they become available<br/>Note: If you activate this and the prices decrease over several days,it is possible that there will be no charging or switching for several days until the lowest prices are reached. |
| `number_of_lowest_prices_for_charging`      | the number of cheapest prices at which loading should/may be made                                                                                                                                                                                                      |
| `number_of_highest_prices_for_discharging`  | the number of the most expensive prices at which discharging should/may be carried out                                                                                                                                                                                 |
| `charging_price_limit`                      | charging is always enabled below this price<br/> the number of the most expensive prices at which discharging should/may be carried out                                                                                                                                |

## ESS Units
### Victron
| Setting       | Meaning                                                                                                                                                                         |
|:--------------|:--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `use_vrm`     | If this point is enabled (true), an attempt is made to connect to the Victron via the VRM portal.<br/>This requires a user/password in the VRM portal                           |
| `ip_address`  | The local IP address of the Victron.<br/>This is required if "use_vrm" is disabled (false).<br/>Otherwise this field remains empty                                              |
| `unit_id`     | VRM Portal ID<br/>can be found in the Settings / VRM online portal / VRM Portal Id.<br/>Note: This ID is required to access the Victron even if you are not using a VRM portal  |
| `user`        | mail adress you use to connect to VRM portal                                                                                                                                    |
| `password`    | password you use to connect to VRM portal                                                                                                                                       |

## Markets
### aWATTar
| Setting   | Meaning                                                            |
|:----------|:--------------------------------------------------------------------|
| `country` | Choose location AT or DE                                           |
| `primary` | If this market is enabled this point sets it as the primary market |
| `enabled` | set your market as enabled/disabled                                |

### Entso-e
| Setting      | Meaning                                                                                                                                                                                                                                                                                                                                                                                             |
|:-------------|:-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `api_token`  | How to get the free api_security_token:<br/>1. Go to https://transparency.entsoe.eu/ --> register and create an account<br/>2. Send an email to transparency@entsoe.eu with “Restful API access” in the subject line<br/>3. The ENTSO-E Helpdesk will respond to your request within 3 working days.<br/>4. Generate a security token at https://transparency.entsoe.eu/usrm/user/myAccountSettings |
| `in_domain`  | To find out your in and out domain key go to:<br/>https://www.entsoe.eu/data/energy-identification-codes-eic/eic-area-codes-map/                                                                                                                                                                                                                                                                    |
| `out_domain` | like in_domain                                                                                                                                                                                                                                                                                                                                                                                      |
| `primary`    | If this market is enabled this point sets it as the primary market                                                                                                                                                                                                                                                                                                                                  |
| `enabled`    | set your market as enabled/disabled                                                                                                                                                                                                                                                                                                                                                                 |

### Tibber
| Setting      | Meaning                                                                                                                                                                                                                                                                                                                                                                                               |
|:-------------|:-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `api_token`  | To get the tibber_api_key:<br/>1. log in with a free or customer Tibber account at https://developer.tibber.com/settings/access-token<br/>2. Create a token by selecting the scopes you need (select "price")<br/>3. Use this link to create a free account with your smartphone: https://tibber.com/de/invite/ojgfbx2e                                                                               |
| `price_unit` | Set to:<br/>"energy" to use the spotmarket-prices (default),<br/>"total" to use the total prices including taxes and fees,<br/>"tax" to use only the taxes and fees                                                                                                                                                                                                                                   |
| `primary`    | If this market is enabled this point sets it as the primary market                                                                                                                                                                                                                                                                                                                                    |
| `enabled`    | set your market as enabled/disabled                                                                                                                                                                                                                                                                                                                                                                   |

***
# Loglevels
### ERROR
The ERROR log level indicates error conditions within an application that hinder the execution of a specific operation. While the application can continue functioning at a reduced level of functionality or performance,<br/>ERROR logs signify issues that should be investigated promptly.

### WARN
Events logged at the WARN level typically indicate that something unexpected has
occurred, but the application can continue to function normally for the time being.
It is also used to signify conditions that should be promptly addressed before they
escalate into problems for the application.

### INFO
The INFO level captures events in the system that are significant to the
application's business purpose. Such events are logged to show that the system is
operating normally. Production systems typically default to logging at this level
so that a summary of the application's normal behavior is visible to anyone
 reviewing the logs.

### DEBUG
The DEBUG level is used for logging messages that aid developers in identifying
issues during a debugging session. The content of the messages logged at the DEBUG
level will vary depending on your application, but they typically contain
detailed information that assists its developers in troubleshooting problems
efficiently. This can include variables' state within the surrounding scope or
relevant error codes.                                                                                                                                    |
