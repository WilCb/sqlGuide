# CRUD - SQL Server

## Introdução

Neste arquivo estão listados exemplos básicos de comandos CRUD (**Create, Read, Update, Delete**) adaptados à sintaxe do **SQL Server**. Eles são essenciais para a manipulação de dados em tabelas e estão entre as primeiras operações que todo desenvolvedor SQL deve dominar.

---

## Exemplos

### CREATE TABLE *(essa parte será melhor detalhada em outro tópico futuramente)*

```sql
-- Cria uma nova tabela chamada "CLIENTES"
CREATE TABLE CLIENTES (
    ID INT PRIMARY KEY IDENTITY(1,1), -- Auto incremento
    NOME NVARCHAR(100) NOT NULL,
    EMAIL NVARCHAR(150) UNIQUE,
    CPF CHAR(11) UNIQUE,
    IDADE INT
);
```
> ℹ️ Para mais informações sobre restrições como IDENTITY, NOT NULL, UNIQUE, consulte o arquivo [CONTRAINTS.md](./CONSTRAINTS.md)

### SELECT

```sql
-- Seleciona todas as colunas e registros da tabela
SELECT * FROM CLIENTES;

-- Seleciona apenas colunas específicas
SELECT NOME, CPF FROM CLIENTES;
```

### SELECT com WHERE

```sql
-- Seleciona registros onde a coluna tem valor específico
SELECT * FROM CLIENTES WHERE CPF = '12345678900';
```

### INSERT

```sql
-- Insere um novo registro na tabela
INSERT INTO CLIENTES 
    (NOME, EMAIL, CPF, IDADE)
VALUES 
    ('João', 'joao@email.com', '12345678900', 19);
```

### INSERT com múltiplos valores

```sql
-- Insere vários registros de uma vez
INSERT INTO CLIENTES 
    (NOME, EMAIL, CPF, IDADE)
VALUES 
    ('Maria', 'maria@email.com', '11111111111', 25),
    ('Carlos', 'Carlos@email.com', '22222222222', 33);
```

> 📌 Importante: a ordem dos valores deve corresponder exatamente à ordem das colunas declaradas.

```sql
-- Insere vários registros omitindo a declaração de colunas
INSERT INTO CLIENTES
VALUES 
    ('Ana', 'ana@email.com', '33333333333', 29),
    ('Pedro', 'pedro@email.com', '44444444444', 40);
```
> ⚠️ Atenção: só use essa forma quando tiver certeza absoluta da ordem das colunas na tabela e que nenhuma delas é gerada automaticamente (como ID com IDENTITY).

### UPDATE

```sql
-- Atualiza valores de colunas com base em uma condição
UPDATE CLIENTES
SET NOME = 'João Paulo'
WHERE CPF = '12345678900';
```

### DELETE
```sql
-- Remove registros com base em uma condição
DELETE FROM CLIENTES
WHERE CPF = '12345678900';
```
> ⚠️ Atenção: Sempre utilize WHERE com o comando DELETE. Sem ele, todos os dados da tabela poderão ser excluídos.