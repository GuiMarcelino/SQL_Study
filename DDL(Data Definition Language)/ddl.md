# DDL(Data Definition Language)

## Oque é DDL?
 
### - DDL é uma parte que trata da definição e modificação da estrutura de dados de um banco de dados.
### Exemplos:
    1-CREATE
    2-ALTER
    3-DROP (IF EXISTS)
___
## 1)```Create``` Usado para criar uma nova tabela.

```sql
CREATE TABLE Students (
  ID int,
  Nome varchar(255),
  Idade int
);

```
### Tabela de Students sem registros
<table>
   <tr>
    <th style="background-color: #989595;"><strong>Id</strong></th>
    <th style="background-color: #989595;"><strong>Name</strong></th>
    <th style="background-color: #989595;"><strong>Age</strong></th>
  </tr>
  <tr>
    <td>1</td>
    <td>Marcos Silva</td>
    <td>41</td>
  </tr>
  <tr>
    <td>2</td>
    <td>Ana Clara</td>
    <td>27</td>
  </tr>
</table>

___
## 2)```Alter``` Usado para fazer mudanças em uma tabela existente.
```sql
-- Adicionando uma nova coluna:
ALTER TABLE Students
    ADD COLUMN Email varchar(255);

-- Renomeando uma coluna:
ALTER TABLE Students
    RENAME COLUMN Name TO FullName;

-- Mudando o tipo de dado de uma coluna:
ALTER TABLE Students
ALTER COLUMN ID TYPE bigint;

-- Mudando um índice:
ALTER INDEX idx_full_name
RENAME TO idx_full_name_student;

-- Mudando "Schema" pode renomear um esquema existente:
ALTER SCHEMA current_name
RENAME TO new_name;

-- Mudando  uma role (usuário ou grupo), como alterar a senha:
ALTER ROLE new_user
WITH PASSWORD 'new_password';
```
___
## 3)```DROP (IF EXISTS)``` 
```sql
-- Excluir uma Tabela:
DROP TABLE IF EXISTS Students;

-- Excluir um Índice:
DROP INDEX IF EXISTS idx_full_name_student;

-- Excluir uma View:
DROP VIEW IF EXISTS view_active_students;
```

