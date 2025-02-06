# **MySQL Tutorial: Uma Introdução Objetiva aos Fundamentos do Banco de Dados MySQL**

## Capítulo 1 - Como instalar o MySQL

### Onde baixar o MySQL

Você pode fazer o download do MySQL no [site oficial](https://dev.mysql.com/downloads/mysql/).

### Instalação do MySQL no Linux

Siga os passos fornecidos na documentação oficial para a instalação no Linux: [Guia de Instalação](https://dev.mysql.com/doc/refman/8.4/en/linux-installation-debian.html).

### Instalação do MySQL no Windows

Siga os passos fornecidos na documentação oficial para a instalação no Windows: [Guia de Instalação](https://dev.mysql.com/doc/refman/8.4/en/windows-installation.html).

### Configuração do Sistema

É interessante observar que, devido à disparidade entre a versão usada no livro e a versão mais recente, alguns passos se tornaram obsoletos. A versão atual automatiza algumas configurações que anteriormente eram manuais, incluindo a obrigatoriedade de definir uma senha para o usuário `root` durante a instalação, enquanto no passado isso era feito posteriormente.

### Exclusão de Contas Anônimas

Na versão 8.4, não foram encontradas contas anônimas por padrão, o que facilita o processo de configuração inicial.

### Criação de Conta para Uso Básico

A sintaxe para criar usuários e conceder privilégios foi atualizada. Utilizei os seguintes comandos:

```sql
CREATE USER 'username'@'%' IDENTIFIED BY '<SENHA_FORTE>';
GRANT CREATE, CREATE TEMPORARY TABLES, DELETE, EXECUTE, INDEX, INSERT, LOCK TABLES, SELECT, SHOW DATABASES, UPDATE ON *.* TO 'username'@'%';
FLUSH PRIVILEGES;
```

Primeiro, criamos o usuário e, em seguida, concedemos os devidos privilégios.

---
