![Logo](views/static/images/logo-seuss.png?raw=true "SEUSS")

# SEUSS

#### [SEUSS -> Comutador Spotmarket de unidade Smart Ess]

# Configurações

## Em geral

| Contexto        | Significado                                                                                                                                    |
| --------------- | ---------------------------------------------------------------------------------------------------------------------------------------------- |
| `time_zone`     | Essencial para o timing correto das operações com base na sua localização geográfica.<br/>Formatar como`Europe/Vienna`,`Europe/Amsterdam`, ... |
| `log_file_path` | Define um caminho alternativo no qual os arquivos de log serão salvos.                                                                         |
| `log_level`     | Os níveis de log usados ​​são: INFO, WARNING, ERROR e DEBUG. ver[Níveis de registro](#loglevels)                                               |

## Preços

| Contexto                                   | Significado                                                                                                                                                                                                                                                                          |
| ------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `use_second_day`                           | ativar/desativar a comparação dos preços de hoje e de amanhã, caso estejam disponíveis<br/>Nota: Se você ativar esta opção e os preços diminuírem ao longo de vários dias, é possível que não haja cobrança ou troca por vários dias até que os preços mais baixos sejam alcançados. |
| `number_of_lowest_prices_for_charging`     | o número de preços mais baratos pelos quais o carregamento deve/pode ser feito                                                                                                                                                                                                       |
| `number_of_highest_prices_for_discharging` | o número dos preços mais caros pelos quais a descarga deve/pode ser realizada                                                                                                                                                                                                        |
| `charging_price_limit`                     | o carregamento está sempre ativado abaixo deste preço<br/>o número dos preços mais caros pelos quais a descarga deve/pode ser realizada                                                                                                                                              |

## Unidades ESS

### Victron

| Contexto     | Significado                                                                                                                                                                                          |
| :----------- | :--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `use_vrm`    | Se este ponto estiver ativado (verdadeiro), é feita uma tentativa de ligação à Victron através do portal VRM.<br/>Isto requer um usuário/senha no portal VRM                                         |
| `ip_address` | O endereço IP local da Victron.<br/>Isto é necessário se "use_vrm" estiver desabilitado (falso).<br/>Caso contrário este campo permanece vazio                                                       |
| `unit_id`    | ID do Portal VRM<br/>pode ser encontrado em Configurações / Portal online VRM / ID do Portal VRM.<br/>Nota: Este ID é necessário para aceder à Victron mesmo que não esteja a utilizar um portal VRM |
| `user`       | endereço de e-mail que você usa para se conectar ao portal VRM                                                                                                                                       |
| `password`   | senha que você usa para se conectar ao portal VRM                                                                                                                                                    |

## Mercados

### responder

| Contexto  | Significado                                                                     |
| :-------- | :------------------------------------------------------------------------------ |
| `country` | Escolha a localização AT ou DE                                                  |
| `primary` | Se este mercado estiver habilitado, este ponto o define como o mercado primário |
| `enabled` | defina seu mercado como ativado/desativado                                      |

### Enzo é

| Contexto     | Significado                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| :----------- | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `api_token`  | Como obter o token de segurança da API gratuito:<br/>1. Vá para<https://transparency.entsoe.eu/>-> cadastre-se e crie uma conta<br/>2. Envie um e-mail para[transparency@entsoe.eu](mailto:transparency@entsoe.eu)com “Acesso Restful à API” na linha de assunto<br/>3. O Helpdesk da ENTSO-E responderá ao seu pedido no prazo de 3 dias úteis.<br/>4. Gere um token de segurança em<https://transparency.entsoe.eu/usrm/user/myAccountSettings> |
| `in_domain`  | Para descobrir sua chave de domínio de entrada e saída, acesse:<br/><https://www.entsoe.eu/data/energy-identification-codes-eic/eic-area-codes-map/>                                                                                                                                                                                                                                                                                              |
| `out_domain` | como in_domain                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| `primary`    | Se este mercado estiver habilitado, este ponto o define como o mercado primário                                                                                                                                                                                                                                                                                                                                                                   |
| `enabled`    | defina seu mercado como ativado/desativado                                                                                                                                                                                                                                                                                                                                                                                                        |

### Tiber

| Contexto     | Significado                                                                                                                                                                                                                                                                                                                                  |
| :----------- | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `api_token`  | Para obter o tibber_api_key:<br/>1. faça login com uma conta Tibber gratuita ou de cliente em<https://developer.tibber.com/settings/access-token><br/>2. Crie um token selecionando os escopos necessários (selecione "preço")<br/>3. Use este link para criar uma conta gratuita com seu smartphone:<https://tibber.com/de/invite/ojgfbx2e> |
| `price_unit` | Definido como:<br/>"energia" para usar os preços do mercado spot (padrão),<br/>"total" para usar os preços totais incluindo impostos e taxas,<br/>"imposto" para usar apenas os impostos e taxas                                                                                                                                             |
| `primary`    | Se este mercado estiver habilitado, este ponto o define como o mercado primário                                                                                                                                                                                                                                                              |
| `enabled`    | defina seu mercado como ativado/desativado                                                                                                                                                                                                                                                                                                   |

* * *

# Níveis de registro

### `ERROR`

O`ERROR`nível de log indica condições de erro dentro de um aplicativo que dificultam a execução de uma operação específica. Embora o aplicativo possa continuar funcionando com um nível reduzido de funcionalidade ou desempenho,<br/>`ERROR`logs significam problemas que devem ser investigados imediatamente.

### `WARN`

Eventos registrados no`WARN`nível normalmente indicam que algo inesperado aconteceu
ocorreu, mas o aplicativo pode continuar funcionando normalmente por enquanto.
Também é usado para significar condições que devem ser prontamente tratadas antes de ocorrerem.
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
