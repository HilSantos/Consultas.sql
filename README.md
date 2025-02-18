# Consultas.sql
Consultas dos mais variados tipos e um exercicio

--Consultas simples:
--Selecione todos os produtos cadastrados
SELECT nome_produto FROM `tb_produtos`
--Liste apenas os nomes e marcas dos produtos
SELECT nome_produto, marca_produto FROM `tb_produtos`
--Exiba os produtos cujo valor de venda seja maior que R$ 800,00
SELECT nome_produto, valor_venda_produto FROM `tb_produtos` WHERE valor_venda_produto > 800
--Mostre todos os produtos que tenham a marca "Nautika"
SELECT nome_produto, marca_produto FROM `tb_produtos` WHERE marca_produto = 'Nautika'
--Liste os produtos ordenados pelo valor de venda do mais barato para o mais caro
SELECT nome_produto, valor_venda_produto FROM `tb_produtos` ORDER BY valor_venda_produto
______________________________________________________________________________________________________________________
--Consultas com filtros:
--Exiba os produtos cujo estoque (quantidade) seja menor que 30
SELECT nome_produto, quantidade_produto FROM `tb_produtos` WHERE quantidade_produto < 55
--Liste os produtos cujo nome começa com a letra "A"
SELECT nome_produto FROM `tb_produtos` WHERE nome_produto LIKE 'B%'
--Mostre os produtos que possuem validade até o final do ano de 2026
SELECT nome_produto, validade_produto FROM `tb_produtos` WHERE validade_produto <= '2027-12-31'
--Exiba os produtos que custam entre R$ 300,00 e R$ 2000,00
SELECT nome_produto, valor_venda_produto FROM `tb_produtos` WHERE valor_venda_produto BETWEEN 300 AND 2500
--Liste os produtos fornecidos pela empresa "Fox Tech Ltda"
SELECT nome_produto, fornecedor_produto FROM `tb_produtos` WHERE fornecedor_produto = 'Fox Tech Ltda'
______________________________________________________________________________________________________________________
--Consultas com Funções agregadas:
--Conte quantos produtos estão cadastrados na tabela
SELECT COUNT(*) FROM tb_produtos
--Exiba o valor medio de venda dos produtos
SELECT AVG(valor_venda_produto) FROM tb_produtos
--Mostre o nome do produto mais caro e o mais barato
SELECT nome_produto, MAX(valor_venda_produto) FROM tb_produtos
_______________________________________________________________________________________________________________________
SELECT nome_produto, valor_venda_produto
FROM tb_produtos
WHERE valor_venda_produto = (SELECT MAX(valor_venda_produto) FROM tb_produtos)
OR valor_venda_produto = (SELECT MIN(valor_venda_produto) FROM tb_produtos);
--Calcule o valor total de compra de todos os produtos em estoque (quantidade * valor_compra)
SELECT SUM(quantidade_produto * valor_compra_produto) FROM tb_produtos
--Liste os fornecedores distintos cadastrados na tabela
SELECT DISTINCT fornecedor_produto FROM tb_produtos;
_______________________________________________________________________________________________________________________
Exercicio1 SQL.sql

CREATE DATABASE db_treinamento;
USE db_treinamento;

CREATE TABLE tb_clientes (
    cliente_id INT AUTO_INCREMENT PRIMARY KEY,
    cliente_nome VARCHAR(100) NOT NULL,
    cliente_email VARCHAR(100) UNIQUE NOT NULL,
    cliente_idade INT CHECK (cliente_idade >= 0),
    cliente_cidade VARCHAR(50),
    cliente_estado VARCHAR(2),
    cliente_data_cadastro DATE DEFAULT (CURDATE())
);

INSERT INTO tb_clientes (cliente_nome, cliente_email, cliente_idade, cliente_cidade, cliente_estado, cliente_data_cadastro)
VALUES 
('Ana Souza', 'ana.souza@email.com', 28, 'São Paulo', 'SP', '2024-02-01'),
('Carlos Lima', 'carlos.lima@email.com', 35, 'Rio de Janeiro', 'RJ', '2024-01-15'),
('Fernanda Oliveira', 'fernanda.oliveira@email.com', 24, 'Belo Horizonte', 'MG', '2023-12-10'),
('João Mendes', 'joao.mendes@email.com', 40, 'Curitiba', 'PR', '2024-01-05'),
('Mariana Costa', 'mariana.costa@email.com', 30, 'Fortaleza', 'CE', '2023-11-22'),
('Pedro Santos', 'pedro.santos@email.com', 22, 'Recife', 'PE', '2024-02-12'),
('Roberta Almeida', 'roberta.almeida@email.com', 27, 'Porto Alegre', 'RS', '2024-02-20'),
('Gustavo Nunes', 'gustavo.nunes@email.com', 33, 'São Paulo', 'SP', '2024-01-30'),
('Amanda Ferreira', 'amanda.ferreira@email.com', 26, 'Salvador', 'BA', '2024-01-18'),
('Diego Martins', 'diego.martins@email.com', 38, 'Manaus', 'AM', '2023-12-05'),
('Lucas Ribeiro', 'lucas.ribeiro@email.com', 29, 'Brasília', 'DF', '2023-11-28'),
('Camila Rocha', 'camila.rocha@email.com', 31, 'Natal', 'RN', '2024-02-02'),
('Bruno Cardoso', 'bruno.cardoso@email.com', 45, 'São Luís', 'MA', '2024-01-25'),
('Juliana Figueiredo', 'juliana.figueiredo@email.com', 21, 'João Pessoa', 'PB', '2024-02-10'),
('Thiago Mendes', 'thiago.mendes@email.com', 34, 'Goiânia', 'GO', '2023-12-15'),
('Patrícia Moura', 'patricia.moura@email.com', 23, 'Florianópolis', 'SC', '2024-01-08');





-- Básico
-- Selecione todos os clientes cadastrados.
SELECT * FROM tb_clientes;
-- Liste apenas os nomes e os e-mails dos clientes.
SELECT cliente_nome, cliente_email FROM tb_clientes;
-- Liste os clientes que moram no estado de São Paulo (SP).
SELECT * FROM tb_clientes WHERE cliente_estado = 'SP';
-- Encontre os clientes com idade maior que 30 anos.
SELECT * FROM tb_clientes WHERE cliente_idade > 30;
-- Liste os clientes ordenados pelo nome em ordem alfabética.
SELECT * FROM tb_clientes ORDER BY cliente_nome;
-- Mostre apenas os clientes cadastrados nos últimos 30 dias.
SELECT * FROM tb_clientes WHERE cliente_data_cadastro >= CURDATE() - INTERVAL 30 DAY;
-- Exiba os clientes que moram no Nordeste (CE, RN, MA, PB, PE).
SELECT * FROM tb_clientes WHERE cliente_estado IN ('CE', 'RN', 'MA', 'PB', 'PE');
-- Encontre todos os clientes com idade entre 25 e 35 anos.
SELECT * FROM tb_clientes WHERE cliente_idade BETWEEN 25 AND 35;
-- Selecione os clientes cujos nomes terminam com a letra "a".
SELECT * FROM tb_clientes WHERE cliente_nome LIKE '%a';
-- Liste os clientes cujo nome contém "Mendes".
SELECT * FROM tb_clientes WHERE cliente_nome LIKE '%Mendes%';
-- Intermediário
-- Encontre o cliente mais velho cadastrado.
SELECT * FROM tb_clientes ORDER BY cliente_idade DESC LIMIT 1;
-- Conte quantos clientes estão cadastrados no banco.
SELECT COUNT(*) FROM tb_clientes;
-- Liste os 5 clientes mais jovens.
SELECT * FROM tb_clientes ORDER BY cliente_idade LIMIT 5;
-- Encontre o cliente que foi cadastrado há mais tempo.
SELECT * FROM tb_clientes ORDER BY cliente_data_cadastro LIMIT 1;
-- Mostre apenas os clientes que têm mais de 30 anos e moram no estado de São Paulo.
SELECT * FROM tb_clientes WHERE cliente_idade > 30 AND cliente_estado = 'SP';
-- Liste os clientes ordenados por idade, do mais novo para o mais velho.
SELECT * FROM tb_clientes ORDER BY cliente_idade;
-- Selecione os clientes que têm "Ferreira" ou "Almeida" no nome.
SELECT * FROM tb_clientes WHERE cliente_nome LIKE '%Ferreira%' OR cliente_nome LIKE '%Almeida%';
-- Quantos clientes moram em cada estado?
SELECT cliente_estado, COUNT(*) FROM tb_clientes GROUP BY cliente_estado;
-- Selecione os clientes que foram cadastrados entre janeiro e fevereiro de 2024.
SELECT * FROM tb_clientes WHERE cliente_data_cadastro BETWEEN '2024-01-01' AND '2024-02-28';
-- Liste os clientes ordenados por data de cadastro, do mais recente ao mais antigo.
SELECT * FROM tb_clientes ORDER BY cliente_data_cadastro DESC;
-- Avançado
-- Selecione os clientes que possuem um e-mail com domínio email.com.
SELECT * FROM tb_clientes WHERE cliente_email LIKE '%@email.com';
-- Liste os clientes cujo nome tenha exatamente 10 caracteres.
SELECT * FROM tb_clientes WHERE LENGTH(cliente_nome) = 10; --Não listou nenhum cliente--;
-- Encontre os clientes que não moram nos estados SP, RJ ou MG.
SELECT * FROM tb_clientes WHERE cliente_estado NOT IN ('SP', 'RJ', 'MG');
-- Mostre os clientes agrupados por cidade e conte quantos existem em cada uma.
SELECT cliente_cidade, COUNT(*) FROM tb_clientes GROUP BY cliente_cidade;
-- Liste os clientes que possuem mais de 30 anos e foram cadastrados antes de 2024.
SELECT * FROM tb_clientes WHERE cliente_idade > 30 AND cliente_data_cadastro < '2024-01-01'; --Não listou nenhum cliente--;
-- Selecione os clientes cujo nome começa com "J" e tem idade maior que 25 anos.
SELECT * FROM tb_clientes WHERE cliente_nome LIKE 'J%' AND cliente_idade > 25;
-- Encontre os clientes que possuem exatamente 5 letras no primeiro nome.
SELECT * FROM tb_clientes WHERE LENGTH(SUBSTRING_INDEX(cliente_nome, ' ', 1)) = 5;
-- Quantos clientes têm mais de 30 anos e moram na região Sul (PR, RS, SC)?
SELECT COUNT(*) FROM tb_clientes WHERE cliente_idade > 30 AND cliente_estado IN ('PR', 'RS', 'SC');
-- Liste os clientes cujo e-mail contém o nome do cliente (exemplo: joao.mendes@email.com).
SELECT * FROM tb_clientes WHERE cliente_email LIKE CONCAT('%', cliente_nome, '%', '@%'); --Não listou nenhum cliente--;
-- Mostre os clientes que moram na mesma cidade que "Pedro Santos".
SELECT * FROM tb_clientes WHERE cliente_cidade = (SELECT cliente_cidade FROM tb_clientes WHERE cliente_nome = 'Pedro Santos');
