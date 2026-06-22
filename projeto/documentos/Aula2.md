# Aula 02 Daremos mais contesto ao projeto
N8N Buscara informações mais detalhadas do projeto.

Usando como base o que foi criado na aula 01 usarmemos, o *NEXTECH1* .

Para comcecar, no nó de *AI Agent* - *Tool (ferramentas)* criaremos um banco de dados * MySQL TOOL *, buscaremos os dados de uma ferrmanta a *Railway* .

Na configuração de MySQL em *Operation* usarmos como *Select*.

Usarmeos a integracao do banco de dados no Railway criando uma conta em https://railway.com/dashboard, e criando um *New* uma nova conecao do banco de dados e usarmeos *Database* e usarmos o *MySQL*.

Com tudo criado agora iremos criar as tabelas usando um comando em sql para a criação.

- Na aula foi usado o comando :
```
CREATE TABLE funcionarios (
    id INT AUTO_INCREMENT PRIMARY KEY,
    nome VARCHAR(100) NOT NULL,
    email VARCHAR(150) NOT NULL UNIQUE,
    departamento VARCHAR(100) NOT NULL,
    cargo VARCHAR(100) NOT NULL,
    data_admissao DATE NOT NULL,
    saldo_ferias INT NOT NULL DEFAULT 0,
    banco_horas DECIMAL(5,1) NOT NULL DEFAULT 0,
    regime VARCHAR(20) NOT NULL DEFAULT 'hibrido'
);

INSERT INTO funcionarios (nome, email, departamento, cargo, data_admissao, saldo_ferias, banco_horas, regime) VALUES
('João Silva', 'joao.silva@empresa.com', 'Engenharia', 'Engenheiro de Software', '2022-03-10', 20, 0.0, 'hibrido'),
('Maria Souza', 'maria.souza@empresa.com', 'Recursos Humanos', 'Analista de RH', '2021-05-15', 5, 12.5, 'hibrido'),
('Carlos Oliveira', 'carlos.oliveira@empresa.com', 'Financeiro', 'Analista Financeiro', '2023-01-20', 0, 0.0, 'presencial'),
('Ana Lima', 'ana.lima@empresa.com', 'Marketing', 'Especialista em Marketing', '2020-11-05', 15, -4.0, 'remoto'),
('Pedro Santos', 'pedro.santos@empresa.com', 'Vendas', 'Executivo de Vendas', '2022-08-01', 10, 8.0, 'hibrido'),
('Fernanda Costa', 'fernanda.costa@empresa.com', 'Operações', 'Gerente de Operações', '2019-02-12', 30, 0.0, 'presencial'),
('Rafael Mendes', 'rafael.mendes@empresa.com', 'TI', 'Analista de Suporte', '2023-06-10', 0, 15.5, 'hibrido'),
('Juliana Rocha', 'juliana.rocha@empresa.com', 'Engenharia', 'Desenvolvedora Front-end', '2021-09-25', 12, 0.0, 'remoto'),
('Bruno Alves', 'bruno.alves@empresa.com', 'Design', 'Designer UX/UI', '2022-04-18', 8, 3.5, 'hibrido'),
('Camila Ferreira', 'camila.ferreira@empresa.com', 'Atendimento', 'Analista de Atendimento', '2024-01-05', 0, 0.0, 'hibrido'),
('Eric Monné', 'eric.monne@chocolatech.com', 'Produto', 'Instrutor de Cursos', '2024-01-15', 25, 8.0, 'hibrido');
```

Para o caso do meu projeto usei os dados contidos no arquivo [sql.md](sql.md)

Apos criar os dados vamos na guia *Settings* descemos a tela até *Networking* e criaremos um link publico para acesso ao banco, clicnado em * Generate Domain*.
 - em Generante Service Domain esolheremos a *3306* e clicaremos em Generate Domain.

O endereco gerado foi acela.proxy.rlwy.net:13372.

Voltando para o N8N, em credencial, usarmos a credencial criada no Railway.
Criaremos uma nova credencial, e me Host usarmemos e endereco acela.proxy.rlwy.net que foi criado anteriormente e 
- Porta usarmeos :13372,
- Usuario : Root
- E a Senha: e mais dificil encontar no Railway, temos que ir em *Variables* e temos a *MYSQL_ROOT_PASSWORD* que copiaremos para usar no N8N.
- Database = railway

Voltando para os Paramters informaremos as tablelas a serem buscadas em *Table*

E atualizaremos o AI Agente, Adicionaremos a busca da informações no banco. 
Clicaremos e *+ add Options * e depois *System Message*. e usaremos o prompt :
```
para o meu projeto utilizei os dados que estao em [systemPrompt.md](systemPrompt.md).
