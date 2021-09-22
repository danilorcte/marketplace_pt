# API para Marketplaces | ANYMARKET


Bem vindo a documentação da API ANYMARKET para Marketplaces.

Esta documentação tem como objetivo orientar as regras e comportamentos esperados na construção do middleware responsável pela integração das informações entre o ANYMARKET e MARKETPLACE.

<!--
focus: false
-->
![image.png](https://stoplight.io/api/v1/projects/cHJqOjgzMDA1/images/9WruoSt9JOQ)

O responsável pela integração deve construir uma aplicação **Middleware** seguindo os padrões de endpoints estabelecidos no tópico de **“remotes”**. Estes remotes serão os caminhos que o ANYMARKET irá enviar as notificações ou consultas para completar as ações que o seller realizar. 

```json title="Exemplo de URLs do Middleware que serão notificadas"
{{URL_MIDDLEWARE}}\sendproduct
{{URL_MIDDLEWARE}}\brands
```

Após receber as notificações e consultas que o ANYMARKET encaminhará para o middleware, o mesmo precisará interpretar as chamadas e realizar as devidas ações para completar as solicitações do Seller, podendo ser processamentos internos do próprio marketplace ou chamadas para a API ANYMARKET afim de inserir informações, atualizar ou consumir dados pertinentes a ação que está sendo executada.

A aplicação **Middleware** será divida em duas etapas de operações que vamos nomear de:

> #### REMOTES
> Os remotes serão os "caminhos" que sua API deve conter. A API ANYMARKET funcionará como um sistema de notificações aonde já temos os remotes prontos que serão disparados na URL base da API que vocês nos informaram no preenchimento do documento de liberação.

---

> #### API ANYMARKET
> Conjunto de APIs do ANYMARKET que permitem ao middleware inserir informações, atualizar ou consumir dados pertinentes a ação que está sendo executada.


Na imagem abaixo temos de forma macro as informações que serão trafegadas através do middleware:

<!--
focus: false
-->
![image.png](https://stoplight.io/api/v1/projects/cHJqOjgzMDA1/images/QNhsD4Yn164)

>No tópico **"Remotes do Middleware"** da nossa documentação, existem mais informações sobre cada notificação ou consulta que o ANYMARKET realiza no middleware, qual ação o seller está solicitando e os comportamentos esperados para cada ação, visando garantir a melhor experiência ao Seller.

## Etapas da integração

|#|Etapa|Responsável|Descrição|
|-|--------------------------------------------------------------|----|-|
|1|Prenchimento do "Formulário de liberação de novo marketplace"|Marketplace|Neste formulário constam informações como URL do Middleware, campos necessários para autenticação no marketplace (login/senha ou token), descrição, comportamentos)|
|2|Liberação de Ambiente Sandbox                                 |ANYMARKET|Nesta etapa o ANYMARKET criará o novo canal com base nas informações do formulário da etapa anterior e fornecerá: **Usuário de acesso ao ANYMARKET** para que você realize os testes durante o desenvolvimento. E também o seu **"appId"** que será o identificador do seu marketplace dento do ANYMARKET, este id deverá ser utilizado em todas as chamadas que você realizar para nossa API.|
|3|Construção do Middleware                                      |Marketplace|Etapa de contrução do middleware pelo marketplace.|
|4|Homologação                                                   |ANYMARKET|Nesta etapa nossa equipe de qualidade irá realizar os testes do novo marketplace visando garantir que a integração está de acordo com os critérios de aceitação previstos. Mais informações sobre esse processo podem ser acessadas no tópico **"Processo de homologação"** da nossa documentação.|
|5|Liberação do marketplace em Beta                              |ANYMARKET|Nesta etapa acompanhamos os 5 primeiros sellers, visando garantir que está tudo funcionando corretamente em ambiente de produção.|
|6|Liberação do marketplace em Produção                          |ANYMARKET|Disponibilizamos o novo marketplace para todos os Sellers do ANYMARKET.|



## Como a integração funciona

Para facilitar a compreensão de como o **Middleware** deve funcionar, seguem abaixo a relação dos **Remotes** que o middleware precisa disponibilizar e seus objetivos, as **APIs do ANYMARKET** disponíveis para o middleware completar as ações dos processos, além do desenho do fluxo de como o middleware se comunica com o ANYMARKET e Marketplace:

### Remotes

|               |                                     |               ||
| ------------- | --- |--------------------------------- | ------------- |
| POST   |/testIntegration | obrigatório | Nesta notificação enviamos os dados de autenticação no marketplace configurados pelo Seller, para que o middleware valide o acesso.|
| POST   |/saveAccount | obrigatório | Nesta notificação enviamos os dados da configuração informados pelo Seller caso o middleware queira armazena.   |
| GET    |/product/{{partnerId}} | obrigatório | Esta consulta serve para obtermos os anúncios do marketplace, para vincularmos com as transmissões do ANYMARKET. |
| GET    |/brands | opcional | Esta consulta serve para obtermos as marcas do marketplace e vincularmos com as marcas do ANYMARKET.  |
| GET    |/categories| opcional | Esta consulta serve para obtermos as categorias do marketplace e vincularmos com as categorias do ANYMARKET.  |
| GET    |/categories/details/{{id}} | opcional | Esta consulta serve para obtermos as categorias filhas do marketplace e vincularmos com as categorias do ANYMARKET.   |
| GET    |/categories/attributes/{{id}} | opcional | Esta consulta serve para obtermos os atributos do marketplace e vincularmos com os produtos do ANYMARKET.  |
| GET    |/variations/types | opcional | Esta consulta serve para obtermos as variações do marketplace e vincularmos com as variações do ANYMARKET.   |
| POST   |/canActive | opcional | Nesta notificação enviamos uma prévia dos dados do produto/sku para que o middleware possa validar se o mesmo pode ser publicado no marketplace. (Ação disparada quando o seller acessa a funcionalidade "Nova Publicação")   |
| GET    |/getDefaultSkuFields | opcional | Esta consulta serve para que o marketplace informe campos adicionais para que o seller preencha ao incluir uma "Nova Publicação" |
| POST   |/canSave | obrigatório | Nesta notificação enviamos uma prévia dos dados do anúncio para que o middleware possa validar se o mesmo pode ser publicado no marketplace. (Ação disparada quando o seller grava uma "Nova Publicação").  |
| POST   |/sendProduct | obrigatório | Nesta notificação enviamos todas as alterações realizadas em um anúncio: Nova Publicação, Alterações do cadasto do anúncio, Alterações de estoque, Alterações de preço, Pausar um anúncio, Finalizar um anúncio e Reenviar um anúncio. |
| DELETE |/deletePublication | obrigatório | Esta notificação será disparada quando uma transmissão for excluída do painel do ANYMARKET, para que oo marketplace inative o anúncio. |
| POST   |/order/force/{{id}} | obrigatório | Enviaremos essa notificação sempre que o seller solicitar o reenvio do pedido do marketplace para o ANYMARKET (Monitoring)  |
| POST   |/forceImportOrders | obrigatório | Enviaremos essa notificação quando o seller solicitar a importação de todos os pedidos para o painel do ANYMARKET (Tela de Configuração).|
| GET    |/order/{{id}} | obrigatório | Esta consulta serve para consultarmos informações do pedido do marketplace.   |
| PUT    |/updateOrderStatusInMarketplace | obrigatório |Esta notificação é enviada sempre que há uma alteração no pedido no ANYMARKET, para que o middleware consulte as informações atualizadas do pedido e replique ao marketplace. |


### APIs ANYMARKET

|               |                                     |               ||
| ------------- | --- |--------------------------------- | ------------- |
| GET   |/api/configuration | opcional | Consulta todas as configurações realizadas pelo seller no ANYMARKET. |
| GET   |/api/configuration/{id} | opcional | Consulta  pelo ID da conta as configurações realizadas pelo seller no ANYMARKET.  |
| GET   |/skumarketplace/{id} | obrigatório | Consulta os dados do anúncio no ANYMARKET.   |
| PUT   |/skumarketplace/{id} | obrigatório | Utilizado para que o middleware marque o anúncio como atualizado.   |
| POST  |/orders | obrigatório | Utilizado para que o middleware grave o pedido no ANYMARKET.|
| PUT   |/orders/{id}/markAsPaid | obrigatório | Utilizado para que o middleware marque o pedido como PAGO no ANYMARKET.  |
| PUT   |/orders/{id}/markAsCanceled | obrigatório | Utilizado para que o middleware marque o pedido como CANCELADO no ANYMARKET.  |
| PUT   |/orders/{id}/markAsShipped | opcional | Utilizado para que o middleware marque o pedido como ENVIADO no ANYMARKET.   |
| PUT   |/orders/{id}/markAsDelivered | opcional | Utilizado para que o middleware marque o pedido como ENTREGUE no ANYMARKET.  |
| GET   |/orders/{id} | obrigatório | Permite o middlewar consulta os dados do pedido no ANYMARKET.  |
| PUT   |/orders/{id}/transmissionStatus | obrigatório | Utilizado para que o middleware marque o pedido como atualizado.    |

### Fluxo

Legenda |          |
--------|----------|
LARANJA | Ações realizadas pelo Seller no painel do ANYMARKET |
VERDE   | Remotes que serão notificados ou consultados no MIDDLEWARE |
AMARELO | APIs do ANYMARKET que serão utilizadas nos processos |
AZUL    | Processamento que o ANYMARKET/MIDDLEWARE deve realizar após as notificações |


<!--
focus: false
-->
![NovaAPIMarketplace7.png](https://stoplight.io/api/v1/projects/cHJqOjgzMDA1/images/tl6o14hZH4g)











<!-- theme: info -->

## Ambientes
>
> **Sandbox:** http://sandbox-api.anymarket.com.br/marketplace/api
>
> **Produção:** https://api.anymarket.com.br/marketplace/api




## Informações úteis


> #### Operações
> Nós fazemos o nosso melhor para que todas as nossas URLs sejam RESTful. Cada URL pode suportar um dos quatro diferentes tipos de verbos HTTP:
>
> |               |                                     |   
> | ------------- | ---------------------------------   | 
> | GET           | obtém informações sobre um recurso  |
> | POST          | cria um recurso                     | 
> | PUT           | atualiza um recurso                 | 
> | DELETE        | exclui um recurso                   | 

---

<!-- theme: danger -->

> #### Limites de consumo
>
> Seja legal. Se você estiver enviando muitas requisições rapidamente, nós retornaremos um código de erro 429 (too many requests). 
>
>Você tem um limite de 10 requisições por segundo por token
>

---

> #### Dúvidas, sugestões e feedbacks podem ser encaminhados por e-mail para:
>
> api@anymarket.com.br.

