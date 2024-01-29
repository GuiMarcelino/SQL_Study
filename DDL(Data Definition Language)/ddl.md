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
CREATE TABLE Alunos (
  ID int,
  Nome varchar(255),
  Idade int
);

```
### Tabela de Alunos sem registros
<table>
   <tr>
    <th style="background-color: #989595;"><strong>Id</strong></th>
    <th style="background-color: #989595;"><strong>Nome</strong></th>
    <th style="background-color: #989595;"><strong>Idade</strong></th>
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
ALTER TABLE Alunos
    ADD COLUMN Email varchar(255);

-- Renomeando uma coluna:
ALTER TABLE Alunos
    RENAME COLUMN Nome TO NomeCompleto;

-- Mudando o tipo de dado de uma coluna:
ALTER TABLE Alunos
ALTER COLUMN ID TYPE bigint;

-- Mudando um índice:
ALTER INDEX idx_nome_completo
RENAME TO idx_nome_completo_aluno;

-- Mudando "Schema" pode renomear um esquema existente:
ALTER SCHEMA nome_atual
RENAME TO novo_nome;

-- Mudando  uma role (usuário ou grupo), como alterar a senha:
ALTER ROLE nome_usuario
WITH PASSWORD 'nova_senha';
```
___
## 3)```DROP (IF EXISTS)``` 
```sql
-- Excluir uma Tabela:
DROP TABLE IF EXISTS Alunos;

-- Excluir um Índice:
DROP INDEX IF EXISTS idx_nome_completo_aluno;

-- Excluir uma View:
DROP VIEW IF EXISTS view_alunos_ativos;
```

