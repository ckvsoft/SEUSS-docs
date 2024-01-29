![Logo](views/static/images/logo-seuss.png?raw=true "SEUSS")

# SEUSS

### [SEUSS -> Commutateur de marché spot pour unité Smart Ess]

#### Veuillez signaler les bugs et suggérer des améliorations. Merci à tous ceux qui ont déjà participé.

###### Si vous souhaitez contribuer à des extensions, veuillez soumettre la pull request dans la branche dev. Pour les corrections de bugs, la pull request peut également être effectuée sur la branche principale

### Que fait ce logiciel ?

Il s'agit d'une application Python 3 qui allume votre unité ESS (contrôleur) au bon moment lorsque vos prix horaires dynamiques de l'énergie sont bas. Ou utilisé pour décharger lorsque les prix sont extrêmement élevés.

#### Les systèmes actuellement pris en charge sont :

### Unités ESS

* * *

-   **_Systèmes de stockage d'énergie Victron Venus OS tels que la série MultiPlus II_**

* * *

### Marchés au comptant

* * *

-   **_répondre_**
-   **_Enzo-E_**
-   **_Tiber_**

* * *

Le contrôle de l'unité ESS (contrôleur) se fait via mqtt. L'avantage de ce contrôle est :
que cette application ne doit pas nécessairement s'exécuter directement sur VenusOS. Un contrôle direct avec D-BUS est en préparation

# Testé

Cette version a eu du succès avec

* * *

-   **_Linux-Ubuntu >= 22.04_**
-   **_Venus OS Raspberry >= v3.12_**

* * *

testé

# Installer

Téléchargez le script d'installation depuis le référentiel GitHub, exécutez la commande suivante dans votre terminal :

    wget -O seuss_install.sh https://raw.githubusercontent.com/ckvsoft/SEUSS/dev/scripts/seuss_install.sh`

Exécutez le script d'installation avec des options supplémentaires pour préparer tout ce qui se trouve dans un sous-répertoire pour votre inspection. Par exemple:

    bash seuss_install.sh`

Le répertoire par défaut est /data/seuss (Venus OS). Mais vous pouvez éventuellement spécifier un répertoire différent en utilisant la variable d'environnement TARGET_DIRECTORY, par exemple.

    TARGET_DIRECTORY=/opt/seuss bash seuss_install.sh`

Sur un Cerbo GX, le système de fichiers est monté en lecture seule. Voir<https://www.victronenergy.com/live/ccgx:root_access>.
Afin de rendre le système de fichiers accessible en écriture, vous devez exécuter la commande suivante avant d'exécuter le script d'installation :

    /opt/victronenergy/swupdate-scripts/resize2fs.sh

# Configuration

Après`SEUSS`a été installé avec succès, un site Web est disponible à l'adresse IP et au port 5000 du`Computer/VenusOS`sur lequel`SEUSS`etait installé.

-   Vous pouvez afficher ou télécharger le fichier journal.
-   De plus, la configuration peut être effectuée à l'aide du[Éditeur de configuration]élément du menu.
-   Des info-bulles pour la plupart des points sont affichées ici.

#### Visionneuse de journaux

-   ![Logo](views/static/images/logviewer.png?raw=true "SEUSS Log Viewer")

#### Éditeur de configuration - Unités ESS

-   ![Logo](views/static/images/configeditor_ess.png?raw=true "SEUSS Config Editor")

#### Éditeur de configuration - Panneaux PV

-   ![Logo](views/static/images/configeditor_panels.png?raw=true "SEUSS Config Editor")

Ceux-ci peuvent également être trouvés dans la description des paramètres.
Pour ceux qui préfèrent travailler dans un fichier de configuration, il existe config.toml

# Paramètres

## Général

| Paramètre       | Signification                                                                                                                                              |
| --------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `time_zone`     | Indispensable pour un timing correct des opérations en fonction de votre situation géographique.<br/>Formater comme`Europe/Vienna`,`Europe/Amsterdam`, ... |
| `log_file_path` | Définit un chemin alternatif dans lequel les fichiers journaux sont enregistrés.                                                                           |
| `log_level`     | Les niveaux de journalisation utilisés sont :`INFO`,`WARNING`,`ERROR`et`DEBUG`. voir[Niveaux de journalisation](#loglevels)                                |

## Des prix

#### Veuillez modifier les prix (utilisez toujours Cent/kWh, peu importe si vous utilisez Awattar (affichant Cent/kWh) ou Entsoe API (affichant EUR/MWh) / prix nets hors taxes).

| Paramètre                                  | Signification                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| ------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `use_second_day`                           | `enable/disable`comparer les prix d'aujourd'hui et de demain s'ils deviennent disponibles<br/>Remarque : Si vous l'activez et que les prix diminuent sur plusieurs jours, il est possible qu'il n'y ait pas de facturation ni de changement pendant plusieurs jours jusqu'à ce que les prix les plus bas soient atteints.                                                                                                                                                                                                                                                                               |
| `number_of_lowest_prices_for_charging`     | Deux modes peuvent être utilisés ici.<br/>mode1 :<br/>_le nombre de prix les moins chers auxquels la facturation devrait/peut avoir lieu. Ici, vous entrez des nombres entiers<br/>mode2 :<br/>_Ici, le nombre de prix est déterminé sur la base du prix moyen. Pour ce mode, vous entrez des nombres décimaux. Par exemple. 0,85 pour recevoir tous les prix qui sont 85 % inférieurs à la moyenne. Ce qui est pertinent ici, c'est la spécification d'une valeur virgule. Avec 1,0, on suppose que 100 % du prix moyen est pris (cela n'a aucun sens) mais si 1 est entré, c'est 1 prix le moins cher |
| `number_of_highest_prices_for_discharging` | Deux modes peuvent être utilisés ici.<br/>mode1 :<br/>_le nombre de prix les plus élevés auxquels la décharge devrait/peut avoir lieu. Ici, vous entrez des nombres entiers<br/>mode2 :<br/>_Ici, le nombre de prix est déterminé sur la base du prix moyen. Pour ce mode, vous entrez des nombres décimaux. Par exemple. 1,25 pour recevoir tous les prix supérieurs de 25 % à la moyenne.<br/>Ce qui est pertinent ici, c'est la spécification d'une valeur virgule. Avec 1,0, on suppose que 100 % du prix moyen est pris (cela n'a aucun sens) mais si 1 est entré, c'est le prix le plus cher.     |
| `charging_price_limit`                     | la recharge est toujours activée en dessous de ce prix<br/>le nombre de prix les plus élevés auxquels la décharge devrait/peut être effectuée                                                                                                                                                                                                                                                                                                                                                                                                                                                           |

## Unités ESS

### Victron

| Paramètre             | Signification                                                                                                                                                                                                                                                                                                                                                                                                                              |
| :-------------------- | :----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `use_vrm`             | Si ce point est activé (vrai), une tentative de connexion au Victron via le portail VRM est effectuée.<br/>Cela nécessite un utilisateur/mot de passe dans le portail VRM                                                                                                                                                                                                                                                                  |
| `ip_address`          | L'adresse IP locale du Victron.<br/>Ceci est requis si`use_vrm`est désactivé (faux).<br/>Sinon ce champ reste vide                                                                                                                                                                                                                                                                                                                         |
| `unit_id`             | ID du portail VRM<br/>peut être trouvé dans le`Settings / VRM online portal / VRM Portal Id`.<br/>Remarque : Cet identifiant est requis pour accéder au Victron même si vous n'utilisez pas de portail VRM.                                                                                                                                                                                                                                |
| `user`                | adresse e-mail que vous utilisez pour vous connecter au portail VRM                                                                                                                                                                                                                                                                                                                                                                        |
| `password`            | mot de passe que vous utilisez pour vous connecter au portail VRM                                                                                                                                                                                                                                                                                                                                                                          |
| `max_discharge_power` | Par défaut : -1<br/>Si tu utilises`Limit inverter power`dans le menu ESS, cette valeur doit être saisie ici.<br/>Si l'onduleur est réglé sur`Discharge false`par cette application, cette valeur sera écrasée dans l'ESS.<br/>Cette limite est ici fixée en mode décharge dans l'ESS.<br/>Si aucune limite n'est définie, laissez la valeur à`-1`.<br/>Exemple : Entrer`1000`limiter le rejet à`1000W`, Entrer`-1`pour la pleine puissance |
| `primary`             | Si ce marché est activé, ce point le définit comme marché primaire                                                                                                                                                                                                                                                                                                                                                                         |
| `enabled`             | Pour utiliser cette entrée, il faut`enabled`. Sinon`disabled`                                                                                                                                                                                                                                                                                                                                                                              |

## Marchés au comptant

### répondre

| Paramètre | Signification                                                      |
| :-------- | :----------------------------------------------------------------- |
| `country` | Choisissez l'emplacement AT ou DE                                  |
| `primary` | Si ce marché est activé, ce point le définit comme marché primaire |
| `enabled` | Pour utiliser cette entrée, il faut`enabled`. Sinon`disabled`      |

### Enzo est

| Paramètre    | Signification                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
| :----------- | :-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `api_token`  | Comment obtenir le jeton de sécurité API gratuit :<br/>1. Allez à<https://transparency.entsoe.eu/>--> inscrivez-vous et créez un compte<br/>2. Envoyez un e-mail à[transparency@entsoe.eu](mailto:transparency@entsoe.eu)avec « Accès API Restful » dans la ligne d'objet<br/>3. Le Helpdesk ENTSO-E répondra à votre demande dans un délai de 3 jours ouvrables.<br/>4. Générez un jeton de sécurité sur<https://transparency.entsoe.eu/usrm/user/myAccountSettings> |
| `in_domain`  | Pour connaître votre clé de domaine d'entrée et de sortie, accédez à :<br/><https://www.entsoe.eu/data/energy-identification-codes-eic/eic-area-codes-map/>                                                                                                                                                                                                                                                                                                           |
| `out_domain` | comme`in_domain`                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
| `primary`    | Si ce marché est activé, ce point le définit comme marché primaire                                                                                                                                                                                                                                                                                                                                                                                                    |
| `enabled`    | Pour utiliser cette entrée, il faut`enabled`. Sinon`disabled`                                                                                                                                                                                                                                                                                                                                                                                                         |

### Tiber

| Paramètre    | Signification                                                                                                                                                                                                                                                                                                                                                                |
| :----------- | :--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `api_token`  | Pour obtenir la clé tibber_api_key :<br/>1. connectez-vous avec un compte Tibber gratuit ou client sur<https://developer.tibber.com/settings/access-token><br/>2. Créez un token en sélectionnant les scopes dont vous avez besoin (sélectionnez "prix")<br/>3. Utilisez ce lien pour créer un compte gratuit avec votre smartphone :<https://tibber.com/de/invite/ojgfbx2e> |
| `price_unit` | Mis à:<br/>"énergie" pour utiliser les prix du marché spot (par défaut),<br/>"total" pour utiliser les prix totaux incluant les taxes et frais,<br/>"taxe" pour utiliser uniquement les taxes et frais                                                                                                                                                                       |
| `primary`    | Si ce marché est activé, ce point le définit comme marché primaire                                                                                                                                                                                                                                                                                                           |
| `enabled`    | Pour utiliser cette entrée, il faut`enabled`. Sinon`disabled`                                                                                                                                                                                                                                                                                                                |

## Panneaux PV

| Paramètre   | Signification                                                                     |
| :---------- | :-------------------------------------------------------------------------------- |
| `LocLat`    | Latitude                                                                          |
| `LocLon`    | Longitude                                                                         |
| `angle`     | Angle de vos panneaux 0 (horizontal) … 90 (vertical)                              |
| `direction` | Azimut plan, -180 … 180 (-180 = nord, -90 = est, 0 = sud, 90 = ouest, 180 = nord) |
| `totPower`  | puissance des modules installés en kilo watt                                      |
| `enabled`   | Pour utiliser cette entrée, il faut`enabled`. Sinon`disabled`                     |

* * *

## Niveaux de journalisation

### `ERROR`

Le`ERROR`Le niveau de journalisation indique les conditions d'erreur au sein d'une application qui entravent l'exécution d'une opération spécifique. Même si l'application peut continuer à fonctionner avec un niveau de fonctionnalité ou de performances réduit,<br/>`ERROR`les journaux signifient des problèmes qui doivent être étudiés rapidement.

### `WARN`

Événements enregistrés au`WARN`Le niveau indique généralement que quelque chose d'inattendu s'est produit.
s'est produit, mais l'application peut continuer à fonctionner normalement pour le moment.
Il est également utilisé pour signifier des conditions qui doivent être rapidement traitées avant d'être
dégénérer en problèmes pour l’application.

### `INFO`

Le`INFO`Le niveau capture les événements dans le système qui sont importants pour le
l'objectif commercial de l'application. De tels événements sont enregistrés pour montrer que le système est
fonctionnant normalement. Les systèmes de production enregistrent généralement par défaut à ce niveau
afin qu'un résumé du comportement normal de l'application soit visible par tous
 examiner les journaux.

### `DEBUG`

Le`DEBUG`Le niveau est utilisé pour enregistrer les messages qui aident les développeurs à identifier
problèmes lors d’une session de débogage. Le contenu des messages enregistrés au DEBUG
Le niveau varie en fonction de votre application, mais ils contiennent généralement
des informations détaillées qui aident ses développeurs à résoudre les problèmes
efficacement. Cela peut inclure l'état des variables dans la portée environnante ou
codes d'erreur pertinents. |

## Inspiration

L'idée est inspirée du projet @christian1980nrw lié ci-dessous. Ce projet est mon premier avec le Victron Venus OS, j'ai donc adopté quelques idées et approches des projets suivants. L'approche est la même et pour les systèmes très étroits, l'implémentation avec un script bash est probablement meilleure.

##### – merci beaucoup de transmettre le savoir :

-   [Sélecteur de marché spot](https://github.com/christian1980nrw/Spotmarket-Switcher)
-   [dynamique](https://github.com/tfranssen/dynamic-ess)
