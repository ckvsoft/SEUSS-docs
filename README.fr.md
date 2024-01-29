![Logo](views/static/images/logo-seuss.png?raw=true "SEUSS")

# SEUSS

#### [SEUSS -> Commutateur de marché spot pour unité Smart Ess]

# Paramètres

## Général

| Paramètre       | Signification                                                                                                                                              |
| --------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `time_zone`     | Indispensable pour un timing correct des opérations en fonction de votre situation géographique.<br/>Formater comme`Europe/Vienna`,`Europe/Amsterdam`, ... |
| `log_file_path` | Définit un chemin alternatif dans lequel les fichiers journaux sont enregistrés.                                                                           |
| `log_level`     | Les niveaux de journalisation utilisés sont : INFO, AVERTISSEMENT, ERREUR et DEBUG. voir[Niveaux de journalisation](#loglevels)                            |

## Des prix

| Paramètre                                  | Signification                                                                                                                                                                                                                                                                                                                      |
| ------------------------------------------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `use_second_day`                           | activer/désactiver la comparaison des prix d'aujourd'hui et de demain s'ils deviennent disponibles<br/>Remarque : Si vous l'activez et que les prix diminuent sur plusieurs jours, il est possible qu'il n'y ait pas de facturation ni de changement pendant plusieurs jours jusqu'à ce que les prix les plus bas soient atteints. |
| `number_of_lowest_prices_for_charging`     | le nombre de prix les moins chers auxquels le chargement devrait/peut être effectué                                                                                                                                                                                                                                                |
| `number_of_highest_prices_for_discharging` | le nombre de prix les plus élevés auxquels la décharge devrait/peut être effectuée                                                                                                                                                                                                                                                 |
| `charging_price_limit`                     | la recharge est toujours activée en dessous de ce prix<br/>le nombre de prix les plus élevés auxquels la décharge devrait/peut être effectuée                                                                                                                                                                                      |

## Unités ESS

### Victron

| Paramètre    | Signification                                                                                                                                                                                                             |
| :----------- | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `use_vrm`    | Si ce point est activé (vrai), une tentative de connexion au Victron via le portail VRM est effectuée.<br/>Cela nécessite un utilisateur/mot de passe dans le portail VRM                                                 |
| `ip_address` | L'adresse IP locale du Victron.<br/>Ceci est requis si "use_vrm" est désactivé (faux).<br/>Sinon ce champ reste vide                                                                                                      |
| `unit_id`    | ID du portail VRM<br/>peut être trouvé dans Paramètres / Portail en ligne VRM / Identifiant du portail VRM.<br/>Remarque : Cet identifiant est requis pour accéder au Victron même si vous n'utilisez pas de portail VRM. |
| `user`       | adresse e-mail que vous utilisez pour vous connecter au portail VRM                                                                                                                                                       |
| `password`   | mot de passe que vous utilisez pour vous connecter au portail VRM                                                                                                                                                         |

## Marchés

### répondre

| Paramètre | Signification                                                      |
| :-------- | :----------------------------------------------------------------- |
| `country` | Choisissez l'emplacement AT ou DE                                  |
| `primary` | Si ce marché est activé, ce point le définit comme marché primaire |
| `enabled` | définir votre marché comme activé/désactivé                        |

### Enzo est

| Paramètre    | Signification                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
| :----------- | :-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `api_token`  | Comment obtenir le jeton de sécurité API gratuit :<br/>1. Allez à<https://transparency.entsoe.eu/>--> inscrivez-vous et créez un compte<br/>2. Envoyez un e-mail à[transparency@entsoe.eu](mailto:transparency@entsoe.eu)avec « Accès API Restful » dans la ligne d'objet<br/>3. Le Helpdesk ENTSO-E répondra à votre demande dans un délai de 3 jours ouvrables.<br/>4. Générez un jeton de sécurité sur<https://transparency.entsoe.eu/usrm/user/myAccountSettings> |
| `in_domain`  | Pour connaître votre clé de domaine d'entrée et de sortie, accédez à :<br/><https://www.entsoe.eu/data/energy-identification-codes-eic/eic-area-codes-map/>                                                                                                                                                                                                                                                                                                           |
| `out_domain` | comme in_domain                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| `primary`    | Si ce marché est activé, ce point le définit comme marché primaire                                                                                                                                                                                                                                                                                                                                                                                                    |
| `enabled`    | définir votre marché comme activé/désactivé                                                                                                                                                                                                                                                                                                                                                                                                                           |

### Tiber

| Paramètre    | Signification                                                                                                                                                                                                                                                                                                                                                                |
| :----------- | :--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `api_token`  | Pour obtenir la clé tibber_api_key :<br/>1. connectez-vous avec un compte Tibber gratuit ou client sur<https://developer.tibber.com/settings/access-token><br/>2. Créez un token en sélectionnant les scopes dont vous avez besoin (sélectionnez "prix")<br/>3. Utilisez ce lien pour créer un compte gratuit avec votre smartphone :<https://tibber.com/de/invite/ojgfbx2e> |
| `price_unit` | Mis à:<br/>"énergie" pour utiliser les prix du marché spot (par défaut),<br/>"total" pour utiliser les prix totaux incluant les taxes et frais,<br/>"taxe" pour utiliser uniquement les taxes et frais                                                                                                                                                                       |
| `primary`    | Si ce marché est activé, ce point le définit comme marché primaire                                                                                                                                                                                                                                                                                                           |
| `enabled`    | définir votre marché comme activé/désactivé                                                                                                                                                                                                                                                                                                                                  |

* * *

# Niveaux de journalisation

### `ERROR`

Le`ERROR`Le niveau de journalisation indique les conditions d'erreur au sein d'une application qui entravent l'exécution d'une opération spécifique. Bien que l'application puisse continuer à fonctionner avec un niveau de fonctionnalité ou de performances réduit,<br/>`ERROR`les journaux signifient des problèmes qui doivent être étudiés rapidement.

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
