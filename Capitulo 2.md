# **Training Leitura Livro - MySQL Tutorial: Uma Introdução Objetiva aos Fundamentos do Banco de Dados MySQL**

## A estrutura de diretórios do MySQL

Na instalação que realizei para a versão 8.4 tem a seguinte estrutura:

1. **Diretório de instalação**: `/usr/share/mysql-8.4`
2. **Diretório de dados**: `/var/lib/mysql`
3. **Diretório de configuração**: `/etc/mysql`
4. **Diretório de logs**: `/var/log/mysql`
5. **Diretório de binários**: `/usr/bin/mysql`

## Uma visão geral dos executáveis

1. **mysqladmin**:

- **Descrição**: Ferramenta de administração do MySQL que permite executar várias operações administrativas, como redefinir a senha do usuário, iniciar/parar o servidor, verificar o status do servidor, etc.
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

## Uma introdução rápida ao monitor MySQL

Instalação do monitor MySQL (mysql client) em um desktop Linux Ubuntu sem instalar o servidor MySQL.

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
