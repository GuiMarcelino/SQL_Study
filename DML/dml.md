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

___

### Comando INSERT:
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
-- Adicionando Alunos
 INSERT INTO Alunos (Nome, Idade) VALUES 
('João', 20),
('Maria', 22),
('Carlos', 19);

-- Adicionando Cursos
INSERT INTO Cursos (Nome, Periodo, Sala) VALUES 
('Matemática', 'Manhã', '101'),
('Literatura', 'Tarde', '102'),
('Ciência', 'Manhã', '103'),
('História', 'Tarde', '104'),
('Geografia', 'Noite', '105');

-- Vinculando Alunos a Cursos
INSERT INTO Alunos_Cursos (AlunoID, CursoID) VALUES 
(1, 1),
(1, 2),
(2, 3),
(3, 1),
(3, 2),
(3, 3),
(3, 4),
(3, 5);
```

### Comando UPDATE:
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
-- Alterando dado da tabela de Alunos
UPDATE Alunos
SET Idade = 21
WHERE Nome = 'João';

-- Alterando dado da tabela de Cursos
UPDATE Cursos
SET Periodo = 'Tarde'
WHERE Periodo = 'Manhã';

-- Atualizar Múltiplas Colunas da tabela de Cursos
UPDATE Cursos
SET Nome = 'Matemática Avançada', Sala = '202'
WHERE ID = 1;
```
