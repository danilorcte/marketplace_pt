# autenticacao

1 - Autenticação API ANYMARKET(endpoints):
Para a autenticação com a API Marketplace, o parceiro deve informar o header o appId fornecido pelo ANYMARKET. Lembrando, appId é o identificador único do marketplace. Além dessa informação, o parceiro também deve informar o header token para as chamadas ao ANYMARKET, que é o Token fornecido pelo ANYMARKET para o lojista.

2 - Autenticação ANYMARKET com o parceiro (remotes):
A tecnologia utilizada é a autenticação JWT (https://jwt.io/). O ANYMARKET encaminhará, em todas as chamadas para o endpoint do parceiro, o header identificado como x-anymarket-token , com o valor JWT com as seguintes informações:

"organization" - Nome da empresa
"oi" - Organization ID, identificador único do lojista; Esse campo diferencia os sellers
"exp" - Tempo de expiração do token
"login" - Usuário que está realizando a chamada; Pode ser utilizado para fins de auditoria

"O parceiro deve estar preparado para receber o token, verificar a expiração do mesmo e identificar a assinatura com a chave pública do ANYMARKET."

Chave pública ANYMARKET

MIGfMA0GCSqGSIb3DQEBAQUAA4GNADCBiQKBgQDVfxWEym1WAYwGhrNjvEUWRgB +p9oUPGu59yePzUT+I/d+C2x9xjURa/Zc+VVZsK2OrHga1+4X4iO1q+nWhmXkD5VysCaJ9 vf7IVntWogFpaBauG2EI7J93Y/sKUBxwxSDZPKhovsaM3DxoNCfW4lUHAWnlIuzPx302TB GtfCpUwIDAQAB

Exemplo JWT ANYMARKET

eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiJ9.eyJpcCI6IjEwLjAuOS4xNzIiLCJvcmdhbml6YXRpb24iOiJBTllNQVJLRVQgVGVzdGUgLSBCcmFzaWwiLCJvaSI6IjIyNDQ5NTA0LiIsImV4cCI6MTYxMjc5MTI2NCwibG9naW4iOiJkYW5pbG8ub2xpdmVpcmFAZGIxLmNvbS5iciJ9.FKF8wRb97xZmpakGbkoYfO0cjIkj48rwcis4DOGlUEh4cD98sFRJTVfrmMOaAe-XrBoPvTWbSdJfNy81-_VMLq9dbcKpBPO8MfHDXmqWV7tuHT1BaIcOkYZl-uIvOMtxCmDiCrX1ny2DvjY_LLuzRjexM6CQw4rRt8NXZb3dGV4


Recomendações

O header x-anymarket-token possui um valor jwt que contem o "OI." (Organization Id/ Identificador do seller no ANYMARKET). Sabendo disso o middleware/marketplace deve fazer a identificação do seller por esse valor. É comum que os marketplaces solicitem para o cliente que ira utilizar da integração o "oi." para a abertura do chamado e com isso quando for disparado as chamadas para o middleware o mesmo terá a informação que o "OI." "X" corresponde ao seller "Y" e saberá que o seller possui liberação ou não para completar as chamadas.