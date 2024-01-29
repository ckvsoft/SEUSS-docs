![Logo](views/static/images/logo-seuss.png?raw=true "SEUSS")

# SEUSS

### [SEUSS -> Conmutador de mercado spot de unidad Smart Ess]

#### Informe los errores y sugiera mejoras. Gracias a todos los que ya han participado.

###### Si desea contribuir con extensiones a esto, envíe la solicitud de extracción en la rama de desarrollo. Para corregir errores, la solicitud de extracción también se puede realizar en la rama principal.

### que hace este software?

Esta es una aplicación Python 3 que enciende su unidad ESS (controlador) en el momento adecuado cuando los precios de energía dinámicos por hora son bajos. O se utiliza para descargar cuando los precios son extremadamente altos.

#### Los sistemas actualmente soportados son:

### Unidades ESS

* * *

-   **_Sistemas de almacenamiento de energía Victron Venus OS como la serie MultiPlus II_**

* * *

### Mercados al contado

* * *

-   **_respuesta_**
-   **_Enzo-E_**
-   **_Tibber_**

* * *

El control de la unidad ESS (controlador) se realiza mediante mqtt. La ventaja de este control es:
que esta aplicación no tiene que ejecutarse directamente en VenusOS. Se está trabajando en el control directo con D-BUS

# Probado

Esta versión tuvo éxito con

* * *

-   **_LinuxUbuntu>= 22.04_**
-   **_Venus OS Frambuesas >= vz.12_**

* * *

probado

# Instalar

Descargue el script de instalación desde el repositorio de GitHub y ejecute el siguiente comando en su terminal:

    wget -O seuss_install.sh https://raw.githubusercontent.com/ckvsoft/SEUSS/dev/scripts/seuss_install.sh`

Ejecute el script del instalador con opciones adicionales para preparar todo en un subdirectorio para su inspección. Por ejemplo:

    bash seuss_install.sh`

El directorio predeterminado es /data/seuss (Venus OS). Pero, opcionalmente, puede especificar un directorio diferente utilizando la variable de entorno TARGET_DIRECTORY, por ejemplo.

    TARGET_DIRECTORY=/opt/seuss bash seuss_install.sh`

En un Cerbo GX, el sistema de archivos está montado en solo lectura. Ver<https://www.victronenergy.com/live/ccgx:root_access>.
Para que se pueda escribir en el sistema de archivos, debe ejecutar el siguiente comando antes de ejecutar el script de instalación:

    /opt/victronenergy/swupdate-scripts/resize2fs.sh

# Configuración

Después`SEUSS`se ha instalado correctamente, hay un sitio web disponible en la dirección IP y el puerto 5000 del`Computer/VenusOS`en la que`SEUSS`fue instalado.

-   Puede ver o descargar el archivo de registro.
-   Además, la configuración se puede realizar mediante el[Editor de configuración]opción del menú.
-   Aquí se muestran sugerencias sobre herramientas para la mayoría de los puntos.

#### Visor de registros

-   ![Logo](views/static/images/logviewer.png?raw=true "SEUSS Log Viewer")

#### Editor de configuración: unidades ESS

-   ![Logo](views/static/images/configeditor_ess.png?raw=true "SEUSS Config Editor")

#### Editor de configuración: paneles fotovoltaicos

-   ![Logo](views/static/images/configeditor_panels.png?raw=true "SEUSS Config Editor")

Estos también se pueden encontrar en la descripción de Configuración.
Para aquellos que prefieren trabajar en un archivo de configuración, existe config.toml

# Ajustes

## General

| Configuración   | Significado                                                                                                                                          |
| --------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------- |
| `time_zone`     | Esencial para la sincronización correcta de las operaciones según su ubicación geográfica.<br/>Formatear como`Europe/Vienna`,`Europe/Amsterdam`, ... |
| `log_file_path` | Establece una ruta alternativa en la que se guardan los archivos de registro.                                                                        |
| `log_level`     | Los niveles de registro utilizados son:`INFO`,`WARNING`,`ERROR`y`DEBUG`. ver[Niveles de registro](#loglevels)                                        |

## Precios

#### Cambie los precios (use siempre Cent/kWh, sin importar si está usando Awattar (que muestra Cent/kWh) o Entsoe API (que muestra EUR/MWh) / precios netos sin impuestos).

| Configuración                              | Significado                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| ------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `use_second_day`                           | `enable/disable`para comparar los precios de hoy y mañana si están disponibles<br/>Nota: Si activa esto y los precios disminuyen durante varios días, es posible que no se realicen cargos ni cambios durante varios días hasta que se alcancen los precios más bajos.                                                                                                                                                                                                                                                                                                               |
| `number_of_lowest_prices_for_charging`     | Aquí se pueden utilizar dos modos.<br/>modo1:<br/>_el número de precios más baratos a los que debería o podría realizarse el cobro. Aquí ingresas números enteros.<br/>modo2:<br/>_Aquí el número de precios se determina en función del precio medio. Para este modo ingresa números decimales. P.ej. 0,85 para recibir todos los precios que están un 85% por debajo del promedio. Lo relevante aquí es la especificación de un valor de coma. Con 1.0 se supone que se toma el 100% del precio medio (no tiene ningún sentido) pero si se introduce 1 es 1 precio más barato      |
| `number_of_highest_prices_for_discharging` | Aquí se pueden utilizar dos modos.<br/>modo1:<br/>_el número de precios más caros a los que debería o podría tener lugar la descarga. Aquí ingresas números enteros.<br/>modo2:<br/>_Aquí el número de precios se determina en función del precio medio. Para este modo ingresa números decimales. P.ej. 1,25 para recibir todos los precios que estén un 25% por encima del promedio.<br/>Lo relevante aquí es la especificación de un valor de coma. Con 1.0 se supone que se toma el 100% del precio promedio (no tiene ningún sentido) pero si se ingresa 1 es 1 precio más caro |
| `charging_price_limit`                     | La carga siempre está habilitada por debajo de este precio.<br/>el número de los precios más caros a los que se debe/puede realizar la descarga                                                                                                                                                                                                                                                                                                                                                                                                                                      |

## Unidades ESS

### victron

| Configuración         | Significado                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| :-------------------- | :--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `use_vrm`             | Si este punto está habilitado (verdadero), se intenta conectarse a Victron a través del portal VRM.<br/>Esto requiere un usuario/contraseña en el portal VRM                                                                                                                                                                                                                                                                                               |
| `ip_address`          | La dirección IP local de Victron.<br/>Esto es necesario si`use_vrm`está deshabilitado (falso).<br/>De lo contrario este campo permanece vacío                                                                                                                                                                                                                                                                                                              |
| `unit_id`             | ID del portal VRM<br/>se puede encontrar en el`Settings / VRM online portal / VRM Portal Id`.<br/>Nota: Esta identificación es necesaria para acceder a Victron incluso si no está utilizando un portal VRM.                                                                                                                                                                                                                                               |
| `user`                | dirección de correo electrónico que utiliza para conectarse al portal VRM                                                                                                                                                                                                                                                                                                                                                                                  |
| `password`            | contraseña que utiliza para conectarse al portal VRM                                                                                                                                                                                                                                                                                                                                                                                                       |
| `max_discharge_power` | Predeterminado: -1<br/>Si utiliza`Limit inverter power`en el menú ESS entonces este valor debe ingresarse aquí.<br/>Si el inversor está configurado en`Discharge false`por esta aplicación, este valor se sobrescribirá en el ESS.<br/>Este límite aquí se establece en el modo de descarga en el ESS.<br/>Si no se establece ningún límite, deje el valor en`-1`.<br/>Ejemplo: entrar`1000`limitar la descarga a`1000W`, Ingresar`-1`para máxima potencia |
| `primary`             | Si este mercado está habilitado este punto lo establece como mercado primario.                                                                                                                                                                                                                                                                                                                                                                             |
| `enabled`             | Para utilizar esta entrada debe ser`enabled`. De lo contrario`disabled`                                                                                                                                                                                                                                                                                                                                                                                    |

## Mercados al contado

### respuesta

| Configuración | Significado                                                                    |
| :------------ | :----------------------------------------------------------------------------- |
| `country`     | Elija ubicación AT o DE                                                        |
| `primary`     | Si este mercado está habilitado este punto lo establece como mercado primario. |
| `enabled`     | Para utilizar esta entrada debe ser`enabled`. De lo contrario`disabled`        |

### Enzo es

| Configuración | Significado                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| :------------ | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `api_token`   | Cómo obtener el token de seguridad API gratuito:<br/>1. Ir a<https://transparency.entsoe.eu/>--> registrarse y crear una cuenta<br/>2. Envíe un correo electrónico a[transparency@entsoe.eu](mailto:transparency@entsoe.eu)con "Acceso API Restful" en la línea de asunto<br/>3. El servicio de asistencia técnica de ENTSO-E responderá a su solicitud en un plazo de 3 días laborables.<br/>4. Genere un token de seguridad en<https://transparency.entsoe.eu/usrm/user/myAccountSettings> |
| `in_domain`   | Para conocer su clave de dominio de entrada y salida, vaya a:<br/><https://www.entsoe.eu/data/energy-identification-codes-eic/eic-area-codes-map/>                                                                                                                                                                                                                                                                                                                                           |
| `out_domain`  | como`in_domain`                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
| `primary`     | Si este mercado está habilitado este punto lo establece como mercado primario.                                                                                                                                                                                                                                                                                                                                                                                                               |
| `enabled`     | Para utilizar esta entrada debe ser`enabled`. De lo contrario`disabled`                                                                                                                                                                                                                                                                                                                                                                                                                      |

### Tibber

| Configuración | Significado                                                                                                                                                                                                                                                                                                                                                           |
| :------------ | :-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `api_token`   | Para obtener tibber_api_key:<br/>1. inicie sesión con una cuenta Tibber gratuita o de cliente en<https://developer.tibber.com/settings/access-token><br/>2. Cree un token seleccionando los alcances que necesita (seleccione "precio")<br/>3. Utilice este enlace para crear una cuenta gratuita con su teléfono inteligente:<https://tibber.com/de/invite/ojgfbx2e> |
| `price_unit`  | Ajustado a:<br/>"energía" para utilizar los precios del mercado spot (predeterminado),<br/>"total" para utilizar los precios totales, incluidos impuestos y tasas,<br/>"impuesto" para utilizar sólo los impuestos y tasas                                                                                                                                            |
| `primary`     | Si este mercado está habilitado este punto lo establece como mercado primario.                                                                                                                                                                                                                                                                                        |
| `enabled`     | Para utilizar esta entrada debe ser`enabled`. De lo contrario`disabled`                                                                                                                                                                                                                                                                                               |

## Paneles fotovoltaicos

| Configuración | Significado                                                                               |
| :------------ | :---------------------------------------------------------------------------------------- |
| `LocLat`      | Latitud                                                                                   |
| `LocLon`      | Longitud                                                                                  |
| `angle`       | Ángulo de sus paneles 0 (horizontal) … 90 (vertical)                                      |
| `direction`   | Azimut del plano, -180 … 180 (-180 = norte, -90 = este, 0 = sur, 90 = oeste, 180 = norte) |
| `totPower`    | Potencia de los módulos instalados en kilovatios.                                         |
| `enabled`     | Para utilizar esta entrada debe ser`enabled`. De lo contrario`disabled`                   |

* * *

## niveles de registro

### `ERROR`

El`ERROR`El nivel de registro indica condiciones de error dentro de una aplicación que dificultan la ejecución de una operación específica. Si bien la aplicación puede continuar funcionando a un nivel reducido de funcionalidad o rendimiento,<br/>`ERROR`Los registros indican problemas que deben investigarse con prontitud.

### `WARN`

Eventos registrados en el`WARN`El nivel suele indicar que ha ocurrido algo inesperado.
ocurrió, pero la aplicación puede continuar funcionando normalmente por el momento.
También se utiliza para indicar condiciones que deben abordarse rápidamente antes de que ocurran.
convertirse en problemas para la aplicación.

### `INFO`

El`INFO`El nivel captura eventos en el sistema que son importantes para el
propósito comercial de la aplicación. Estos eventos se registran para mostrar que el sistema está
funcionando normalmente. Los sistemas de producción normalmente registran de forma predeterminada en este nivel.
para que cualquier persona pueda ver un resumen del comportamiento normal de la aplicación
 revisando los registros.

### `DEBUG`

El`DEBUG`El nivel se utiliza para registrar mensajes que ayudan a los desarrolladores a identificar
problemas durante una sesión de depuración. El contenido de los mensajes registrados en DEBUG.
El nivel variará dependiendo de su aplicación, pero normalmente contienen
información detallada que ayuda a sus desarrolladores a solucionar problemas
eficientemente. Esto puede incluir el estado de las variables dentro del alcance circundante o
códigos de error relevantes. |

## Inspiración

La idea está inspirada en el proyecto @christian1980nrw vinculado a continuación. Este es mi primer proyecto con Victron Venus OS, por lo que adopté algunas ideas y enfoques de los siguientes proyectos. El enfoque es el mismo y para sistemas muy limitados probablemente sea mejor la implementación con un script bash.

##### – muchas gracias por transmitir el conocimiento:

-   [Conmutador de mercado al contado](https://github.com/christian1980nrw/Spotmarket-Switcher)
-   [dinámica](https://github.com/tfranssen/dynamic-ess)
