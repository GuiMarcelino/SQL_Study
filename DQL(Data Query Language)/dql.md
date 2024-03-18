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

### - O RIGHT JOIN é uma operação em SQL usada para combinar e retornar linhas de duas ou mais tabelas. 

### A peculiaridade do RIGHT JOIN é que ele retorna todas as linhas da tabela à direita (a segunda tabela mencionada na consulta) e as linhas correspondentes da tabela à esquerda (a primeira tabela). Quando não há correspondências entre as tabelas, o RIGHT JOIN preenche as colunas da tabela à esquerda com valores NULL.

    Exemplo:

    Temos duas tabelas (Students) e (Courses).
    
    Queremos listar todos os cursos disponíveis e, se algum aluno estiver matriculado nesses cursos, você também quer mostrar os nomes desses alunos.
    
    Se um curso não tiver alunos matriculados, você ainda quer listar o curso, mas a coluna do aluno ficará como (NULL).

    Atenção: Por esse motivo Right join não deve ser utilizado quando vc quer obter resultados que tenha correspondência nas duas tabelas.

## Estrutura Básica Right Join:
### SELECT colunas: Especifica quais colunas você deseja selecionar para o resultado.

- FROM tabela1: A primeira tabela da qual você quer combinar dados.

- RIGHT JOIN tabela2: A segunda tabela que você quer garantir que todas as linhas sejam retornadas.

- ON tabela1.coluna = tabela2.coluna: A condição que estabelece como as duas tabelas devem ser unidas.


```sql
SELECT colunas
FROM tabela1
RIGHT JOIN tabela2 ON tabela1.coluna = tabela2.coluna;
```

* Se quisermos listar todos os cursos junto com os alunos matriculados, usaríamos:

```sql
SELECT Courses.Name AS Curso, Students.Name AS Aluno
FROM Courses
RIGHT JOIN Students_Courses ON Courses.ID = Students_Courses.CourseID
RIGHT JOIN Students ON Students_Courses.StudentID = Students.ID;
```

### - O LEFT JOIN é uma operação em SQL usada para combinar e retornar linhas de duas ou mais tabelas. 

### A particularidade do LEFT JOIN é que ele retorna todas as linhas da tabela à esquerda (a primeira tabela mencionada na consulta) e as linhas correspondentes da tabela à direita (a segunda tabela). Quando não existem correspondências na tabela à direita para linhas na tabela à esquerda, o LEFT JOIN preenche as colunas da tabela à direita com valores NULL.

## Estrutura Básica Left Join:
### SELECT colunas: Especifica quais colunas você deseja selecionar para o resultado.

- SELECT colunas: Especifica as colunas que você deseja incluir no resultado.

- FROM tabela1: Indica a tabela principal de onde os dados serão selecionados inicialmente.

- LEFT JOIN tabela2 ON tabela1.coluna = tabela2.coluna: Define como as tabelas serão unidas, garantindo que todas as linhas da tabela à esquerda sejam retornadas, juntamente com as linhas correspondentes da tabela à direita.


```sql
SELECT colunas
FROM tabela1
LEFT JOIN tabela2 ON tabela1.coluna = tabela2.coluna;
```

* Para listar todos os alunos e seus cursos, alterando o foco do RIGHT JOIN para LEFT JOIN, a consulta seria adaptada da seguinte forma:

```sql
SELECT Students.Name AS Aluno, Courses.Name AS Curso
FROM Students
LEFT JOIN Students_Courses ON Students.ID = Students_Courses.StudentID
LEFT JOIN Courses ON Students_Courses.CourseID = Courses.ID;
```

### - O GROUP BY é usado no SQL para agrupar registros que têm valores iguais em determinadas colunas

### Geralmente usamos para agrupar e contar algum dado ou tirar alguma média.

## Estrutura Básica GROUP BY:
```sql
SELECT coluna1, function(coluna2)
FROM tabela
GROUP BY coluna1;
```

### Aqui é um exemplo concetro do comando, contar quantos estudantes estão inscritos em cada curso na tabela Students_Courses:
 - **CourseID** é a coluna pela qual estamos agrupando.

 - **COUNT(StudentID)** é a função de agregação que conta o número de estudantes para cada CourseID.

 - **Students_Courses** é a tabela de onde os dados são selecionados.

```sql
SELECT CourseID, COUNT(StudentID)
FROM Students_Courses
GROUP BY CourseID;
```

### - O HAVING é usado para filtrar grupos criados pelo GROUP BY Geralmente usamos o HAVING para aplicar condições sobre resultados agregados, como contagens ou médias, permitindo incluir apenas grupos específicos nos resultados finais.

### Diferente da cláusula WHERE, que filtra linhas individuais antes da operação de agrupamento, o HAVING permite aplicar filtros depois que os grupos foram formados, isso significa que o HAVING é essencialmente inútil sem um GROUP BY, porque sua função é filtrar grupos, e sem o GROUP BY, não há grupos para filtrar.

## Estrutura Básica HAVING:
```sql
SELECT coluna1, AVG(coluna2)
FROM tabela
WHERE coluna2 > 10;
```

 - **CourseID** é a coluna pela qual estamos agrupando.

 - **COUNT(StudentID)** é a função de agregação que conta o número de estudantes para cada CourseID.

 - **HAVING COUNT(StudentID) > 5** é a condição que filtra apenas os grupos (cursos) que têm mais de 5 estudantes inscritos.

 - **Students_Courses** é a tabela de onde os dados são selecionados.

### Aqui está um exemplo concreto do comando: filtrar cursos que têm mais de 5 estudantes inscritos, na tabela Students_Courses:

```sql
SELECT CourseID, COUNT(StudentID) AS NumberOfStudents
FROM Students_Courses
GROUP BY CourseID
HAVING COUNT(StudentID) > 5;
```
### - (LIMIT e OFFSET) A cláusula LIMIT é simples e direta: ela instrui o banco de dados a retornar no máximo o número especificado de registros da consulta. Neste exemplo, estamos solicitando apenas os nomes dos primeiros 5 estudantes da tabela Students. Isso pode ser útil, por exemplo, se você quiser mostrar uma lista prévia ou realizar uma análise rápida de um subconjunto de dados.

### - O LIMIT é especialmente útil em interfaces de usuário que exibem dados em páginas, onde você quer mostrar uma quantidade fixa de registros por página. Em conjunto com a cláusula OFFSET, você pode navegar através de grandes conjuntos de dados em partes mais gerenciáveis.

### Uso com OFFSET para Paginação, além do LIMIT, você pode usar a cláusula OFFSET para pular um número específico de registros antes de começar a retornar os registros. Isso é comum em sistemas de paginação:

## Estrutura Básica LIMIT:
```sql
SELECT colunas
FROM tabela
LIMIT numero;
```

## Estrutura Básica LIMIT e OFFSET:
```sql
SELECT colunas
FROM tabela
LIMIT numero OFFSET numero;
```
### OFFSET 10 diz ao banco de dados para pular os primeiros 10 registros. Após pular esses registros, o LIMIT 5 aplicará, retornando os próximos 5 registros após os primeiros 10, isso é útil para implementar a paginação, onde, por exemplo, você quer mostrar a terceira página de resultados, assumindo que cada página mostra 5 registros exemplo:

```sql
SELECT Name
FROM Students
LIMIT 5 OFFSET 10;
```