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


> #### API ANYMARKET
> Conjunto de APIs do ANYMARKET que permitem ao middleware inserir informações, atualizar ou consumir dados pertinentes a ação que está sendo executada.


Na imagem abaixo temos de forma macro as informações que serão trafegadas através do middleware:

<!--
focus: false
-->
![image.png](https://stoplight.io/api/v1/projects/cHJqOjgzMDA1/images/QNhsD4Yn164)

>No tópico **"Remotes do Middleware"** da nossa documentação, existem mais informações sobre cada notificação ou consulta que o ANYMARKET realiza no middleware, qual ação o seller está solicitando e os comportamentos esperados para cada ação, visando garantir a melhor experiência ao Seller.

## Etapas

|#|Etapa|Responsável|Descrição|
|-|--------------------------------------------------------------|----|-|
|1|Prenchimento do "Formulário de liberação de novo marketplace" ||Marketplace|Neste formulário constam informações como URL do Middleware, campos necessários para autenticação no marketplace (login/senha ou token), descrição, comportamentos)|
|2|Liberação de Ambiente Sandbox                                 |ANYMARKET|Nesta etapa o ANYMARKET criará o novo canal com base nas informações do formulário da etapa anterior e fornecerá: **Usuário de acesso ao ANYMARKET** para que você realize os testes durante o desenvolvimento. E também o seu **"appId"** que será o identificador do seu marketplace dento do ANYMARKET, este id deverá ser utilizado em todas as chamadas que você realizar para nossa API.|
|3|Construção do Middleware                                      |Marketplace|Etapa de contrução do middleware pelo marketplace.|
|4|Homologação                                                   |ANYMARKET|Nesta etapa nossa equipe de qualidade irá realizar os testes do novo marketplace visando garantir que a integração está de acordo com os critérios de aceitação previstos. Mais informações sobre esse processo podem ser acessadas no tópico **"Processo de homologação"** da nossa documentação.|
|5|Liberação do marketplace em Beta                              |ANYMARKET|Nesta etapa acompanhamos os 5 primeiros sellers, visando garantir que está tudo funcionando corretamente em ambiente de produção.|
|6|Liberação do marketplace em Produção                          |ANYMARKET|Disponibilizamos o novo marketplace para todos os Sellers do ANYMARKET.|



## Como a integração funciona

Para padronizar o comportamento e experíencia para os sellers:

Remotes

|               |                                     |               ||
| ------------- | --- |--------------------------------- | ------------- |
| POST   |[/testIntegration](./docs/remotes/testintegration.md) | Explicar para que serve  | obrigatório |
| POST   |/saveAccount | Explicar para que serve  | obrigatório |
| GET    |/product/123?idAccount=123&definitionScope=COST  | Explicar para que serve  | obrigatório |
| GET    |/brands | Explicar para que serve  | opcional |
| GET    |/categories | Explicar para que serve  | opcional |
| GET    |/categories/details/{{codeInMarketplace}} | Explicar para que serve  | opcional |
| GET    |/categories/attributes/{{idAnymarketCategory}} | Explicar para que serve  | opcional |
| GET    |/variations/types | Explicar para que serve  | opcional |
| POST   |/canActive | Explicar para que serve  | opcional |
| GET    |/getDefaultSkuFields | Explicar para que serve  | opcional |
| POST   |/canSave | Explicar para que serve  | obrigatório |
| POST   |/sendProduct | Explicar para que serve  | obrigatório |
| DELETE |/deletePublication | Explicar para que serve  | obrigatório |
| POST   |/order/force/{orderIdInMarketPlace} | Explicar para que serve  | obrigatório |
| POST   |/forceImportOrders | Explicar para que serve  | obrigatório |
| GET   |/order/(orderIdInMarketPlace) | Explicar para que serve  | obrigatório |
| PUT   |/updateOrderStatusInMarketplace | Explicar para que serve  | obrigatório |


APIs ANYMARKET

|               |                                     |               ||
| ------------- | --- |--------------------------------- | ------------- |
| GET   |/api/configuration | Explicar para que serve  | opcional |
| GET   |/api/configuration/{id} | Explicar para que serve  | opcional |
| GET   |/skumarketplace/{id} | Explicar para que serve  | obrigatório |
| PUT   |/skumarketplace/{id} | Explicar para que serve  | obrigatório |
| POST  |/orders | Explicar para que serve  | obrigatório |
| PUT   |/orders/{id}/markAsPaid | Explicar para que serve  | obrigatório |
| PUT   |/orders/{id}/markAsCanceled | Explicar para que serve  | obrigatório |
| PUT   |/orders/{id}/markAsShipped | Explicar para que serve  | opcional |
| PUT   |/orders/{id}/markAsDelivered | Explicar para que serve  | opcional |
| GET   |/orders/{id} | Explicar para que serve  | obrigatório |
| PUT   |/orders/{id}/transmissionStatus | Explicar para que serve  | obrigatório |

## Fluxo

Legenda |          |
--------|----------|
LARANJA | Ações realizadas pelo Seller no ANYMARKET |
VERDE   | Remotes que serão notificados no MIDDLEWARE |
AMARELO | APIs do ANYMARKET que serão utilizadas nos processos |
AZUL    | Processamento que o ANYMARKET/MIDDLEWARE deve realizar após as notificações |


<!--
focus: false
-->
![NovaAPIMarketplace6.png](https://stoplight.io/api/v1/projects/cHJqOjgzMDA1/images/knfnyuV3Qdo)










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

