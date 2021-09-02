## API Marketplace | ANYMARKET

Para o início do desenvolvimento da integração, deverá ser preenchido o formulário para liberação do Marketplace. Este formulário é enviado para a equipe de desenvolvimento que disponibiliza o novo marketplace dentro do ANYMARKET. Nesse momento, serão enviados para você um usuário do ANYMARKET para que você realize os testes do seu desenvolvimento e o appId, que é o identificador do seu marketplace dento do ANYMARKET.
Este id deverá ser utilizado em todas as chamadas que você realizar para nossa API.



O marketplace deve construir um middleware seguindo os padrões estabelecidos nos “remotes”, que serão os caminhos que o ANYMARKET irá enviar a chamada para completar as ações que o seller realizar. Em conjunto com as notificações que o ANYMARKET encaminhará para o middleware, o mesmo precisará interpretar as chamadas e realizar as devidas ações, podendo ser processamentos interno do próprio marketplace ou chamadas para a nossa API afim de inserir informações, atualizar ou consumir dados pertinentes a ação que está sendo executada.




> #### Operações
> Nós fazemos o nosso melhor para que todas as nossas URLs sejam RESTful. Cada URL pode suportar um dos quatro diferentes tipos de verbos HTTP:
> |               |                                     |   
> | ------------- | :---------------------------------: | 
> | GET           | obtém informações sobre um recurso  |
> | POST          | cria um recurso                     | 
> | PUT           | atualiza um recurso                 | 
> | DELETE        | exclui um recurso                   | 

<!-- theme: danger -->

> #### Informações Importantes
>
> Seja legal. Se você estiver enviando muitas requisições rapidamente, nós retornaremos um código de erro 429 (too many requests). 
>
>Você tem um limite de 10 requisições por segundo por token.

> #### Dúvidas, sugestões e feedbacks podem ser encaminhados por e-mail para: 
> api@anymarket.com.br.

