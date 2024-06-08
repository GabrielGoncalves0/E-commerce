# Mini E-commerce

## Descrição

Projeto academico de desenvolvimento web fullstack com foco na criação de um sistema de e-commerce. Este projeto foi desenvolvido como parte de um curso de Fullstack e engloba uma variedade de tecnologias para garantir sua funcionalidade e desempenho.

## Tecnologias Utilizadas

- **Backend:** Node.js, Express, multer.
- **Frontend:** HTML, CSS, JavaScript, Bootstrap, EJS.
- **Armazenamento Local:** Local Storage.
- **Banco de Dados:** MySQL.
- **Comunicação:** Fetch API.

## Funcionalidades Principais

- **Registro de Produtos e Pedidos:** Permite registrar novos produtos e pedidos no sistema.
- **Vitrine Pública:** Exibe os produtos disponíveis para todos os usuários.
- **Autenticação de Usuários:** Apenas usuários autenticados podem cadastrar novos produtos.
- **Carrinho de Compras:** Adicione itens ao carrinho e confirme pedidos usando Local Storage.
- **Modal de Confirmação de Pedidos:** Confirme pedidos diretamente na vitrine.
- **Listagem de Pedidos:** Exibe todos os pedidos junto com os produtos incluídos.
- **Exportação de Dados:** Exporte dados para formatos Excel e PDF.
- **Filtragem:** Filtragem na tabela pedidos.
  
## Como Começar

Para começar a usar este projeto, siga estas etapas:

1. Clone o repositório:
   ```sh
   git clone https://github.com/GabrielGoncalves0/Mini-E-commerce.git

2. Crie seu banco de dados e coloque em db/database.js

        this.#conexao = mysql.createPool({
            host: '127.0.0.1', //endereço do nosso banco de dados na nuvem
            database: 'db_aula', //a database de cada um de vocês possui a nomenclatura PFS1_(RA)
            user: 'root', // usuario e senha de cada um de vocês é o RA
            password: 'root',
        });

3. Configure o banco de dados MySQL executando o seguinte script:
   
   <details>
     <summary>Script SQL para Configuração do Banco de Dados (clique para expandir)</summary>
  
     ```sql
     create database db_aula;
   
     use db_aula; 
   
     CREATE TABLE `tb_marca` (
       `mar_id` int NOT NULL AUTO_INCREMENT,
       `mar_nome` varchar(255) DEFAULT NULL,
       PRIMARY KEY (`mar_id`)
     ) ENGINE=InnoDB AUTO_INCREMENT=0 DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;
   
     CREATE TABLE `tb_categoria` (
       `cat_id` int NOT NULL AUTO_INCREMENT,
       `cat_nome` varchar(255) DEFAULT NULL,
       PRIMARY KEY (`cat_id`)
     ) ENGINE=InnoDB AUTO_INCREMENT=0 DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;
   
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
   
     CREATE TABLE `tb_perfil` (
         `per_id` INT NOT NULL PRIMARY KEY AUTO_INCREMENT,
         `per_nome` varchar(50) DEFAULT NULL
     );
   
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
   
     create table `tb_pedido` (
         `ped_id` int not null primary key auto_increment,
         `ped_data` datetime
     );
   
     create table `tb_pedidoitens` (
         `pit_id` int not null primary key auto_increment,
         `ped_id` int,
         `prd_id` int,
         `pit_quantidade` int,
         `pit_valorunidade` decimal (6,2),
         `pit_valortotal` decimal(6,2),
         
         constraint `fk_pedido_item` foreign key (`ped_id`) references `tb_pedido`(`ped_id`),
         constraint `fk_pedido_produto` foreign key (`prd_id`) references `tb_produto`(`prd_id`)
     );
   
     insert into tb_marca (mar_nome) values ('Jequiti');
     insert into tb_marca (mar_nome) values ('Boticário');
     insert into tb_marca (mar_nome) values ('Natura');
   
     insert into tb_categoria (cat_nome) values ('Blush');
     insert into tb_categoria (cat_nome) values ('Batom');
     insert into tb_categoria (cat_nome) values ('Maquiagem');
     insert into tb_categoria (cat_nome) values ('Perfume');
   
     insert into tb_perfil(per_nome) values("adm");
     insert into tb_usuario(usu_nome, usu_email, usu_senha, usu_ativo, per_id) values ("admin", "teste@hotmail.com", "teste", 1, "1");

4. Para logar no sistema utilize o login: teste@hotmail.com e a senha: teste;
