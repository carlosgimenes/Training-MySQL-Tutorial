# **Tutorial MySQL: Uma Introdução Objetiva aos Fundamentos do Banco de Dados MySQL**

## Capítulo 4 - Como criar banco de dados, tabelas e índices

### SQL significa Structured Qurey Language

- É a linguagem usada para a criação e consulta de banco de dados relacionais.

### Data Definition Language ou DDL

- É a Linguagem de Definição de Dados, utilizada para criação das estruturas do banco de dados.

### Data Manipulation Language ou DML

-É a Linguagem de Manipulação de Dados, utilizada para a manipulação do banco de dados.

## Letras maiúsculas e minúsculas

As palavras-chaves no SQL não levam em conta o case sensitive, ou seja, a diferença entre as letras maiúsculas e minúsculas.

No MySQL, o sistema operacional utilizado é que definirá se os nomes do banco de dados e das tabelas levarão em conta a diferença entre letras maiúsculas e minúsculas.

A razão disto é que, geralmente, cada banco de dados terá um diretório subjacente em seu sistema operacional e cada tabela terá um arquivo subjacente. Estes nomes  de diretórios e arquivos seguem regras que dependem do sistema operacional.

Para diminuir a confusão, é uma boa prática tratar todos os identificadores como case sensitive, mesmo que você esteja trabalhando em um sistema Windows. Isto permitirá trocar de uma plataforma para outra facilmente.

## Identificadores no MySQL

Um identificador é simplesmente o nome de um alias, um banco de dados, uma tabela, uma coluna ou um índice. É como você identifica com exclusividade este objeto.
Em geral os identificadores podem conter qualquer caractere, com estas exceções:

- Eles não podem conter caracteres de aspas, ASCII(0) e ASCII(255).
- Os nomes do banco de dados podem conter qualquer caractere permitido em um nome de diretório, mas não os caracteres que possuem um significado especial em nome de diretório (`/`, `\` e `.`) por razões óbvias.
- Os nomes da tabela podem conter qualquer caractere permitido nos nomes de arquivo, exceto `.` e `/`.

Todos os identificadores, exceto os alias, podem ser configurados para terem 64 caracteres de comprimento. Os nomes de alias podem ter até 255 caracteres de comprimento.

## Como criar um banco de dados

Fazemos isso com a instrução SQL ``CREATE DATABASE``

```sql
create database nomedatabase;
```

Podemos verificar se a instrução funcionou corretamente executando o comando

```sql
show databases;
```

## Como selecionar um banco de dados

Antes de criar uma tabela ou fazer qualquer coisa com o banco de dados, precisamos informar ao MySQL que desejamos trabalhar com ele. Fazemos isto com a instrução `use`:

```sql
use nomedatabase
```

O banco de dados _**nomedatabase**_ agora está selecionado e todas as ações que tomarmos de agora em diante serão aplicadas nele, por padrão.

## Como criar tabelas

Para criarmos uma tabela, usamos a instrução SQL ``CREATE TABLE``. A forma usual desta instrução é:

```sql
create table nometabela ( definição tabela ) [ type = tipo_tabela ];
```

Ou seja, começamos com as palavras `create table`, seguimos com o nome desejado para a tabela e continuamos com um conjunto de definições de colunas. No final da instrução, podemos especificar, opcionalmente, o tipo de mecanismo de armazenamento desejado.

### Exemplo de criação da tabela

```sql
drop database if exists employee;
create database employee;

use employee;

create table department
(
department_id int not null auto_increment primary key,
name varchar(20)
) type=InnoDB;

create table employee
(
employee_id int not null auto_increment primary key,
name varchar(80),
job varchar(15),
department_id int not null references department(department_id)
) type=InnoDB;

create table employee_skills
(
employee_id int not null references employee(employee_id),
skill varchar(15) not null,
primary key (employee_id, skill)
) type=InnoDB;

create table client
(
client_id int not null auto_increment primary key,
name varchar(40),
address varchar(100),
contact_person varchar(80),
contact_number char(12)
) type=InnoDB;

create table assignment
(
client_id int not null references client(client_id),
employee_id int not null references employee(employee_id),
workdate date not null,
hours float,
primary key (client_id, employee_id, workdate)
) type=InnoDB;
```

### Analisando as instruções SQL neste arquivo uma a uma.

Começamos com:

```sql
drop database if exists employe;
```

Esta instrução verifica se um banco de dados chamado ``employee`` já existe. Se existir, a instrução irá apagá-lo. Isto não é estritamente necessário e ainda pode ser perigoso. Note que se você usar o MySQL em um ambiente de hospedagem de sites, por exemplo, a empresa responsável pela hospedagem poderá desativar o comando ``drop database``.

Agora começaremos a criar as tabelas dentro deste banco de dados. Vamos criar a tabela ``department``, como a seguir:

```sql
create table department
(
department_id int not null auto_increment primary key,
name varchar(20)
) type=InnoDB;
```

Para criar as colunas na tabela, fornecemos uma lista separada por vírgula das declarações da coluna entre parênteses. Note que os atributos de uma coluna não precisam ser separados por vírgula, apenas as colunas em si.

Em geral, nas instruções ``CREATE`` temos a tendência de colocar um item em cada linha para aumentar a legibilidade.

Nesta tabela, estamos declarando duas colunas. Cada declaração da coluna começa com o nome da coluna, seguido de informações sobre seu tipo.

Para facilitar nosso entendimento, vamos ver primeiro a segunda coluna, onde é declarado o nome do departamento: ``name varchar (20)``.

Esta declaração informa que a coluna será chamada ``name`` e que seu tipo é ``varchar(20)``. O tipo ``varchar`` é uma string com comprimento variável, neste caso, com até 20 caracteres. Também poderíamos ter usado ``char``, que é uma string com comprimento fixo. Escolher ``varchar`` ou  ``char`` não faz diferença em relação uso dos dados, mas no modo como os dados são armazenados na memória. Uma coluna do tipo ``varchar(20)`` ocupa tanto espaço quanto o número de caracteres armazenados nela, ao passo que **uma coluna do tipo ``char(20)`` tem sempre 20 caracteres de largura, independente do que está armazenando.**

