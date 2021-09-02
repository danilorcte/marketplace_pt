# Entenda a API


A versão 2 da API AnyMarket é um passo a frente no sentido de facilitar a integração de nossos parceiros aos diversos marketplaces disponíveis. A criação da API permite que aplicações existentes ou novas aplicações estendam suas operações de venda de forma simples.

Uma vez que você tenha solicitado seu token de acesso ao nosso suporte, é fácil começar a integração com o AnyMarket.

Todos as URLs são acessíveis através do host sandbox-api.anymarket.com.br. Por exemplo: Você pode recuperar todas as suas categorias acessando a URL com o seu TOKEN de acesso (substitua TOKEN pelo seu próprio):

```
http://sandbox-api.anymarket.com.br/v2/categories?gumgaToken=TOKEN
```

É necessário informar o seu token de acesso para todas as URLs que serão acessadas. Além de utilizá-lo como parâmetro na URL, é possível passá-lo como cabeçalho da requisição. O nome gumgaToken deve ser utilizado para ambas as formas.

## Limites

Seja legal. Se você estiver enviando muitas requisições rapidamente, nós retornaremos um código de erro 429 (too many requests). Você tem um limite de **10 requisições por segundo** por token.

## Operações

[cadastrar um produto](#497ef920-87bd-4a3f-b91e-19abadb3f7c0) 

Nós fazemos o nosso melhor para que todas as nossas URLs sejam [RESTful](http://en.wikipedia.org/wiki/Representational_state_transfer). Cada URL pode suportar um dos quatro diferentes tipos de verbos http:

-   **GET** obtém informações sobre um recurso
-   **POST** cria um recurso
-   **PUT** atualiza um recurso
-   **DELETE** exclui um recurso

## Estrutura

### Paginação

A grande maioria das requisições que retornam uma coleção de recursos são paginadas. Por exemplo, a consulta de categorias principais. Toda resposta paginada é retornada no seguinte formato:

```
{
  "links": [
    {
      "rel": "prev",
      "href": "http://sandbox-api.anymarket.com.br/v2/categories?offset=0"
    },
    {
      "rel": "next",
      "href": "http://sandbox-api.anymarket.com.br/v2/categories?offset=4"
    }
  ],
  "content": [
    ...
  ],
  "page": {
    "size": 2,
    "totalElements": 6,
    "totalPages": 3,
    "number": 1
  }
}
```

Para facilitar a navegação sequencial de dados, nós disponibilizamos links para ir a próxima página ou retornar a anterior.

Por padrão a consulta retorna 20 recursos por página. No entanto, nós permitimos que esse número seja aumentado até um máximo de 100. Abaixo segue os parâmetros que alteram a forma como a pagina é retornada:

-   **offset:** Indica a partir de qual recurso a consulta irá começar
-   **limit:** Indica a quantidade de recursos a serem retornados, indo de 20 a no máximo 100.
-   **sort:** Indica por qual atributo a consulta deve ser ordenada
