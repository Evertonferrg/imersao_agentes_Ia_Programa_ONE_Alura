-- 1. Criação das Tabelas
CREATE TABLE IF NOT EXISTS clientes (
    id INT AUTO_INCREMENT PRIMARY KEY,
    nome VARCHAR(100) NOT NULL,
    email VARCHAR(150) NOT NULL UNIQUE,
    telefone VARCHAR(20),
    data_cadastro TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

CREATE TABLE IF NOT EXISTS produtos (
    id INT AUTO_INCREMENT PRIMARY KEY,
    nome VARCHAR(150) NOT NULL,
    categoria VARCHAR(50),
    preco DECIMAL(10, 2) NOT NULL,
    estoque INT NOT NULL DEFAULT 0,
    descricao TEXT,
    url_imagem VARCHAR(255)
);

CREATE TABLE IF NOT EXISTS pedidos (
    id INT AUTO_INCREMENT PRIMARY KEY,
    cliente_id INT,
    data_pedido TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    valor_total DECIMAL(10, 2) NOT NULL,
    status VARCHAR(20) DEFAULT 'pendente',
    FOREIGN KEY (cliente_id) REFERENCES clientes(id)
);

-- 2. Limpeza de dados antigos para evitar duplicidade (opcional)
-- DELETE FROM clientes;
-- DELETE FROM produtos;

-- 3. Inserção de Dados (Seed)
INSERT INTO clientes (nome, email, telefone) VALUES
('Alice Silva', 'alice.silva@gmail.com', '11977776666'),
('Roberto Dias', 'rdias_tech@outlook.com', '21988885555'),
('Carla Mendes', 'carla.mendes@empresa.com', '31999994444');

INSERT INTO produtos (nome, categoria, preco, estoque, descricao, url_imagem) VALUES
('Monitor Ultrawide 34"', 'Periféricos', 2800.00, 15, 'Monitor curvo de alta resolução', 'https://via.placeholder.com/300?text=Monitor+Ultrawide'),
('Arduino Uno R4', 'IoT', 180.00, 80, 'Placa de desenvolvimento', 'https://via.placeholder.com/300?text=Arduino+Uno+R4'),
('Fonte 750W Gold', 'Hardware', 650.00, 25, 'Fonte modular 80 Plus', 'https://via.placeholder.com/300?text=Fonte+750W'),
('Câmera Segurança WiFi', 'Smart Home', 320.00, 40, 'Visão noturna e detecção', 'https://via.placeholder.com/300?text=Camera+WiFi'),
('Headset Gamer Pro', 'Periféricos', 590.00, 20, 'Cancelamento de ruído', 'https://via.placeholder.com/300?text=Headset+Gamer'),
('Esp32 DevKit V1', 'IoT', 85.00, 120, 'WiFi e Bluetooth integrado', 'https://via.placeholder.com/300?text=ESP32+DevKit'),
('SSD NVMe 1TB', 'Hardware', 520.00, 60, 'Velocidade 7000MB/s', 'https://via.placeholder.com/300?text=SSD+NVMe+1TB');



CREATE TABLE IF NOT EXISTS sugestoes_produtos (
    id INT AUTO_INCREMENT PRIMARY KEY,
    cliente_id INT,
    nome_produto VARCHAR(150),
    data_sugestao TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    FOREIGN KEY (cliente_id) REFERENCES clientes(id)
);

*   **Opção B (Registrar no Chat/Logs):** Se não quiser criar tabela, você pode simplesmente instruir o Agente a registrar isso em uma variável de memória ou, melhor ainda, solicitar que o Agente "anote" isso para você em um arquivo ou base de conhecimento.

---

### 2. Atualização no seu System Prompt
Para que o Agente saiba lidar com essa solicitação, adicione estas instruções ao seu **System Prompt** (dentro do nó do Agente):

> **FLUXO DE SUGESTÃO DE PRODUTOS:**
> 1. Se o cliente solicitar a inclusão de um produto para futuras compras, verifique primeiro se o produto já existe na tabela `produtos`.
> 2. **Se o produto existir:** Confirme com o cliente que ele foi adicionado à "Lista de Desejos" (ou equivalente).
> 3. **Se o produto NÃO existir:** Pergunte ao cliente: *"Este item ainda não consta em nosso catálogo. Poderia me dar mais detalhes ou o nome completo do produto que gostaria de ver disponível nas próximas compras?"*
> 4. **Ação:** Após o cliente fornecer os dados, utilize a ferramenta de `INSERT` na tabela `sugestoes_produtos` (ou simplesmente responda confirmando que a sugestão foi registrada para a equipe de compras da NexTech).

---

### 3. Configuração no n8n
Para que isso funcione, siga estes passos:

1.  **Crie o nó MySQL de Insert:** Configure um novo nó de `Insert` apontando para a tabela `sugestoes_produtos`.
2.  **Mapeie os parâmetros:** O seu Agente precisará extrair o `nome_produto` e o `cliente_id` da conversa.
3.  **Habilite a ferramenta:** Adicione este nó de `Insert` como uma nova **Tool** no seu **AI Agent** (assim como você fez para a ferramenta de cadastro de clientes).

### Dica de Fluxo para o Cliente
Quando o cliente disser: *"Quero comprar o produto X no futuro"*, o seu Agente agora:
1.  Busca o cliente pelo nome (para pegar o `cliente_id`).
2.  Verifica se o produto existe.
3.  Se tudo estiver certo, executa o `INSERT` na tabela de sugestões.
4.  Responde: *"Perfeito! Registrei seu interesse no produto X. Assim que ele estiver disponível, entraremos em contato."*

**Deseja que eu te passe o código SQL completo para você criar essa tabela de sugestões e já deixar o banco preparado para esse fluxo de "Lista de Desejos"?**