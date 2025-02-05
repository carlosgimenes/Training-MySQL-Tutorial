# Guia de Referência Rápida

- Para iniciar o MySQL
```sql
sudo systemctl start mysql
```

- Para reiniciar o MySQL
```sql
sudo systemctl restart mysql
```

- Para - Parar o MySQL
```sql
sudo systemctl stop mysql
```

- Para ver o status do MySQL
```sql
sudo systemctl status mysql
```

- Para conectar-se ao MySQL
```sql
mysql -u username -p
```

- Para conectar-se ao MySQL a partir de um outro Desktop
```sql
mysql -h hostname -u username -p
```

- Para listar todos Databases
```sql
show databases;
```

Ao executar o comando ```SHOW DATABASES``` para ver os bancos de dados existentes, veremos entre outros, o banco de dados ```MySQL```. Este é o banco de dados de 
sistema. Ele mantêm as informações relativas às contas e privilégios dos usuários.

- Para listar todas tabelas de um banco de dados
```sql
show tables;
```

- Para listar informações de uma tabela
```sql
describe nometabela;
```

- Para executar um arquivo de comandos estando conectado ao monitor SQL
```sql
source nomearquivo;
```

- Para executar um arquivo de comandos NÃO estando conectado ao monitor SQL
```sql
mysql -u username -p < nomearquivo
```

- Para encerrar conexão
```sql
\q
```

- Para criar um database
```sql
create database nomedatabase;
```

- Para fazeralgumacoisa
```sql
digiteaquiocomando
