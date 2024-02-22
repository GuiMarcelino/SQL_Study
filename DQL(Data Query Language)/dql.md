# DQL(Data Query Language)

## Oque é DML?
 
### - DQL é uma parte da linguagem SQL usada para realizar consultas em bancos de dados. O comando mais comum em DQL é o SELECT, que é utilizado para buscar e recuperar dados de uma ou mais tabelas.


* Aqui está a estrutura básica de uma consulta SELECT:

      SELECT column1, column2, ...
      FROM table_name
      WHERE condition
      ORDER BY column;


* SELECT: Especifica as colunas que serão recuperadas na consulta.

* FROM: Indica a(s) tabela(s) de onde os dados serão selecionados.

* WHERE: Filtra os registros baseados em uma condição específica.

* ORDER BY: Organiza os resultados de acordo com uma coluna específica.

## Para a explicação e exemplos vamos utilizar as seguintes tabelas:
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
  <tr>
    <td>1</td>
    <td>Miguel</td>
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

## Exemplos Práticos Estrutura básica do SELECT:

* Selecionando Todas as colunas da tabela Students:
```sql
  SELECT * FROM Students;
```
* Selecionando colunas específicas da tabela Students:
```sql
  SELECT Name, Age FROM Students;
```
* Selecionando colunas utilizando condição WHERE na tabela Students:
```sql
  SELECT * FROM Students WHERE Age > 20;
```
* Ordenando pelo campo age na tabela Students:
```sql
  SELECT * FROM Students ORDER BY Age;
```

## O que são Joins?
 
### - JOINs são comandos em SQL que permitem unir dados de duas ou mais tabelas, com base em uma coluna relacionada entre elas. Imagine que cada tabela é como uma lista separada e JOIN é uma maneira de combinar essas listas em uma só, com base em critérios comuns.

## Tipos de Joins?

### - INNER JOIN  é usado para combinar registros de duas tabelas baseando-se em uma condição de correspondência. Somente os registros que atendem à condição de correspondência nas duas tabelas são incluídos no resultado final, então retorna linhas quando há pelo menos uma correspondência em ambas as tabelas.

* Consulta simples, vamos usar apenas a relação entre duas tabelas: Students e Students_Courses. A tabela Students possui informações sobre os alunos, e Students_Courses tem informações sobre quais cursos os alunos estão matriculados:

      Neste comando SQL, estamos fazendo o seguinte:

      SELECT Students.Name: Estamos pedindo para que o resultado mostre apenas o nome dos alunos.

      FROM Students: Indicamos que a tabela principal que estamos usando é a Students.

      INNER JOIN Students_Courses ON Students.ID = Students_Courses.StudentID: Estamos dizendo para juntar a tabela Students com a tabela Students_Courses onde o campo ID da tabela Students corresponde ao campo StudentID da tabela Students_Courses, ou seja vai retornar os nomes dos alunos(João,João, Maria, Carlos), não retorna o aluno (Miguel) pois ele não esta vinculado a nenhum curso, perceba que retornar 2 vezes o nome do aluno (João).

      A consulta com INNER JOIN retorna registros duplicados quando existem múltiplas correspondências na tabela com a qual está sendo feita a junção. No caso do aluno "João", ele aparece duas vezes porque está matriculado em dois cursos diferentes.

```sql
SELECT Students.Name
FROM Students
INNER JOIN Students_Courses ON Students.ID = Students_Courses.StudentID;
```

* Alunos e seus cursos com filtragem por idade:
```sql
SELECT 
  Students.Name AS StudentName,
  Courses.Name AS CourseName
FROM 
  Students
INNER JOIN 
  Students_Courses ON Students.ID = Students_Courses.StudentID
INNER JOIN 
  Courses ON Students_Courses.CourseID = Courses.ID
WHERE 
  Students.Age > 20;
```

* Alunos e seus cursos com filtragem por período do curso:
```sql
SELECT 
  Students.Name AS StudentName, 
  Courses.Name AS CourseName
FROM 
  Students
INNER JOIN 
  Students_Courses ON Students.ID = Students_Courses.StudentID
INNER JOIN 
  Courses ON Students_Courses.CourseID = Courses.ID
WHERE 
  Courses.Period = 'Manhã';
```

* Alunos e seus cursos com múltiplas condições:
```sql
SELECT 
  Students.Name AS StudentName, 
  Courses.Name AS CourseName
FROM 
  Students
INNER JOIN 
  Students_Courses ON Students.ID = Students_Courses.StudentID
INNER JOIN 
  Courses ON Students_Courses.CourseID = Courses.ID
WHERE 
  Students.Age > 20 AND Courses.Period = 'Manhã';
```