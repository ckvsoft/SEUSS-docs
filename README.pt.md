![Logo](views/static/images/logo-seuss.png?raw=true "SEUSS")

# SEUSS

### [SEUSS -> Comutador Spotmarket de unidade Smart Ess]

#### Por favor, relate os bugs e sugira melhorias. Obrigado a todos que já participaram.

###### Se você gostaria de contribuir com extensões para isso, envie a solicitação pull no branch dev. Para correções de bugs, o pull request também pode ser feito no branch principal

### O que este software faz?

Este é um aplicativo Python 3 que liga sua unidade ESS (controlador) no momento certo quando os preços dinâmicos de energia por hora estão baixos. Ou usado para descarregar quando os preços são extremamente altos.

#### Os sistemas atualmente suportados são:

### Unidades ESS

* * *

-   **_Sistemas de armazenamento de energia Victron Venus OS, como a série MultiPlus II_**

* * *

### Mercados à Vista

* * *

-   **_responder_**
-   **_Enzo-E_**
-   **_Tiber_**

* * *

O controle da unidade ESS (controlador) é feito via mqtt. A vantagem deste controle é:
que este aplicativo não precisa ser executado diretamente no VenusOS. O controle direto com D-BUS está em andamento

# Testado

Esta versão fez sucesso com

* * *

-   **_Linux Ubuntu >= 22.04_**
-   **_Venus OS Raspberry >= v3.12_**

* * *

testado

# Instalar

Baixe o script de instalação do repositório GitHub e execute o seguinte comando em seu terminal:

    wget -O seuss_install.sh https://raw.githubusercontent.com/ckvsoft/SEUSS/dev/scripts/seuss_install.sh`

Execute o script do instalador com opções adicionais para preparar tudo em um subdiretório para sua inspeção. Por exemplo:

    bash seuss_install.sh`

O diretório padrão é /data/seuss (Venus OS). Mas você pode opcionalmente especificar um diretório diferente usando a variável de ambiente TARGET_DIRECTORY, por exemplo.

    TARGET_DIRECTORY=/opt/seuss bash seuss_install.sh`

Em um Cerbo GX o sistema de arquivos é montado somente leitura. Ver<https://www.victronenergy.com/live/ccgx:root_access>.
Para tornar o sistema de arquivos gravável, você precisa executar o seguinte comando antes de executar o script de instalação:

    /opt/victronenergy/swupdate-scripts/resize2fs.sh

# Configuração

Depois`SEUSS`foi instalado com sucesso, um site está disponível no endereço IP e na porta 5000 do`Computer/VenusOS`em que`SEUSS`foi instalado.

-   Você pode visualizar ou baixar o arquivo de log.
-   Além disso, a configuração pode ser realizada usando o[Editor de configuração]item do menu.
-   Dicas de ferramentas para a maioria dos pontos são exibidas aqui.

#### Visualizador de registro

-   ![Logo](views/static/images/logviewer.png?raw=true "SEUSS Log Viewer")

#### Editor de configuração - Unidades ESS

-   ![Logo](views/static/images/configeditor_ess.png?raw=true "SEUSS Config Editor")

#### Editor de configuração - Painéis fotovoltaicos

-   ![Logo](views/static/images/configeditor_panels.png?raw=true "SEUSS Config Editor")

Eles também podem ser encontrados na descrição das configurações.
Para quem prefere trabalhar em um arquivo de configuração, existe o config.json

# Configurações

## Em geral

| Contexto        | Significado                                                                                                                                    |
| --------------- | ---------------------------------------------------------------------------------------------------------------------------------------------- |
| `time_zone`     | Essencial para o timing correto das operações com base na sua localização geográfica.<br/>Formatar como`Europe/Vienna`,`Europe/Amsterdam`, ... |
| `log_file_path` | Define um caminho alternativo no qual os arquivos de log serão salvos.                                                                         |
| `log_level`     | Os níveis de log usados ​​são:`INFO`,`WARNING`,`ERROR`e`DEBUG`. ver[Níveis de registro](#loglevels)                                            |

## Preços

#### Por favor, altere os preços (use sempre Cent/kWh, não importa se você está usando Awattar (exibindo Cent/kWh) ou Entsoe API (exibindo EUR/MWh) / preços líquidos sem impostos).

| Contexto                                   | Significado                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| ------------------------------------------ | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `use_second_day`                           | `enable/disable`para comparar os preços de hoje e de amanhã, se estiverem disponíveis<br/>Nota: Se você ativar esta opção e os preços diminuírem ao longo de vários dias, é possível que não haja cobrança ou troca por vários dias até que os preços mais baixos sejam alcançados.                                                                                                                                                                                                                                                                                   |
| `number_of_lowest_prices_for_charging`     | Dois modos podem ser usados ​​aqui.<br/>modo1:<br/>_o número de preços mais baratos pelos quais a cobrança deve/pode ocorrer. Aqui você insere números inteiros<br/>modo2:<br/>_Aqui o número de preços é determinado com base no preço médio. Para este modo você insere números decimais. Por exemplo. 0,85 para receber todos os preços que estão 85% abaixo da média. O que é relevante aqui é a especificação de um valor de vírgula. Com 1,0 assume-se que 100% do preço médio é considerado (não faz sentido), mas se for inserido 1, será o preço mais barato |
| `number_of_highest_prices_for_discharging` | Dois modos podem ser usados ​​aqui.<br/>modo1:<br/>_o número de preços mais caros pelos quais a descarga deve/pode ocorrer. Aqui você insere números inteiros<br/>modo2:<br/>_Aqui o número de preços é determinado com base no preço médio. Para este modo você insere números decimais. Por exemplo. 1,25 para receber todos os preços 25% acima da média.<br/>O que é relevante aqui é a especificação de um valor de vírgula. Com 1,0 assume-se que 100% do preço médio é considerado (não faz sentido), mas se for inserido 1, será o preço mais caro            |
| `charging_price_limit`                     | o carregamento está sempre ativado abaixo deste preço<br/>o número dos preços mais caros pelos quais a descarga deve/pode ser realizada                                                                                                                                                                                                                                                                                                                                                                                                                               |

## Unidades ESS

### Victron

| Contexto              | Significado                                                                                                                                                                                                                                                                                                                                                                                                                         |
| :-------------------- | :---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `use_vrm`             | Se este ponto estiver ativado (verdadeiro), é feita uma tentativa de ligação à Victron através do portal VRM.<br/>Isto requer um usuário/senha no portal VRM                                                                                                                                                                                                                                                                        |
| `ip_address`          | O endereço IP local da Victron.<br/>Isto é necessário se`use_vrm`está desabilitado (falso).<br/>Caso contrário este campo permanece vazio                                                                                                                                                                                                                                                                                           |
| `unit_id`             | ID do Portal VRM<br/>pode ser encontrado no`Settings / VRM online portal / VRM Portal Id`.<br/>Nota: Este ID é necessário para aceder à Victron mesmo que não esteja a utilizar um portal VRM                                                                                                                                                                                                                                       |
| `user`                | endereço de e-mail que você usa para se conectar ao portal VRM                                                                                                                                                                                                                                                                                                                                                                      |
| `password`            | senha que você usa para se conectar ao portal VRM                                                                                                                                                                                                                                                                                                                                                                                   |
| `max_discharge_power` | Padrão: -1<br/>Se você usar`Limit inverter power`no menu ESS então este valor deve ser inserido aqui.<br/>Se o inversor estiver configurado para`Discharge false`por este aplicativo, esse valor será substituído no ESS.<br/>Este limite aqui é definido no modo de descarga no ESS.<br/>Se nenhum limite for definido, deixe o valor em`-1`.<br/>Exemplo: Entrar`1000`limitar a descarga a`1000W`, Digitar`-1`para potência total |
| `only_observation`    | Se`only observation`estiver ativado, o essunit será usado apenas para fins estatísticos. A essunit não executa nenhuma condição                                                                                                                                                                                                                                                                                                     |
| `enabled`             | Para usar esta entrada deve ser`enabled`. De outra forma`disabled`                                                                                                                                                                                                                                                                                                                                                                  |

## Mercados à Vista

### responder

| Contexto  | Significado                                                                     |
| :-------- | :------------------------------------------------------------------------------ |
| `country` | Escolha a localização AT ou DE                                                  |
| `primary` | Se este mercado estiver habilitado, este ponto o define como o mercado primário |
| `enabled` | Para usar esta entrada deve ser`enabled`. De outra forma`disabled`              |

### Enzo é

| Contexto     | Significado                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| :----------- | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `api_token`  | Como obter o token de segurança da API gratuito:<br/>1. Vá para<https://transparency.entsoe.eu/>-> cadastre-se e crie uma conta<br/>2. Envie um e-mail para[transparency@entsoe.eu](mailto:transparency@entsoe.eu)com “Acesso Restful à API” na linha de assunto<br/>3. O Helpdesk da ENTSO-E responderá ao seu pedido no prazo de 3 dias úteis.<br/>4. Gere um token de segurança em<https://transparency.entsoe.eu/usrm/user/myAccountSettings> |
| `in_domain`  | Para descobrir sua chave de domínio de entrada e saída, acesse:<br/><https://www.entsoe.eu/data/energy-identification-codes-eic/eic-area-codes-map/>                                                                                                                                                                                                                                                                                              |
| `out_domain` | como`in_domain`                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| `primary`    | Se este mercado estiver habilitado, este ponto o define como o mercado primário                                                                                                                                                                                                                                                                                                                                                                   |
| `enabled`    | Para usar esta entrada deve ser`enabled`. De outra forma`disabled`                                                                                                                                                                                                                                                                                                                                                                                |

### Tiber

| Contexto     | Significado                                                                                                                                                                                                                                                                                                                                  |
| :----------- | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `api_token`  | Para obter o tibber_api_key:<br/>1. faça login com uma conta Tibber gratuita ou de cliente em<https://developer.tibber.com/settings/access-token><br/>2. Crie um token selecionando os escopos necessários (selecione "preço")<br/>3. Use este link para criar uma conta gratuita com seu smartphone:<https://tibber.com/de/invite/ojgfbx2e> |
| `price_unit` | Definido como:<br/>"energia" para usar os preços do mercado spot (padrão),<br/>"total" para usar os preços totais, incluindo impostos e taxas,<br/>"imposto" para usar apenas os impostos e taxas                                                                                                                                            |
| `primary`    | Se este mercado estiver habilitado, este ponto o define como o mercado primário                                                                                                                                                                                                                                                              |
| `enabled`    | Para usar esta entrada deve ser`enabled`. De outra forma`disabled`                                                                                                                                                                                                                                                                           |

## Painéis fotovoltaicos

| Contexto          | Significado                                                                                 |
| :---------------- | :------------------------------------------------------------------------------------------ |
| `locLat`          | Latitude                                                                                    |
| `locLong`         | Longitude                                                                                   |
| `angle`           | Ângulo dos seus painéis 0 (horizontal)… 90 (vertical)                                       |
| `direction`       | Azimute do plano, -180… 180 (-180 = norte, -90 = leste, 0 = sul, 90 = oeste, 180 = norte)   |
| `totPower`        | potência dos módulos instalados em quilo watt                                               |
| `total_area`      | Área total dos painéis em metros quadrados                                                  |
| `damping_morning` | Com este parâmetro você pode ajustar o resultado pela manhã. Valor flutuante 0..1, padrão 0 |
| `damping_evening` | Com este parâmetro você pode ajustar o resultado à noite. Valor flutuante 0..1, padrão 0    |
| `enabled`         | Para usar esta entrada deve ser`enabled`. De outra forma`disabled`                          |

* * *

## Níveis de registro

### `ERROR`

O`ERROR`nível de log indica condições de erro dentro de um aplicativo que dificultam a execução de uma operação específica. Embora o aplicativo possa continuar funcionando com um nível reduzido de funcionalidade ou desempenho,<br/>`ERROR`logs significam problemas que devem ser investigados imediatamente.

### `WARN`

Eventos registrados no`WARN`nível normalmente indicam que algo inesperado aconteceu
ocorreu, mas o aplicativo pode continuar funcionando normalmente por enquanto.
Também é usado para indicar condições que devem ser prontamente tratadas antes de ocorrerem.
se transformar em problemas para o aplicativo.

### `INFO`

O`INFO`nível captura eventos no sistema que são significativos para o
finalidade comercial do aplicativo. Tais eventos são registrados para mostrar que o sistema está
operando normalmente. Os sistemas de produção normalmente usam como padrão o registro em log neste nível
para que um resumo do comportamento normal do aplicativo fique visível para qualquer pessoa
 revisando os registros.

### `DEBUG`

O`DEBUG`nível é usado para registrar mensagens que ajudam os desenvolvedores a identificar
problemas durante uma sessão de depuração. O conteúdo das mensagens registradas no DEBUG
nível irá variar dependendo da sua aplicação, mas eles normalmente contêm
informações detalhadas que auxiliam seus desenvolvedores na solução de problemas
eficientemente. Isso pode incluir o estado das variáveis ​​dentro do escopo circundante ou
códigos de erro relevantes. |

## Inspiração

A ideia é inspirada no projeto @christian1980nrw vinculado abaixo. Este projeto é o meu primeiro com o Victron Venus OS, por isso adotei algumas ideias e abordagens dos projetos seguintes. A abordagem é a mesma e para sistemas muito restritos a implementação com um script bash é provavelmente melhor

##### – muito obrigado por repassar o conhecimento:

-   [Alternador de mercado spot](https://github.com/christian1980nrw/Spotmarket-Switcher)
-   [dinâmico](https://github.com/tfranssen/dynamic-ess)
