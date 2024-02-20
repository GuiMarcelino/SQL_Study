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