# Como funciona fluxo Anúncio

Quando o seller cria uma nova publicação, o remote **/canSave** é disparado e é onde o marketplace poderá fazer uma pré-validação do anúncio, antes que ele seja publicado. Porém o Marketplace pode não optar por realizar essa pré-validação, nesses casos basta que ele retorne um **http - 200 OK** e no **"responsebody = true"** que é a informação esperada para prosseguir com o anúncio, conforme imagem do fluxo abaixo.

Após o seller clicar para confirmar a publicação, irá aparecer para ele em tela se o mesmo pretende enviar essa publicação para o Marketplace. Se o seller clica em "SIM", o remote **/sendProduct** entra em ação, que é o responsável por enviar uma notificação ao marketplace atraves do middleware dizendo que um anuncio foi criado no ANYMARKET. Caso o seller clique em "NÃO" a publicação fica no estado de Stand By e o **/sendProduct** não é disparado até que o envio da publicação seja feito na tela de transmissão, selecionando a publicação criada e clicando no botão ENVIAR.

Toda nova criação de publicação, a informação de STATUS que será disparado no JSON do **/sendProduct** sempre irá como **"UNPUBLISHED"**, nesse momento o marketplace fará um GET no endpoint **/skumarketplace/{id}** para buscar os dados da transmissão e cadastrar o anúncio, e realize também um PUT no endpoint **/skumarketplace/{id}** informando para nós qual o STATUS da publicação no marketplace, por exemplo:
- **Ativo;**
- **Em catalogação;**
- **Publicação em analise;**

O esperado é que essas ações ocorram de forma síncrona.

**Sobre os tipos de Status no ANYMARKET clique nesse [Link](https://anymarketplace.stoplight.io/docs/marketplace-pt/b3A6MjA2MjE0NTk-atualizar-dados-da-transmissao).**

### O remote do /sendProduct será disparado sempre quando tivermos alguma criação ou atualização da transmissão.

<!--
focus: false
-->
![image.png](http://s3-sa-east-1.amazonaws.com/images.anymarket.com.br/36019811./85A383CC28FC3896B154C85A70BACD3B/standard_resolution.jpg)

---

# Atualizando Publicação

Começando pelo módulo temos um botão “Atualizar apenas preço, estoque e status?” que existe na aba “configurações de Anúncios” que são representados pelos atributos no Json do **/sendProduct**;

- **onlySyncPrice: boolean**
- **onlySyncStock: boolean**
- **onlySyncStatus: boolean**

São referente ao parâmetro do modulo aonde o seller pode definir que "Atualizar apenas preço, estoque e status", fazendo com que ao receber esses dados como **"false"** o Marketplace deve atualizar todas as informações cadastrais ou seja, consumir as informações como titulo, descrição, imagens e etc, para que o anuncio tenha as mesmas informações que estão no produto dentro do ANYMARKET. 

Por outro lado, quando a informação estiver como **"true"**, quer dizer que o seller definiu que após o envio do anuncio, qualquer nova atualização deve ser somente atualizado "Preço, estoque e status".
<!--
focus: false
-->
![image.png](http://s3-sa-east-1.amazonaws.com/images.anymarket.com.br/36019811./774D3EF342B5328F86977ED7EAD93FEE/standard_resolution.jpg)

Caso a flag do modulo esteja **"Habilitada"** (**onlySyncStatus,onlySyncPrice,onlySyncStock = true**) o Marketplace não precisa acionar o endpoint: **/skumarketplace/{id}** e sim o endpoint **/skumarketplace/{id}/priceStock** tendo somente os valores pertinentes ao preço de(**price**), preço por(**discountPrice**) e estoque(**availableAmount**);

**Contendo o responseBody:**
```json title="GET: /skumarketplace/{id}/priceStock" lineNumbers
{
    "id": 62325,
    "skuInMarketplace": "22222",
    "idInMarketplace": "62325",
    "price": 59.9,
    "discountPrice": 43.93,
    "availableAmount": 100
}
````


Se o anuncio sofreu atualização de estoque, preço ou status eles seram mapeados nos seguintes atributos do json do **/sendProduct:**

- **updateStatus": boolean**
- **updatePrice": boolean**
- **updateStock": boolean**

Caso o anuncio tenha sofrido uma atualização de estoque será disparado:
```json title="POST: \sendProduct" lineNumbers
{
"idSkuMarketplace": 123456,
"idSkuMarketplaceMain": 1234567,
"status": "ACTIVE",
"onlySync": true,
"idSku": 251231,
"availableAmount": 1000,
"idAccount": 25,
"idProduct": 222222,
"skuInMarketplace": null,
"onlySyncPrice": true,
"onlySyncStock": true,
"onlySyncStatus": true,
"updateStatus": false,
"updatePrice": false,
"updateStock": true
}
```
Conforme os cenários de atualizações, caso na api do marketplace tenha rotas diferentes para cada atualização o mesmo não precisará acionar duas rotas sempre que o **/sendProduct** for disparado, sabendo de fato o que atualizar conforme os parâmetros encaminhados ou até mesmo retirar a necessidade de comparação dos valores para realizar a atualização. 

A utilização do endpoint **/skumarketplace/{id}/priceStock** também pode ser utilizado para fins de performance visto que são menos dados que são retornados, ficando como endpoint opcional.

# Excluindo uma Publicação

### DELETE /deletePublication

Esse remote é acionado quando uma publicação é excluida no AnyMarket, notificando ao Marketplace que foi realizado uma exclusão e que é necessário que ele desative essa publicação tambem no Marketplace.