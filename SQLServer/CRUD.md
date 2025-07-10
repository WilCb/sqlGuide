# CRUD - SQL Server

## Introdução

Neste arquivo estão listados exemplos básicos de comandos CRUD (Create, Read, Update, Delete) adaptados à sintaxe do **SQL Server**. Eles são essenciais para a manipulação de dados em tabelas e estão entre as primeiras operações que todo desenvolvedor SQL deve dominar.

---

## Exemplos

### SELECT

```sql
-- Seleciona todas as colunas e registros da tabela
SELECT * FROM tabela;

-- Seleciona apenas colunas específicas da tabela clientes
SELECT NOME, CPF FROM CLIENTES;
```

### SELECT com WHERE

```sql
-- Seleciona registros onde a coluna tem valor específico
SELECT * FROM tabela WHERE coluna = 'valor';

-- Seleciona todas as colunas da tabela cliente com um CPF específico:
SELECT * FROM CLIENTES 
WHERE CPF = '12345678900';
```

### INSERT

```sql
-- Insere um novo registro na tabela
INSERT INTO tabela 
    (coluna1, coluna2)
VALUES 
    ('valor1', 'valor2');

-- Exemplo: considerando que a tabela só tenha 3 colunas
INSERT INTO CLIENTES 
    (CPF, NOME, IDADE)
VALUES 
    ('12345678900', 'João', 19);
```

### INSERT com múltiplos valores

```sql
-- Insere vários registros de uma vez
INSERT INTO tabela 
    (coluna1, coluna2)
VALUES 
    ('valor1a', 'valor2a'),
    ('valor1b', 'valor2b');
```