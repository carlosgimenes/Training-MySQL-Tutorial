# Training Leitura Livro - MySQL Tutorial Uma introdução objetiva aos fundamentos do banco de dados MySQL

## Você pode fazer o download do MySQL em

[Link para Página de Download](https://dev.mysql.com/downloads/mysql/)

## Como instalar o MySQL no Linux

Segui os passos na documentação existente no site.

[Link para página com Passo a Passo](https://dev.mysql.com/doc/refman/8.4/en/linux-installation-debian.html)

## Como configurar o seu sistema

Creio que em função da versão utilizada no livro ser muito antiga, alguns passos que recomendava realizar, não foi necessário executar, versão atual parece ter corrigido e por isso não encontrei referências.

A instalação como realizei, _**obrigou**_ a definir a senha para o usuário _**root**_, no livro isto foi definido posteriormente, uma vez que não obrigava.

## Como excluir as contas anônimas

Na versão que instalei (8.4), não encontrei usuários nesta condição.

## Como criar uma conta para o uso básico

A sintaxe fornecida no livro não é mais suportada, a sintaxe que utilizei foi:

```sql
CREATE USER 'nomeusuario'@'%' IDENTIFIED BY 'MinhaSenha123';
GRANT CREATE, CREATE TEMPORARY TABLES, DELETE, EXECUTE, INDEX, INSERT, LOCK TABLES, SELECT, SHOW DATABASES, UPDATE ON *.* TO 'nomeusuario'@'%';
FLUSH PRIVILEGES;
```

Agora devo primeiro criar o usuário e depois conceder os privilégios.
