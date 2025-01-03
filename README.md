# Mini E-commerce 🚀

## Descrição 📜

**Mini E-commerce** é um projeto acadêmico de desenvolvimento web **fullstack** com foco na criação de um sistema de e-commerce. Desenvolvido como parte de um curso de Fullstack, este projeto integra uma variedade de tecnologias modernas para garantir sua funcionalidade e desempenho.

O objetivo é criar uma plataforma simples e eficiente onde usuários possam navegar, adicionar produtos ao carrinho, realizar pedidos e gerenciar seu catálogo de produtos. Ao mesmo tempo, administradores podem cadastrar novos produtos e visualizar os pedidos feitos.

---

## Tecnologias Utilizadas ⚙️

O sistema foi desenvolvido utilizando as seguintes tecnologias:

- **Backend:** 
  - Node.js
  - Express
  - Multer (para upload de arquivos)
  
- **Frontend:**
  - HTML
  - CSS
  - JavaScript
  - Bootstrap
  - EJS
  
- **Armazenamento Local:** Local Storage (para persistência de dados do carrinho).
- **Banco de Dados:** MySQL (para armazenamento de dados de produtos, pedidos e usuários).
- **Comunicação:** Fetch API (para fazer requisições assíncronas entre o front-end e o back-end).

---

## Funcionalidades Principais 🎯

O **Mini E-commerce** oferece as seguintes funcionalidades principais:

- **Registro de Produtos e Pedidos**: Permite que novos produtos e pedidos sejam cadastrados no sistema.
- **Vitrine Pública**: Exibe os produtos disponíveis para todos os usuários, com filtros de busca.
- **Autenticação de Usuários**: Apenas usuários autenticados podem cadastrar novos produtos e realizar pedidos.
- **Carrinho de Compras**: Adicione produtos ao carrinho e confirme pedidos utilizando Local Storage.
- **Modal de Confirmação de Pedidos**: Confirme pedidos diretamente na vitrine de produtos.
- **Listagem de Pedidos**: Visualize todos os pedidos realizados, incluindo os produtos comprados.
- **Exportação de Dados**: Exporte os dados de pedidos e produtos para formatos Excel e PDF.
- **Filtragem**: Permite filtrar pedidos por diferentes critérios na lista de pedidos.

---

## Imagens do Projeto 📸

Veja abaixo algumas imagens demonstrando o funcionamento do projeto:

### 1. **Vitrine Pública**

A vitrine exibe todos os produtos disponíveis para compra:

![Vitrine Pública](https://github.com/user-attachments/assets/e1104f83-239c-418e-9207-6fdcfd1922aa)

---

### 2. **Carrinho de Compras**

O carrinho permite que o usuário visualize os produtos adicionados antes de finalizar a compra:

![Carrinho de Compras](https://github.com/user-attachments/assets/158cced2-28bf-432f-bb6a-67d0fc6c6570)

---

### 3. **Lista de Pedidos**

Aqui, os administradores podem visualizar todos os pedidos realizados, com detalhes de produtos e valores:

![Lista de Pedidos](https://github.com/user-attachments/assets/c4f098b2-9296-4a4d-b41a-1330970d9f57)

---

### 4. **Listagem de Produtos**

Os administradores podem cadastrar novos produtos e visualizá-los nesta tela:

![Listagem de Produtos](https://github.com/user-attachments/assets/d88e61b5-94e2-4435-a14c-1dac1c52ceab)

---

## Como Começar 🚀

Siga os passos abaixo para começar a usar o **Mini E-commerce** em sua máquina:

### 1. **Clone o Repositório**

Clone o repositório para o seu ambiente local utilizando o comando abaixo:

```sh
git clone https://github.com/GabrielGoncalves0/Mini-Ecommerce.git
```

---

### 2. **Configuração do Banco de Dados**

Crie seu banco de dados e configure a aplicação com os dados correspondentes:

```javascript
this.#conexao = mysql.createPool({
    host: '', // Endereço do banco de dados
    database: '', // Nome do seu banco de dados
    user: '', // Usuário do banco
    password: '', // Senha do banco
});
```

<details>
  <summary>Script SQL para criação do Banco de Dados (Clique para expandir)</summary>

  ```sql
  -- Criação do banco de dados
  CREATE DATABASE db_aula;
  USE db_aula;

  -- Tabela de Marcas
  CREATE TABLE `tb_marca` (
    `mar_id` int NOT NULL AUTO_INCREMENT,
    `mar_nome` varchar(255) DEFAULT NULL,
    PRIMARY KEY (`mar_id`)
  ) ENGINE=InnoDB AUTO_INCREMENT=0 DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;

  -- Tabela de Categorias
  CREATE TABLE `tb_categoria` (
    `cat_id` int NOT NULL AUTO_INCREMENT,
    `cat_nome` varchar(255) DEFAULT NULL,
    PRIMARY KEY (`cat_id`)
  ) ENGINE=InnoDB AUTO_INCREMENT=0 DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;

  -- Tabela de Produtos
  CREATE TABLE `tb_produto` (
    `prd_id` int NOT NULL AUTO_INCREMENT,
    `prd_cod` varchar(50) DEFAULT NULL,
    `prd_nome` varchar(255) DEFAULT NULL,
    `prd_quantidade` int DEFAULT NULL,
    `cat_id` int DEFAULT NULL,
    `mar_id` int DEFAULT NULL,
    `prd_imagem` varchar(100) DEFAULT NULL, 
    `prd_valor` int DEFAULT NULL,
    PRIMARY KEY (`prd_id`),
    KEY `fk_produto_marca` (`mar_id`),
    KEY `fk_produto_categoria` (`cat_id`),
    CONSTRAINT `fk_produto_categoria` FOREIGN KEY (`cat_id`) REFERENCES `tb_categoria` (`cat_id`),
    CONSTRAINT `fk_produto_marca` FOREIGN KEY (`mar_id`) REFERENCES `tb_marca` (`mar_id`)
  ) ENGINE=InnoDB AUTO_INCREMENT=0 DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;

  -- Tabela de Perfis
  CREATE TABLE `tb_perfil` (
    `per_id` INT NOT NULL PRIMARY KEY AUTO_INCREMENT,
    `per_nome` varchar(50) DEFAULT NULL
  );

  -- Tabela de Usuários
  CREATE TABLE `tb_usuario` (
    `usu_id` INT NOT NULL PRIMARY KEY AUTO_INCREMENT,
    `usu_nome` varchar(50) DEFAULT NULL,
    `usu_email` varchar(50) DEFAULT NULL,
    `usu_senha` varchar(50) DEFAULT NULL,
    `usu_ativo` INT DEFAULT NULL,
    `per_id` INT DEFAULT NULL,
    KEY `fk_usuario_perfil` (`per_id`),
    CONSTRAINT `fk_usuario_perfil` FOREIGN KEY (`per_id`) REFERENCES `tb_perfil` (`per_id`)
  );

  -- Tabela de Pedidos
  CREATE TABLE `tb_pedido` (
    `ped_id` int not null primary key auto_increment,
    `ped_data` datetime
  );

  -- Tabela de Itens de Pedidos
  CREATE TABLE `tb_pedidoitens` (
    `pit_id` int not null primary key auto_increment,
    `ped_id` int,
    `prd_id` int,
    `pit_quantidade` int,
    `pit_valorunidade` decimal(6,2),
    `pit_valortotal` decimal(6,2),
    
    CONSTRAINT `fk_pedido_item` FOREIGN KEY (`ped_id`) REFERENCES `tb_pedido`(`ped_id`),
    CONSTRAINT `fk_pedido_produto` FOREIGN KEY (`prd_id`) REFERENCES `tb_produto`(`prd_id`)
  );

  -- Inserção de dados iniciais
  INSERT INTO tb_marca (mar_nome) VALUES ('Jequiti');
  INSERT INTO tb_marca (mar_nome) VALUES ('Boticário');
  INSERT INTO tb_marca (mar_nome) VALUES ('Natura');

  INSERT INTO tb_categoria (cat_nome) VALUES ('Blush');
  INSERT INTO tb_categoria (cat_nome) VALUES ('Batom');
  INSERT INTO tb_categoria (cat_nome) VALUES ('Maquiagem');
  INSERT INTO tb_categoria (cat_nome) VALUES ('Perfume');

  INSERT INTO tb_perfil (per_nome) VALUES("adm");
  INSERT INTO tb_usuario (usu_nome, usu_email, usu_senha, usu_ativo, per_id) 
    VALUES ("admin", "teste@hotmail.com", "teste", 1, "1");

```
</details>

---

### 3. **Rode a aplicação**

**No diretório do projeto, execute**
```sh
npm install
```
**Iniciar o Servidor**
```sh
npm start
```

---

## 4. Login de Teste

Para acessar o sistema, utilize as credenciais que cadastrou no usuário, por exemplo:

- **Email:** teste@hotmail.com
- **Senha:** teste

---

## Contribuindo 🤝

Contribuições são sempre bem-vindas! Se você tiver sugestões ou melhorias para este projeto, sinta-se à vontade para:

1. **Abrir uma Issue**: Relate problemas ou faça sugestões para melhorias.
2. **Enviar um Pull Request**: Se você implementou uma melhoria ou correção, envie seu pull request para revisão.

Fique à vontade para contribuir, e vamos construir um projeto melhor juntos!

---


