# **Training Leitura Livro - MySQL Tutorial: Uma Introdução Objetiva aos Fundamentos do Banco de Dados MySQL**

## A estrutura de diretórios do MySQL

Na instalação que realizei para a versão 8.4, a estrutura é a seguinte:

1. **Diretório de instalação**: `/usr/share/mysql-8.4`
2. **Diretório de dados**: `/var/lib/mysql`
3. **Diretório de configuração**: `/etc/mysql`
4. **Diretório de logs**: `/var/log/mysql`
5. **Diretório de binários**: `/usr/bin/mysql`

## Uma visão geral dos executáveis

1. **mysqladmin**:
    - **Descrição**: Ferramenta de administração do MySQL que permite executar várias operações administrativas, como redefinir a senha do usuário, iniciar/parar o servidor, verificar o status do servidor, entre outras.
    - **Status**: Ainda é amplamente utilizado.

2. **myisamchk**:
    - **Descrição**: Ferramenta para verificar, reparar e otimizar tabelas MyISAM. Essas operações são úteis para manter a integridade e o desempenho das tabelas MyISAM.
    - **Status**: Ainda é utilizado, mas as tabelas MyISAM têm sido cada vez mais substituídas por tabelas InnoDB, que oferecem melhor desempenho e recursos.

3. **mysqldump**:
    - **Descrição**: Utilitário para criar backups de bancos de dados MySQL. Ele gera scripts SQL que podem ser usados para recriar o banco de dados e seus dados.
    - **Status**: Ainda é amplamente utilizado para backups e migrações de bancos de dados.

4. **mysqlbinlog**:
    - **Descrição**: Ferramenta para ler arquivos binários de log do MySQL. Esses logs contêm todas as instruções SQL que alteraram os dados, e a ferramenta pode ser usada para replicação e recuperação de dados.
    - **Status**: Ainda é utilizado, especialmente em configurações de replicação e para recuperação de dados.

5. **mysqlshow**:
    - **Descrição**: Ferramenta para mostrar informações sobre bancos de dados, tabelas e colunas do MySQL. É útil para obter uma visão rápida da estrutura do banco de dados.
    - **Status**: Ainda é utilizado, embora outras ferramentas como `SHOW DATABASES` e `SHOW TABLES` também sejam comumente usadas para obter informações semelhantes.

## Uma visão geral das interfaces do usuário

No MySQL, você tem várias opções para a interface do usuário. As interfaces do usuário mais populares são a interface da linha de comandos `mysql` (também conhecida como monitor MySQL) e o phpMyAdmin.

O monitor MySQL vem com a sua instalação básica. É uma interface de linha de comando, sempre disponível como uma opção. É simples de usar e funciona em todas as plataformas.

O phpMyAdmin é uma interface baseada na web para usar o MySQL. É muito popular entre os provedores de internet que fornecem o MySQL para o desenvolvimento de aplicações web.

Se você tiver o MySQL instalado, já terá, também, o monitor MySQL. No entanto, caso esteja utilizando um desktop para acessar um MySQL que esteja rodando em um servidor remoto, você pode fazer a instalação do `mysql client`.

## Instalação do monitor MySQL (mysql client) em um desktop Linux Ubuntu sem instalar o servidor MySQL

1. **Atualize os pacotes do sistema**:

```bash
sudo apt update
```

2. **Instale apenas o cliente MySQL**:

```bash
sudo apt install mysql-client
```

3. **Conecte-se ao servidor MySQL remoto**:

```bash
mysql -u seu_usuario -p -h endereco_do_servidor
```

Isso permitirá que você utilize o cliente MySQL em seu desktop Ubuntu para executar consultas SQL no servidor remoto sem precisar instalar o servidor MySQL localmente.

## Uma introdução rápida ao monitor MySQL

Agora, um pouco sobre o básico do monitor MySQL.

### Conexões

- **Conexão local com o `mysql`**:

```bash
mysql -u username -p
```

- **Conexão remota com o `mysql`**:

```bash
mysql -h hostname -u username -p
```

### Comandos Básicos

- Para visualizar os bancos de dados disponíveis:

```sql
SHOW DATABASES;
```

- Para selecionar um banco de dados:

```sql
USE nomebancodedados;
```

- Para visualizar as tabelas em um banco de dados selecionado:

```sql
SHOW TABLES;
```

- Para obter informações sobre uma tabela específica:

```sql
DESCRIBE nomedatabela;
```

- Para executar um arquivo de comandos estando conectado:

```sql
SOURCE nomedoarquivo;
```

- Para executar um arquivo de comandos sem estar conectado:

```bash
mysql -u username -p < nomedoarquivo;
```

- Para sair do monitor MySQL:

```sql
\q
```

Estas são as informações básicas para iniciar a utilização do programa `mysql`.

---
