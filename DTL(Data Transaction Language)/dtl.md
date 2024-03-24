# DTL(Data Transaction Language)

## Oque é DTL?
 
### - DTL (Data Transaction Language) é uma parte da linguagem SQL que lida com o controle de transações em um banco de dados, transações são cruciais para manter a integridade e a confiabilidade dos dados, pois permitem que múltiplas operações de banco de dados sejam executadas ou revertidas como uma única unidade lógica.

### Estrutura Básica TRANSACTION:
```sql
BEGIN; -- Inicia a transação
-- Operações SQL como INSERT, UPDATE, DELETE
COMMIT; -- Aplica as alterações ao banco de dados se tudo estiver correto
-- ou
ROLLBACK; -- Desfaz as alterações se houver algum erro nas operações
```
### Exemplo de transação simples:

```sql
BEGIN;
UPDATE Accounts SET balance = balance - 100 WHERE id = 1;
UPDATE Accounts SET balance = balance + 100 WHERE id = 2;
COMMIT;
```

### O uso do COMMIT: deve ser utilizado após a execução das operações desejadas, e quando você quer tornar permanentes essas operações.
___

### - Estrutura Básica COMMIT:
```sql
BEGIN;
-- Operações SQL
COMMIT; -- Confirma todas as operações desde o BEGIN
```

### Exemplo de Transação com COMMIT:
```sql
BEGIN;
-- Insere a matrícula do aluno no curso 2
INSERT INTO Students_Courses (StudentID, CourseID) VALUES (1, 2);
-- Insere a matrícula do aluno no curso 3
INSERT INTO Students_Courses (StudentID, CourseID) VALUES (1, 3);
COMMIT; -- Confirma as operações, efetivando as matrículas
```

### O uso do ROLLBACK: para desfazer as operações realizadas na transação atual se detectar um erro ou se desejar cancelar a transação por qualquer outro motivo.
___

### - Estrutura Básica ROLLBACK:
```sql
BEGIN;
-- Operações SQL
ROLLBACK; -- Desfaz todas as operações desde o BEGIN
```

### Exemplo de Transação com COMMIT:
```sql
BEGIN;
-- Insere a matrícula do aluno no curso 4
INSERT INTO Students_Courses (StudentID, CourseID) VALUES (1, 4);
-- Insere a matrícula do aluno no curso 5
INSERT INTO Students_Courses (StudentID, CourseID) VALUES (1, 5);
ROLLBACK; -- Desfaz as operações, cancelando as matrículas
```