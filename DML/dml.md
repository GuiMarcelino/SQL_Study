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
-- Tabela de Alunos
CREATE TABLE Alunos (
  ID int PRIMARY KEY,
  Nome varchar(255),
  Idade int
);

-- Tabela de Cursos
CREATE TABLE Cursos (
    ID serial PRIMARY KEY,
    Nome varchar(255),
    Periodo varchar(50),
    Sala varchar(50)
);

-- Tabela Intermediária ou de junção
CREATE TABLE Alunos_Cursos (
    ID serial PRIMARY KEY,
    AlunoID int NOT NULL,
    CursoID int NOT NULL,
    FOREIGN KEY (AlunoID) REFERENCES Alunos (ID),
    FOREIGN KEY (CursoID) REFERENCES Cursos (ID)
);
```


# Explicação de cada tabela e relacionamento:

* ### Tabela de Alunos
  * ID serial PRIMARY KEY: Chave  primária e identificador do aluno.
  * Nome varchar(255): Nome do aluno.
  * Idade int: Idade do aluno.

* ### Tabela de Cursos:
  * ID serial int PRIMARY KEY: Chave  primária e identificador do curso.
  * Nome varchar(255): Nome do curso.
  * Periodo varchar(50): Período que o curso é realizado(matutino/vespertino/noturno).
  * Sala varchar(50): Sala que o curso é realizado.


* ### Tabela junção Alunos_Cursos:
  * ID serial int PRIMARY KEY: Chave  primária e identificador do relacionamento entre aluno e curso.
  * AlunoID int NOT NULL: Identificador do aluno e não pode ser nulo.
  * CursoID int NOT NULL: Identificador do curso e não pode ser nulo.
  * Sala varchar(50): Sala que o curso é realizado.
  * FOREIGN KEY (AlunoID) REFERENCES Alunos (ID): Chave estrangeira referente ao ID do aluno.
  * FOREIGN KEY (CursoID) REFERENCES Cursos (ID): Chave estrangeira referente ao ID do curso.

* ### Relacionamentos:
  * Muitos-Para-Muitos ou N para N: Este é o tipo de relacionamento que temos entre Alunos e Cursos.
  
        Aqui, um aluno pode estar matriculado em vários cursos, e um curso pode ter vários alunos.
        
        Devido à natureza complexa desse relacionamento, ele não pode ser representado diretamente no modelo relacional e requer uma tabela de junção ou uma tabela associativa, que no nosso caso é a tabela Alunos_Cursos.




