Projeto: NexTech E-commerce Assistant 🚀

Bem-vindo à documentação do NexTech E-commerce Assistant, uma inteligência artificial desenvolvida para gerir o atendimento, consultas de catálogo, pedidos e gestão de sugestões de produtos da empresa NexTech.

[logo empresa ](./src/img/Gemini_Generated_Image_5twivj5twivj5twi.png)

Este projeto evoluiu através de três fases de desenvolvimento, integrando orquestração de fluxos, bancos de dados relacionais e inteligência artificial generativa para criar um atendimento automatizado e eficiente.



🛠️ Tecnologias Utilizadas
Orquestração: N8N (Workflow Automation)

Inteligência Artificial: Cohere (LLM, Embeddings e AI Agent)

Banco de Dados: MySQL

Hospedagem de Banco: Railway

Interface de Usuário: Telegram Bot API

Arquitetura: RAG (Retrieval-Augmented Generation) com Vector Store

📈 Evolução do Projeto
Aula 01: Fundamentos
Iniciámos o projeto estabelecendo a base da estrutura do NexTech, preparando o ambiente para a automação e definindo o escopo do assistente de e-commerce.

[Imagem Aula 01 ](./src/img/aula01.png)

Aula 02: Integração com Base de Dados
Nesta etapa, conectamos o sistema a um banco de dados real para armazenamento de informações.

Infraestrutura: Criámos a base de dados no Railway, configurando domínios públicos para acesso remoto.

Modelagem de Dados: Estruturamos tabelas relacionais (clientes, produtos, pedidos, sugestoes_produtos) para permitir a consulta dinâmica.

Conectividade: Configurámos as credenciais do MySQL no N8N, permitindo que o Agente de IA realizasse consultas (SELECT) e inserções (INSERT) diretamente no banco.
[Imagem banco de Dados ](./src/img/bancoDeDados.png)

[Imagem Aula 02 ](./src/img/aula02.png)

Aula 03: Produção, Telegram e Fluxo Inteligente
Na fase final, transformamos o protótipo numa ferramenta de produção.

Interface: Integração via Telegram Bot (configurado através do BotFather).

Gestão de Contexto: Implementação do Simple Memory para garantir que o bot lembre o histórico da conversa com cada utilizador (via chat.id).

Fluxo Inteligente: Introdução de um Text Classifier e um nó Switch. Esta arquitetura separa logicamente a Consulta de Catálogo (tratada pelo AI Agent com Cohere) dos fluxos de Cadastro (tratados diretamente por ferramentas de banco de dados), otimizando tokens e aumentando a precisão da IA.
[Imagem Aula 03 ](./src/img/aula03.png)

Publicação: Automação pronta em ambiente de produção.

🤖 Persona do Assistente (System Prompt)
O NexTech E-commerce Assistant foi configurado com uma persona técnica e profissional:

[Imagem chat 01 ](./src/img/chat%201.png)
[Imagem chat 02 ](./src/img/chat2.png)
[Imagem chat 03 ](./src/img/chat%203.png)



Responsabilidades: Atendimento ao cliente, consulta de estoque/preços e suporte a pedidos.

Regras de Ouro: Não inventar dados, cruzar informações entre clientes e pedidos para relatórios precisos e responder de forma comercial e eficiente.

📊 Estrutura do Banco de Dados
Abaixo, o esquema atual que sustenta a inteligência do nosso bot:

clientes: Gestão de cadastro.

produtos: Catálogo com URL de imagem, preço e stock.

pedidos: Histórico de transações vinculadas aos clientes.

sugestoes_produtos: Tabela dedicada para capturar novos interesses dos clientes (funcionalidade "Lista de Desejos").

🚀 Como Executar
Garanta que o seu N8N tenha acesso à URL do banco MySQL no Railway.

Verifique se o Token do Telegram está ativo no Telegram Trigger.

Execute o fluxo com a intenção de cadastro ou consulta para validar o roteamento do nó Switch.

----
## Projeto Realizado:
Este projeto foi executado apartir das aulas da Imersao Agentes de IA da Alura / One.

Projeto executado por :
Everton Ferreira Guedes 

