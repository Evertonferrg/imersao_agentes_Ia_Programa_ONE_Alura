# Aula 03 Produção 

Para iniciar a aula criamos um bot no telegran, para isso acessamos o https://web.telegram.org

- buscamo por *BotFather* iniciar e ao apertar */* solicitamos o criar novo bot.

- criamos um nome para bot como o final _bot exemplo o que foi feito em aula chocolatech_bot.

Sera gerado um token de acesso que devera ser copiado para usar no n8n.

## Inicio no N8N

Para inicia duplicamos o arquivo da aula dois nomeando como produção aula3. 

No novo arquivo removemos o *When chat message received* e trocamos por né de *telegran* e um gatilho de *on message*.
- em Credential usarememos * Create new credential* e em *Access Token* usaremos o tokken criado no telegram. 

Na outra ponta do *AI AGENT* criamos um novo no do *Telegram* mas agora usando *Send a text message* .
- mantemos:
  - Resource como : Message
  - Operation como: Send Message
E Chat ID: clicamos em *Expression* na caixa do chat id. Ao tentar executar teremos o erro do *simple Memory*. 
 - em Simple Memory mudamos a *Session ID* para *Define below* e em Key espandimos a tela e buscamos o "Id" do "chat" e arrastamos para o Expression. ficara :
 ```
 {{ $json.message.chat.id}} 
 ```
 E em result contera o id do chat.

- Agora teremos um erro no agent que esta usando um chat input, trocaremos:
 - *Source for prompt* para *Define below*
 - com o * Telegran Trigger* em execução acessarmos as configurações do *AI Agent*
 E arras tamos *text* da mensagem para o *Prompt*, especificando para o prompt de onde esta vindo as informações.

Agora vamos voltar a configurar o no de resposta do Telegran acessando as configurações.
 - em *Text* puxamos o *output* em AI Agent que esta a esquerda.
 - Abrimos o Telegran Trigger e arranstmos o *id* do chat para o *Chat ID* dos paramentros.

Por fim iremos usar o Publish para automatizar a automacao publicando o projeto.