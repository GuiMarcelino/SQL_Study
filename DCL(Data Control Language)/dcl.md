# DCL(Data Control Language)

## Oque é DCL?
 
### - DCL (Data Control Language) inclui comandos SQL utilizados para definir permissões, controlar o acesso aos dados em um banco de dados, e gerenciar direitos e privilégios de usuários e roles. Os comandos mais comuns são GRANT, REVOKE, e DENY.

### O uso do GRANT: é para conceder privilégios específicos em objetos do banco de dados, como tabelas ou visões, para usuários ou roles. Esses privilégios podem incluir operações como SELECT, INSERT, UPDATE, DELETE, etc.

### Estrutura Básica GRANT:
```sql
GRANT permissao ON objeto TO usuario_role;
```
### Exemplo de uso do GRANT: Conceder permissão de SELECT na tabela Students para o usuário estudante.

```sql
GRANT SELECT ON Students TO estudante;
```
___

### - O uso do REVOKE: é para remover privilégios previamente concedidos de objetos do banco de dados de usuários ou roles. Essa operação é crucial para manter o controle de acesso e garantir que apenas usuários autorizados tenham permissões específicas.
___

### - Estrutura Básica REVOKE:
```sql
REVOKE permissao ON objeto FROM usuario_role;
```

### Exemplo de uso do REVOKE:
```sql
REVOKE SELECT ON Students FROM estudante;
```
___

### - Deny: O comando DENY é específico do SQL Server e não faz parte do padrão SQL utilizado pelo PostgreSQL, o PostgreSQL utiliza REVOKE para remover permissões e não tem um comando direto equivalente a DENY para negar explicitamente privilégios, em sistemas que suportam DENY, ele é usado para negar explicitamente certos privilégios a usuários ou roles, mesmo que esses privilégios tenham sido concedidos por meio de outro GRANT.