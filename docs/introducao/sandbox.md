# Ambiente de sandbox

Para permitir que o integrador teste suas funcionalidades e assegure de que irá operar sem erros no ambiente de produção, o AnyMarket disponibiliza o ambiente de sandbox. Os testes realizados nesse ambiente certificam a aplicação de que todas as regras de API estão sendo aplicadas.

O ambiente de sandbox do AnyMarket possui as mesmas operações do ambiente de produção, no entanto, as informações são distintas do ambiente de produção. Os ambientes de sandbox e produção são isolados e não possuem acesso um ao outro.

Os tokens de acesso obtidos através do contato com o AnyMarket dão acesso aos dois ambientes, porém cada ambiente requisita seu próprio token. Não é possível acessar o ambiente de produção com o token da sandbox e vice-versa.

Uma vez obtido o Token de Sandbox, a Aplicação opera de forma idêntica ao ambiente de produção. A principal diferença é que a Aplicação deve apontar para o ambiente de Sandbox ao invés de Produção.

URL de sandbox:

```
http://sandbox-api.anymarket.com.br/v2
```

URL de produção:

```
http://api.anymarket.com.br/v2
```