# DML(Data Manipulation Language)

## Oque é DML?
 
### - DML é um conjunto de comandos usados em bancos de dados SQL para manipular dados nas tabelas.

### Esses comandos permitem que você realize operações como inserir, atualizar, deletar e consultar dados de um banco de dados. DML é usado para gerenciar e manipular os dados propriamente ditos, não a estrutura do banco de dados.
### Exemplos:

    1-INSERT: Inserir dados

    2-UPDATE: Atualizar dados

    3-DELETE: Excluir dados

    4-SELECT: Embora tecnicamente faça parte do DQL (Data Query Language), o comando SELECT é frequentemente agrupado com DML, pois é usado para consultar e recuperar dados de uma tabela.
___


# Criando Tabelas de exemplo

```sql
-- Tabela de Students
CREATE TABLE Students (
  ID int PRIMARY KEY,
  Name varchar(255),
  Age int
);

-- Tabela de Courses
CREATE TABLE Courses (
    ID serial PRIMARY KEY,
    Name varchar(255),
    Period varchar(50),
    Classroom varchar(50)
);

-- Tabela Intermediária ou de junção
CREATE TABLE Students_Courses (
    ID serial PRIMARY KEY,
    StudentID int NOT NULL,
    CourseID int NOT NULL,
    FOREIGN KEY (StudentID) REFERENCES Students (ID),
    FOREIGN KEY (CourseID) REFERENCES Courses (ID)
);
```

# Explicação de cada tabela e relacionamento:

* ### Tabela de Students
  * ID serial PRIMARY KEY: Chave  primária e identificador do aluno.
  * Name varchar(255): Nome do aluno.
  * Age int: Idade do aluno.

* ### Tabela de Courses:
  * ID serial int PRIMARY KEY: Chave  primária e identificador do curso.
  * Name varchar(255): Nome do curso.
  * Period varchar(50): Período que o curso é realizado(matutino/vespertino/noturno).
  * Classroom varchar(50): Sala que o curso é realizado.


* ### Tabela junção Students_Courses:
  * ID serial int PRIMARY KEY: Chave  primária e identificador do relacionamento entre student e course.
  * StudentID int NOT NULL: Identificador do student e não pode ser nulo.
  * CourseID int NOT NULL: Identificador do course e não pode ser nulo.
  * FOREIGN KEY (StudentID) REFERENCES Students (ID): Chave estrangeira referente ao ID do student.
  * FOREIGN KEY (StudentID) REFERENCES Courses (ID): Chave estrangeira referente ao ID do course.

* ### Relacionamentos:
  * Muitos-Para-Muitos ou N para N: Este é o tipo de relacionamento que temos entre Students e Courses.
  
        Aqui, um student pode estar matriculado em vários courses, e um curso pode ter vários student.
        
        Devido à natureza complexa desse relacionamento, ele não pode ser representado diretamente no modelo relacional e requer uma tabela de junção ou uma tabela associativa, que no nosso caso é a tabela Students_Courses.

___

## Comando INSERT:
#### O que é INSERT?
* O comando INSERT é usado para adicionar novos registros (linhas) a uma tabela em um banco de dados. Ele permite inserir valores em uma ou mais colunas da tabela. Este comando é fundamental para adicionar dados ao banco de dados.

* A estrutura básica de um comando INSERT é a seguinte:

      nome_tabela: O nome da tabela onde os dados serão inseridos.

      (coluna1, coluna2, ...): As colunas nas quais os dados serão inseridos. Você pode omitir este especificador de coluna se estiver fornecendo valores para todas as colunas da tabela na ordem em que são definidas.

      VALUES (valor1, valor2, ...): Os valores correspondentes às colunas especificadas. Os tipos de dados dos valores devem corresponder aos tipos de dados das colunas.

    ```sql
    INSERT INTO nome_tabela (coluna1, coluna2, ...)
    VALUES (valor1, valor2, ...);
    ```

```sql
-- Adicionando Students
 INSERT INTO Student (Name, Age) VALUES 
('João', 20),
('Maria', 22),
('Carlos', 19);

-- Adicionando Courses
INSERT INTO Courses (Name, Period, Classroom) VALUES 
('Matemática', 'Manhã', '101'),
('Literatura', 'Tarde', '102'),
('Ciência', 'Manhã', '103'),
('História', 'Tarde', '104'),
('Geografia', 'Noite', '105');

-- Vinculando Student a Courses
INSERT INTO Students_Courses (StudentID, CourseID) VALUES 
(1, 1),
(1, 2),
(2, 3),
(3, 1),
(3, 2),
(3, 3),
(3, 4),
(3, 5);
```
___
## Comando UPDATE:
#### O que é UPDATE?
* O comando UPDATE é utilizado para modificar os dados existentes em uma ou mais linhas de uma tabela no banco de dados. Ele permite alterar valores de uma ou mais colunas, baseando-se em uma condição especificada.

* A estrutura básica de um comando UPDATE é a seguinte:

      nome_tabela: Nome da tabela onde os dados serão atualizados.

      SET: Especifica as colunas que serão    atualizadas e seus novos valores.

      WHERE: Define a condição para selecionar quais linhas devem ser atualizadas. Se omitido, todas as linhas da tabela serão atualizadas, o que deve ser feito com cautela.


    ```sql
    UPDATE nome_tabela
    SET coluna1 = novo_valor1, coluna2 = novo_valor2, ...
    WHERE condição;
    ```

```sql
-- Alterando dado da tabela de Students
UPDATE Students
SET Age = 21
WHERE Name = 'João';

-- Alterando dado da tabela de Courses
UPDATE Courses
SET Period = 'Manhã'
WHERE Name = 'Geografia';

-- Atualizar Múltiplas Colunas da tabela de Cursos
UPDATE Courses
SET Name = 'Matemática Avançada', Classroom = '202'
WHERE ID = 1;
```

<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">

<div class="alert-stripes">
  <strong>🚨 Dicas Importantes com UPDATE:</strong>
  <ul>
    <li><strong>Sempre use a cláusula WHERE com cautela:</strong> Se você omitir a cláusula WHERE, todas as linhas da tabela serão atualizadas, o que pode levar a alterações indesejadas e de grande escala.</li>
    <li><strong>Teste com SELECT antes:</strong> Antes de executar um UPDATE, especialmente em tabelas grandes ou críticas, você pode usar um comando SELECT com a mesma cláusula WHERE para garantir que está selecionando as linhas corretas.</li>
  </ul>
</div>
</body>
</html>

___
### Comando DELETE:
____
#### O que é DELETE?

* O comando DELETE é usado para remover um ou mais registros de uma tabela em um banco de dados. É uma ferramenta poderosa que deve ser usada com cautela, pois a exclusão de registros é uma operação permanente (a menos que o banco de dados esteja configurado para suportar operações de undo ou haja backups recentes).

* A estrutura básica de um comando DELETE é a seguinte:

      nome_tabela: O nome da tabela de onde os registros serão excluídos.

      WHERE condição: Uma condição que especifica quais registros devem ser excluídos. Se a cláusula WHERE for omitida, todos os registros da tabela serão excluídos, o que deve ser feito com extrema cautela.


    ```sql
    DELETE FROM nome_tabela
    WHERE condição;
    ```

```sql
-- Deletar um Registro Específico
DELETE FROM Students
WHERE Name = 'Rafael';

-- Deletar Registros com Condições Específicas
DELETE FROM Students
WHERE Age < 20;

-- Deletar Todos os Registros de uma Tabela
DELETE FROM Students;
```

### Registros na tabela de Students:
<table>
  <tr>
    <th style="background-color: #989595;"><strong>Id</strong></th>
    <th style="background-color: #989595;"><strong>Name</strong></th>
    <th style="background-color: #989595;"><strong>Age</strong></th>
  </tr>
  <tr>
    <td>2</td>
    <td>Maria</td>
    <td>22</td>
  </tr>
  <tr>
    <td>3</td>
    <td>Carlos</td>
    <td>19</td>
  </tr>
  <tr>
    <td>1</td>
    <td>João</td>
    <td>21</td>
  </tr>
</table>


### Registros na tabela de Courses:
<table>
  <tr>
    <th style="background-color: #989595;"><strong>Id</strong></th>
    <th style="background-color: #989595;"><strong>Name</strong></th>
    <th style="background-color: #989595;"><strong>Period</strong></th>
    <th style="background-color: #989595;"><strong>Classroom</strong></th>
  </tr>
  <tr>
    <td>2</td>
    <td>Literatura</td>
    <td>Tarde</td>
    <td>102</td>
  </tr>
  <tr>
    <td>3</td>
    <td>Ciência</td>
    <td>Manhã</td>
    <td>103</td>
  </tr>
  <tr>
    <td>4</td>
    <td>História</td>
    <td>Tarde</td>
    <td>104</td>
  </tr>
  <tr>
    <td>5</td>
    <td>Geografia</td>
    <td>Manhã</td>
    <td>105</td>
  </tr>
  <tr>
    <td>1</td>
    <td>Matemática Avançada</td>
    <td>Manhã</td>
    <td>202</td>
  </tr>
</table>


### Registros na tabela de Students_Courses:
<table>
  <tr>
    <th style="background-color: #989595;"><strong>Id</strong></th>
    <th style="background-color: #989595;"><strong>StudentID</strong></th>
    <th style="background-color: #989595;"><strong>CourseID</strong></th>
  </tr>
  <tr>
    <td>1</td>
    <td>1</td>
    <td>1</td>
  </tr>
  <tr>
    <td>2</td>
    <td>1</td>
    <td>2</td>
  </tr>
  <tr>
    <td>3</td>
    <td>2</td>
    <td>3</td>
  </tr>
  <tr>
    <td>4</td>
    <td>3</td>
    <td>1</td>
  </tr>
  <tr>
    <td>5</td>
    <td>3</td>
    <td>2</td>
  </tr>
  <tr>
    <td>6</td>
    <td>3</td>
    <td>3</td>
  </tr>
  <tr>
    <td>7</td>
    <td>3</td>
    <td>4</td>
  </tr>
  <tr>
    <td>8</td>
    <td>3</td>
    <td>5</td>
  </tr>
</table>
