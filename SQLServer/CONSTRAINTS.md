# CONSTRAINTS - SQL Server

## Introdução

Constraints (ou **restrições**) são regras aplicadas a colunas ou tabelas que ajudam a garantir a integridade dos dados no banco. No **SQL Server**, você pode aplicar essas restrições durante a criação ou alteração de tabelas.

---

## Tipos de Constraints

- `PRIMARY KEY` – Garante que os valores sejam únicos e não nulos (identificador da tabela)
- `FOREIGN KEY` – Garante a integridade referencial entre tabelas
- `NOT NULL` – Garante que a coluna não aceite valores nulos
- `UNIQUE` – Garante que os valores sejam únicos na coluna
- `CHECK` – Garante que os valores obedeçam a uma condição lógica
- `DEFAULT` – Define um valor padrão para a coluna

---

## Exemplos

### PRIMARY KEY + IDENTITY

```sql
-- Cria uma tabela com chave primária e auto incremento
CREATE TABLE CLIENTES (
    ID INT PRIMARY KEY IDENTITY(1,1), -- Auto incremento começa em 1 e incrementa de 1 em 1
    NOME NVARCHAR(100) NOT NULL
);

-- Também é possível criar desta forma:
CREATE TABLE CLIENTES (
    ID INT IDENTITY(1,1), -- Auto incremento
    NOME NVARCHAR(100) NOT NULL,
    PRIMARY KEY (ID)
);
```

### FOREIGN KEY

```sql
-- Cria duas tabelas e estabelece uma chave estrangeira
CREATE TABLE CLIENTES (
    ID INT PRIMARY KEY IDENTITY(1,1),
    NOME NVARCHAR(100)
);

CREATE TABLE PEDIDOS (
    ID INT PRIMARY KEY IDENTITY(1,1),
    CLIENTE_ID INT,
    FOREIGN KEY (CLIENTE_ID) REFERENCES CLIENTES(ID)
);
```
> 📌 Isso impede, por exemplo, que um pedido seja registrado para um cliente inexistente.

### NOT NULL
```sql
-- Garante que a coluna não aceite valores nulos
CREATE TABLE PRODUTOS (
    ID INT PRIMARY KEY,
    NOME NVARCHAR(100) NOT NULL
);
```

### UNIQUE
```sql
-- Garante que os valores da coluna sejam únicos
CREATE TABLE USUARIOS (
    ID INT PRIMARY KEY,
    EMAIL NVARCHAR(150) UNIQUE
);
```
> ⚠️ A diferença entre PRIMARY KEY e UNIQUE é:
> - "PRIMARY KEY não aceita valores nulos e só pode haver uma por tabela."
> - "UNIQUE aceita valores nulos e pode haver várias por tabela (desde que em colunas diferentes)."

### CHECK

```sql
-- Restringe os valores aceitos por uma coluna
CREATE TABLE FUNCIONARIOS (
    ID INT PRIMARY KEY,
    SALARIO DECIMAL(10,2) CHECK (SALARIO > 0)
);

-- Outro exemplo: não permite cadastrar um cliente menor de 18 anos
CREATE TABLE TAB_CHECK (
    ID INT NOT NULL,
    NOME VARCHAR(50),
    IDADE INT,
    CIDADE VARCHAR(50),
    CONSTRAINT CHK_IDADE CHECK (IDADE >= 18)
);
```

### DEFAULT
```sql
-- Define um valor padrão para uma coluna
CREATE TABLE CLIENTES (
    ID INT PRIMARY KEY,
    NOME NVARCHAR(100),
    ATIVO BIT DEFAULT 1
);
```
> Se o valor de ATIVO não for informado na inserção, o padrão será 1 (ativo).

### Adicionando Constraints após a criação da tabela

```sql
-- Adiciona uma constraint UNIQUE a uma coluna existente
ALTER TABLE USUARIOS
ADD CONSTRAINT UQ_Email UNIQUE (EMAIL);

-- Adiciona uma constraint CHECK
ALTER TABLE FUNCIONARIOS
ADD CONSTRAINT CK_SalarioPositivo CHECK (SALARIO > 0);
```

### Removendo Constraints

```sql
-- Remove uma constraint pelo nome
ALTER TABLE FUNCIONARIOS
DROP CONSTRAINT CK_SalarioPositivo;
```

> 📌 Use a system view INFORMATION_SCHEMA.TABLE_CONSTRAINTS para ver as constraints existentes.
> ```sql
>SELECT * 
>FROM INFORMATION_SCHEMA.TABLE_CONSTRAINTS
>WHERE TABLE_NAME = 'NOME_DA_SUA_TABELA';
> ```

Veja também sobre TIPOS.md para os tipos do SQLServer