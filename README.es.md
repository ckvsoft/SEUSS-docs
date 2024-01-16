[checo](README.cs.md)-[danés](README.da.md)-[Alemán](README.de.md)-[Inglés](README.md)-[Español](README.es.md)-[estonio](README.et.md)-[finlandés](README.fi.md)-[Francés](README.fr.md)-[Griego](README.el.md)-[italiano](README.it.md)-[Holandés](README.nl.md)-[noruego](README.no.md)-[Polaco](README.pl.md)-[portugués](README.pt.md)-[sueco](README.sv.md)-[japonés](README.ja.md)

![Logo](views/static/images/logo-seuss.png?raw=true "SEUSS")

# SEUSS

#### [SEUSS -> Conmutador de mercado spot de unidad Smart Ess]

\#Prueba

# Ajustes

## General

| Configuración   | Significado                                                                                                                                     |
| --------------- | ----------------------------------------------------------------------------------------------------------------------------------------------- |
| `time_zone`     | Esencial para la sincronización correcta de las operaciones según su ubicación geográfica.<br/>Formato como Europa/Viena, Europa/Amsterdam, ... |
| `log_file_path` | Establece una ruta alternativa en la que se guardan los archivos de registro.                                                                   |
| `log_level`     | Los niveles de registro utilizados son: INFO, WARNING, ERROR y DEBUG. ver[Niveles de registro](#loglevels)                                      |

## Precios

| Configuración                              | Significado                                                                                                                                                                                                                                                                   |
| ------------------------------------------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `use_second_day`                           | habilitar/deshabilitar la comparación de precios de hoy y mañana si están disponibles<br/>Nota: Si activa esto y los precios disminuyen durante varios días, es posible que no se realicen cargos ni cambios durante varios días hasta que se alcancen los precios más bajos. |
| `number_of_lowest_prices_for_charging`     | el número de precios más baratos a los que se debe/puede realizar la carga                                                                                                                                                                                                    |
| `number_of_highest_prices_for_discharging` | el número de los precios más caros a los que se debe/puede realizar la descarga                                                                                                                                                                                               |
| `charging_price_limit`                     | La carga siempre está habilitada por debajo de este precio.<br/>el número de los precios más caros a los que se debe/puede realizar la descarga                                                                                                                               |

## Unidades ESS

### victron

| Configuración | Significado                                                                                                                                                                                                     |
| :------------ | :-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `use_vrm`     | Si este punto está habilitado (verdadero), se intenta conectarse a Victron a través del portal VRM.<br/>Esto requiere un usuario/contraseña en el portal VRM                                                    |
| `ip_address`  | La dirección IP local de Victron.<br/>Esto es necesario si "use_vrm" está deshabilitado (falso).<br/>De lo contrario este campo permanece vacío                                                                 |
| `unit_id`     | ID del portal VRM<br/>se puede encontrar en Configuración/portal en línea VRM/ID del portal VRM.<br/>Nota: Esta identificación es necesaria para acceder a Victron incluso si no está utilizando un portal VRM. |
| `user`        | dirección de correo electrónico que utiliza para conectarse al portal VRM                                                                                                                                       |
| `password`    | contraseña que utiliza para conectarse al portal VRM                                                                                                                                                            |

## Mercados

### respuesta

| Configuración | Significado                                                                    |
| :------------ | :----------------------------------------------------------------------------- |
| `country`     | Elija ubicación AT o DE                                                        |
| `primary`     | Si este mercado está habilitado este punto lo establece como mercado primario. |
| `enabled`     | configura tu mercado como habilitado/deshabilitado                             |

### Enzo es

| Configuración | Significado                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| :------------ | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `api_token`   | Cómo obtener el token de seguridad API gratuito:<br/>1. Ir a<https://transparency.entsoe.eu/>--> registrarse y crear una cuenta<br/>2. Envíe un correo electrónico a[transparency@entsoe.eu](mailto:transparency@entsoe.eu)con "Acceso API Restful" en la línea de asunto<br/>3. El servicio de asistencia técnica de ENTSO-E responderá a su solicitud en un plazo de 3 días laborables.<br/>4. Genere un token de seguridad en<https://transparency.entsoe.eu/usrm/user/myAccountSettings> |
| `in_domain`   | Para conocer su clave de dominio de entrada y salida, vaya a:<br/><https://www.entsoe.eu/data/energy-identification-codes-eic/eic-area-codes-map/>                                                                                                                                                                                                                                                                                                                                           |
| `out_domain`  | como en_dominio                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
| `primary`     | Si este mercado está habilitado este punto lo establece como mercado primario.                                                                                                                                                                                                                                                                                                                                                                                                               |
| `enabled`     | configura tu mercado como habilitado/deshabilitado                                                                                                                                                                                                                                                                                                                                                                                                                                           |

### Tibber

| Configuración | Significado                                                                                                                                                                                                                                                                                                                                                           |
| :------------ | :-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `api_token`   | Para obtener tibber_api_key:<br/>1. inicie sesión con una cuenta Tibber gratuita o de cliente en<https://developer.tibber.com/settings/access-token><br/>2. Cree un token seleccionando los alcances que necesita (seleccione "precio")<br/>3. Utilice este enlace para crear una cuenta gratuita con su teléfono inteligente:<https://tibber.com/de/invite/ojgfbx2e> |
| `price_unit`  | Ajustado a:<br/>"energía" para utilizar los precios del mercado spot (predeterminado),<br/>"total" para utilizar los precios totales, incluidos impuestos y tasas,<br/>"impuesto" para utilizar sólo los impuestos y tasas                                                                                                                                            |
| `primary`     | Si este mercado está habilitado este punto lo establece como mercado primario.                                                                                                                                                                                                                                                                                        |
| `enabled`     | configura tu mercado como habilitado/deshabilitado                                                                                                                                                                                                                                                                                                                    |

* * *

# niveles de registro

### ERROR

El nivel de registro de ERROR indica condiciones de error dentro de una aplicación que dificultan la ejecución de una operación específica. Si bien la aplicación puede continuar funcionando a un nivel reducido de funcionalidad o rendimiento,<br/>Los registros de ERRORES indican problemas que deben investigarse con prontitud.

### ADVERTIR

Los eventos registrados en el nivel WARN normalmente indican que ha ocurrido algo inesperado.
ocurrió, pero la aplicación puede continuar funcionando normalmente por el momento.
También se utiliza para indicar condiciones que deben abordarse rápidamente antes de que ocurran.
convertirse en problemas para la aplicación.

### INFORMACIÓN

El nivel INFO captura eventos en el sistema que son importantes para el
propósito comercial de la aplicación. Estos eventos se registran para mostrar que el sistema está
funcionando normalmente. Los sistemas de producción normalmente registran de forma predeterminada en este nivel.
para que cualquier persona pueda ver un resumen del comportamiento normal de la aplicación
 revisando los registros.

### DEPURAR

El nivel DEBUG se utiliza para registrar mensajes que ayudan a los desarrolladores a identificar
problemas durante una sesión de depuración. El contenido de los mensajes registrados en DEBUG.
El nivel variará dependiendo de su aplicación, pero normalmente contienen
información detallada que ayuda a sus desarrolladores a solucionar problemas
eficientemente. Esto puede incluir el estado de las variables dentro del alcance circundante o
códigos de error relevantes. |
