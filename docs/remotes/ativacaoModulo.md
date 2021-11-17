# Ativação do Módulo de Integração

Um dos primeiros processos que realizamos internamente assim que inicamos um projeto de integração com o Marketplace, é a criação do **Módulo**. Mas o que seria esse Módulo? Neste tópico iremos trazer mais informações sobre essa tela no ANYMARKET e seu funcionamento via API.


### O que é o Módulo de Integração?
No ANYMARKET, o Seller tem acesso a uma tela onde listará todas as integrações com os Marketplaces que temos disponíveis, e será nesse local onde o Seller irá ativar e configurar a integração.

Assim que iniciamos o processo de integração com um novo Marketplace no ANYMARKET, enviamos um formulário e uma das informações que solicitamos é:

- **Quais são os dados fundamentais para autenticar um novo cliente?** 

Essa informação é importante para a construção da tela do Módulo personalizada para cada Marketplace aqui no ANYMARKET, pois será o próprio Marketplace quem vai definir por quais informações irá realizar a autenticação do Seller.

Exemplos de autenticações:
- Token + Senha;
- Id da Loja;
- Usuario e Senha;
- Token + Usuario e Senha;
- Etc;

Essas informações deverão ser passadas para o Seller, para que eles consigam ativar a integração via ANYMARKET. No print de exemplo que disponibilizamos abaixo, o Marketplace irá controlar por Login e Senha, então a tela de autenticação terá o campo Nome da Conta (Campo Padrão para todas as telas de módulo ANYMARKET) e abaixo os campos de autenticação (Login + Senha) que o Marketplace definiu (Campos personalizados).
<!--
focus: false
-->
![image.png](https://stoplight.io/api/v1/projects/cHJqOjgzMDA1/images/1hmZJccVDNo)


### Comportamentos da tela do Módulo
Iremos detalhar nesse tópico como é o funcionamento da tela do módulo, quais os remotes que serão acionados e o retorno e ações esperadas na integração.



(IMAGEM DO FLUXO)

Baseando no fluxo acima, a partir do momento em que o Seller acessa a tela do módulo e insere as informações e clica no botão **SALVAR**, o ANYMARKET irá disparar no remote **/testIntegration** as seguintes informações:

|Headers||
|-------|--|
|**x-anymarket-token** | JWT com as informações para autenticação no middleware. |


Exemplo JWT ANYMARKET:

```` json
eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiJ9.eyJpcCI6IjEwLjAuOS4xNzIiLCJvcmdhbml6YXRpb24iOiJBTllNQVJLRVQgVGVzdGUgLSBCcmFzaWwiLCJvaSI6IjIyNDQ5NTA0LiIsImV4cCI6MTYxMjc5MTI2NCwibG9naW4iOiJkYW5pbG8ub2xpdmVpcmFAZGIxLmNvbS5iciJ9.FKF8wRb97xZmpakGbkoYfO0cjIkj48rwcis4DOGlUEh4cD98sFRJTVfrmMOaAe-XrBoPvTWbSdJfNy81-_VMLq9dbcKpBPO8MfHDXmqWV7tuHT1BaIcOkYZl-uIvOMtxCmDiCrX1ny2DvjY_LLuzRjexM6CQw4rRt8NXZb3dGV4
````

Este JWT contem as seguintes informações:

```` json
"organization" - Nome da empresa
"oi" - Organization ID, identificador único do lojista; Esse campo diferencia os sellers
"exp" - Tempo de expiração do token
"login" - Usuário que está realizando a chamada; Pode ser utilizado para fins de auditoria
````
O middleware deve estar preparado para receber o token, verificar a expiração do mesmo e identificar a assinatura com a chave pública do ANYMARKET.


### Requisição

```json title="POST: \testIntegration" lineNumbers
{
	"id": 10,
	"active": true,
	"templateId": 10,
	"accountName": "accountName",
	"discountType": "PERCENT",
	"useSandbox": true,
	"accountDefault": true,
	"priceFactor": 10.0,
	"discountValue": 5.0,
	"initialDateForOrderImport": "dd-MM-yyyy",
	"updatePriceStockStatus": true,
	"additionOfFreight": 0,
        "user": null,
	"login": "XXXXXXXX",
	"senha": "XXXXXXXX"
}
```

---

```json json_schema
{
  "title": "testIntegration",
  "type": "object",
  "properties": {
    "id": {
      "type": "integer",
      "description": "Id da Conta"
    },
    "active": {
      "type": "boolean",
      "description": "Informa se a conta está Ativa"
    },
    "templateId": {
      "type": "number",
      "description": ""
    },
    "accountName": {
      "type": "string",
      "description": "Nome da Conta inserida pelo Seller"
    },
    "discountType": {
      "type": "string",
      "description": "Tipo de desconto (PERCENT ou VALUE)"
    },
    "useSandbox": {
      "type": "boolean",
      "description": "Se a conta usada é em Sandbox"
    },
    "accountDefault": {
      "type": "boolean",
      "description": "Se é a conta Padrão"
    },
     "priceFactor": {
      "type": "number",
      "description": "Fator de preço multiplicador (MARKUP ADICIONAL)"
    },
    "discountValue": {
      "type": "number",
      "description": "Valor de desconto"
    },
    "initialDateForOrderImport": {
      "type": "string",
      "format": "dd-MM-yyyy",
      "description": "Data inicial de importação dos pedidos."
    },
    "updatePriceStockStatus": {
      "type": "boolean",
      "description": "Define se será permitido somente atualização de Preço, Estoque e Status"
    },
    "additionOfFreight": {
      "type": "integer",
      "description": "Valor adicional em cima da tabela de frete."
    },
    "user": {
      "type": "string",
      "description": "Nesse primeiro momento virá nulo, porem no remote do saveAccount, terá as informações do Token do Seller.."
    },
    "login": {
      "type": "string",
      "description": "CAMPO PERSONALIZADO PARA AUTENTICAÇÃO DO SELLER"
    },
    "senha": {
      "type": "string",
      "description": "CAMPO PERSONALIZADO PARA AUTENTICAÇÃO DO SELLER"
    }
  }
}
```

### Respostas que esperamos

O Marketplace verificará as informações inseridas nos campos pré determinados, retornando:

```json title="200 - OK" 
true
```

Caso o marketplace valide as informações, iremos disparar outra chamada acionando o remote do **/saveAccount**. Nesse momento, o Marketplace irá armazenar as configurações que o Seller realizou e a informação visual via tela ficará como Ativo. 




---

```json title="401 - Unauthorized"  
false
```
Caso não
