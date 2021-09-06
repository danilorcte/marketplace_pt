# API para Marketplaces | ANYMARKET


Bem vindo a documentação da API ANYMARKET para Marketplaces.

Esta documentação tem como objetivo orientar as regras e comportamentos esperados na construção do middleware responsável pela integração das informações entre o ANYMARKET e MARKETPLACE.

<!--
focus: false
-->
![image.png](https://stoplight.io/api/v1/projects/cHJqOjgzMDA1/images/9WruoSt9JOQ)

O responsável pela integração deve construir um middleware seguindo os padrões estabelecidos nos “remotes”, que serão os caminhos que o ANYMARKET irá enviar as chamadas para completar as ações que o seller realizar. Em conjunto com as notificações que o ANYMARKET encaminhará para o middleware, o mesmo precisará interpretar as chamadas e realizar as devidas ações, podendo ser processamentos internos do próprio marketplace ou chamadas para a nossa API afim de inserir informações, atualizar ou consumir dados pertinentes a ação que está sendo executada.

Para o início do desenvolvimento da integração, deverá ser preenchido o formulário para liberação do Marketplace. Este formulário é enviado para a equipe de desenvolvimento que disponibiliza o novo marketplace dentro do ANYMARKET. Nesse momento, serão enviados para você um usuário do ANYMARKET para que você realize os testes do seu desenvolvimento e o appId, que é o identificador do seu marketplace dento do ANYMARKET.
Este id deverá ser utilizado em todas as chamadas que você realizar para nossa API.

A aplicação será divida em duas etapas de operações que vamos nomear de: "Remotes" e "Endpoints" que serão explicados mais adiante na documentação.

Para inicio, precisamos entender como a integração ira funcionar. Como dito na introdução, será encaminhado para vocês um formulário que deve ser preenchido com as URL's do middleware a ser implementado para comunicação com o ANYMARKET. Para liberação será necessário 3 URL's, que serão elas:


1- TELA DO MODULO

2- URL BASE MIDDLEWARE


Remotes
Os Remotes serão os "caminhos" que sua API deve conter. A API ANYMARKET funcionará como um sistema de notificações aonde já temos os remotes prontos que serão disparados na URL base da API que vocês nos informaram no preenchimento do documento de liberação.

Abaixo contem os remotes de cadas uma das aplicações que o marketplace deve realizar com base na regra de negocio previamente formalizada na PGP.


## Como a integração funciona

Para padronizar o comportamento e experíencia para os sellers:

<!--
focus: false
-->
![NovaAPIMarketplace2.png](https://stoplight.io/api/v1/projects/cHJqOjgzMDA1/images/aOVLFjR1HPs)



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


<!-- theme: info -->

## Ambientes
>
> **Sandbox:** http://sandbox-api.anymarket.com.br/marketplace/api
>
> **Produção:** https://api.anymarket.com.br/marketplace/api



## Etapas

1. Formulario de liberaçaõ de marketplace.
2. Liberação de Ambiente Sandbox + appId (Este id deverá ser utilizado em todas as chamadas que você realizar para nossa API.)
3. Construção do Middleware
4. Homologação
5. Beta
6. Produção




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

