# Como importar a coleção de APIs para o Postman

É possível realizar os testes nos endpoints através da nossa página de documentação, entretanto pode ser necessário a importação de umas das nossas api´s ao seu API Client preferido. É o que vamos demonstrar abaixo, simples e fácil. O programa utilizado nos exemplos será o [POSTMAN](https://www.postman.com).



- Acesse a página de referência da API desejada.

<!--
focus: false
-->
![image.png](https://stoplight.io/api/v1/projects/cHJqOjgyMDQx/images/Otg79unc2vA)

- Selecione a opção export e seleciona Bundled References, e salve o arquivo em 

<!--
focus: false
-->
![download.gif](https://stoplight.io/api/v1/projects/cHJqOjgyMDQx/images/X2qE2e2yXrw)

Após baixar o arquivo .yaml

Abrir o POSTMAN -> import -> File -> Upload Files.

<!--
focus: false
-->
![importando.gif](https://stoplight.io/api/v1/projects/cHJqOjgyMDQx/images/f46myXG9sYM)

Pronto. A collection esta importada.

Agora precisamos definir o token de segurança na collection.

1. clicar na collection importada
2. na aba Authorization, preencher o campo Value com seu token

Agora só testar.
