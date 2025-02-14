# **Tutorial MySQL: Uma Introdução Objetiva aos Fundamentos do Banco de Dados MySQL**

## Capítulo 4 - Como Criar Banco de Dados e Tabelas

### Introdução

Este capítulo aborda os comandos essenciais para a criação de bancos de dados e tabelas no MySQL, explicando suas sintaxes, exemplos e boas práticas. O objetivo é garantir a compreensão e fixação dos conceitos através da prática e análise detalhada dos comandos.

---

### **SQL: Structured Query Language**

- SQL é a linguagem utilizada para **criação**, **manipulação** e **consulta** em bancos de dados relacionais.

#### **Tipos de SQL**

1. **Data Definition Language (DDL):**
   Linguagem de definição de dados usada para criar e modificar a estrutura de bancos de dados. Exemplos: `CREATE`, `ALTER`, `DROP`.

2. **Data Manipulation Language (DML):**
   Linguagem de manipulação de dados usada para inserir, atualizar, excluir e consultar dados. Exemplos: `INSERT`, `UPDATE`, `DELETE`, `SELECT`.

---

### **Sensibilidade a Maiúsculas e Minúsculas**

- As palavras-chave do SQL não diferenciam letras maiúsculas de minúsculas (case-insensitive).
- No MySQL, a sensibilidade ao caso em nomes de bancos de dados e tabelas depende do sistema operacional:
  - **Windows:** Case-insensitive.
  - **Linux:** Case-sensitive (por padrão).

**Boas Práticas:**
Trate todos os identificadores como **case-sensitive** para evitar inconsistências ao migrar entre plataformas.

---

### **Identificadores no MySQL**

- Os **identificadores** são nomes exclusivos atribuídos a objetos do banco de dados, como tabelas, colunas e índices.  
- Restrições:
  - Não podem conter aspas (`'` ou `"`), `ASCII(0)`, ou `ASCII(255)`.
  - Os nomes de tabelas devem obedecer às regras do sistema operacional subjacente (ex.: não usar `/`, `\` ou `.`).

**Comprimento Máximo:**

- Identificadores comuns: 64 caracteres.  
- Aliases: Até 255 caracteres.

---

### **Como Criar um Banco de Dados**

Para criar um banco de dados, use o comando `CREATE DATABASE`:

```sql
CREATE DATABASE nome_do_banco;
```

Após criar, liste os bancos de dados disponíveis com:

```sql
SHOW DATABASES;
```

---

### **Selecionar um Banco de Dados**

Antes de trabalhar com tabelas ou realizar consultas, selecione o banco de dados com o comando `USE`:

```sql
USE nome_do_banco;
```

---

### **Criar Tabelas**

O comando `CREATE TABLE` cria tabelas dentro do banco de dados selecionado. Estrutura básica:

```sql
CREATE TABLE nome_tabela (
    coluna1 tipo1 [restrições],
    coluna2 tipo2 [restrições],
    ...
) [ENGINE=tipo_de_mecanismo];
```

---

### **Exemplo: Script Completo**

Este script demonstra como criar um banco de dados completo com tabelas relacionadas:

```sql
DROP DATABASE IF EXISTS employee;
CREATE DATABASE employee;

USE employee;

CREATE TABLE department (
    department_id INT NOT NULL AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(20)
) ENGINE=InnoDB;

CREATE TABLE employee (
    employee_id INT NOT NULL AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(80),
    job VARCHAR(15),
    department_id INT NOT NULL REFERENCES department(department_id)
) ENGINE=InnoDB;

CREATE TABLE employee_skills (
    employee_id INT NOT NULL REFERENCES employee(employee_id),
    skill VARCHAR(15) NOT NULL,
    PRIMARY KEY (employee_id, skill)
) ENGINE=InnoDB;

CREATE TABLE client (
    client_id INT NOT NULL AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(40),
    address VARCHAR(100),
    contact_person VARCHAR(80),
    contact_number CHAR(12)
) ENGINE=InnoDB;

CREATE TABLE assignment (
    client_id INT NOT NULL REFERENCES client(client_id),
    employee_id INT NOT NULL REFERENCES employee(employee_id),
    workdate DATE NOT NULL,
    hours FLOAT,
    PRIMARY KEY (client_id, employee_id, workdate)
) ENGINE=InnoDB;
```

---

### **Explicando o Script**

#### **1. Excluindo o Banco de Dados (se existir)**

```sql
DROP DATABASE IF EXISTS employee;
```

- Remove o banco de dados `employee` caso ele já exista. Isso é útil para evitar erros ao recriar o banco, mas pode ser perigoso em ambientes de produção.

#### **2. Criando o Banco de Dados**

```sql
CREATE DATABASE employee;
```

- Cria o banco de dados `employee`.

#### **3. Selecionando o Banco de Dados**

```sql
USE employee;
```

- Define que as próximas operações serão executadas no banco de dados `employee`.

#### **4. Criando a Tabela `department`**

```sql
CREATE TABLE department (
    department_id INT NOT NULL AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(20)
) ENGINE=InnoDB;
```

- Cria a tabela `department` com:
  - `department_id`: Identificador exclusivo, numérico, auto-incrementado.
  - `name`: Nome do departamento, com até 20 caracteres.
  - O mecanismo de armazenamento é definido como `InnoDB`, que suporta transações e chaves estrangeiras.

#### **5. Criando a Tabela `employee`**

```sql
CREATE TABLE employee (
    employee_id INT NOT NULL AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(80),
    job VARCHAR(15),
    department_id INT NOT NULL REFERENCES department(department_id)
) ENGINE=InnoDB;
```

- Inclui uma chave estrangeira `department_id`, que referencia a tabela `department`. Isso assegura que todo funcionário esteja associado a um departamento válido. Além disso, a restrição `NOT NULL` garante que o campo `department_id` sempre terá um valor atribuído, evitando registros incompletos. O atributo `AUTO_INCREMENT` na tabela `department` é usado para gerar valores exclusivos automaticamente para cada novo registro, simplificando a manutenção e garantindo integridade.

#### **6. Criando a Tabela `employee_skills`**

```sql
CREATE TABLE employee_skills (
    employee_id INT NOT NULL REFERENCES employee(employee_id),
    skill VARCHAR(15) NOT NULL,
    PRIMARY KEY (employee_id, skill)
) ENGINE=InnoDB;
```

- Define uma chave primária composta por `employee_id` e `skill`, garantindo combinações únicas.

#### **7. Criando a Tabela `client`**

```sql
CREATE TABLE client (
    client_id INT NOT NULL AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(40),
    address VARCHAR(100),
    contact_person VARCHAR(80),
    contact_number CHAR(12)
) ENGINE=InnoDB;
```

- Contém informações de clientes, como nome e detalhes de contato.

#### **8. Criando a Tabela `assignment`**

```sql
CREATE TABLE assignment (
    client_id INT NOT NULL REFERENCES client(client_id),
    employee_id INT NOT NULL REFERENCES employee(employee_id),
    workdate DATE NOT NULL,
    hours FLOAT,
    PRIMARY KEY (client_id, employee_id, workdate)
) ENGINE=InnoDB;
```

- Registra alocações de funcionários para clientes em datas específicas, com controle de horas trabalhadas.
- A chave primária composta garante que cada combinação de cliente, funcionário e data seja única.

---

### **Verificando Estruturas Criadas**

1. **Listar tabelas:**

   ```sql
   SHOW TABLES;
   ```

   - Retorna a lista de tabelas criadas no banco de dados atual.
   - **Exemplo de saída:**
     - ![Resultado SHOW TABLES](./images/TelaResultadoShowTables.png)

2. **Inspecionar uma tabela:**

   ```sql
   DESCRIBE nome_tabela;
   ```

   - Mostra detalhes sobre a estrutura da tabela, como colunas, tipos e chaves.

   **Exemplo:**

   ```sql
   DESCRIBE department;
   ```

   - **Exemplo de saída:**
     - ![Resultado DESCRIBE department](./images/TelaResultadoDescribleDepartment.png)

---

### **Instrução CREATE TABLE**

A instrução `CREATE TABLE` é usada para criar tabelas no banco de dados. Ela define a estrutura da tabela, incluindo nomes das colunas, tipos de dados e restrições. Vamos explorar alguns pontos importantes sobre esta instrução:

#### **Estrutura Básica**

```sql
CREATE TABLE nome_tabela (
    coluna1 tipo1 [restrições],
    coluna2 tipo2 [restrições],
    ...
) [ENGINE=tipo_de_mecanismo];
```

- **`nome_tabela`**: Nome da tabela a ser criada.
- **`coluna1`, `coluna2`**: Nomes das colunas.
- **`tipo1`, `tipo2`**: Tipos de dados atribuídos às colunas (ex.: `INT`, `VARCHAR`, `DATE`).
- **`restrições`**: Opções como `NOT NULL`, `AUTO_INCREMENT`, `PRIMARY KEY` etc.
- **`ENGINE`**: Define o mecanismo de armazenamento (ex.: `InnoDB`, `MyISAM`).

#### **Tipos de Dados Comuns**

1. **Numéricos**:
   - `INT`, `SMALLINT`, `BIGINT` (números inteiros).
   - `DECIMAL`, `FLOAT` (números com casas decimais).

2. **Texto**:
   - `CHAR(n)` (texto de comprimento fixo).
   - `VARCHAR(n)` (texto de comprimento variável).
   - `TEXT` (grande quantidade de texto).

3. **Datas**:
   - `DATE` (apenas data).
   - `DATETIME` (data e hora).

4. **Booleanos**:
   - `BOOLEAN` ou `TINYINT(1)` (valores verdadeiro/falso).

#### **Exemplo Simples**

Criação de uma tabela `produtos`:

```sql
CREATE TABLE produtos (
    id INT NOT NULL AUTO_INCREMENT PRIMARY KEY,
    nome VARCHAR(50) NOT NULL,
    preco DECIMAL(10, 2) NOT NULL,
    data_cadastro DATE
) ENGINE=InnoDB;
```

- **`id`**: Identificador único para cada produto, com incremento automático.
- **`nome`**: Nome do produto, obrigatório.
- **`preco`**: Preço do produto, obrigatório, com duas casas decimais.
- **`data_cadastro`**: Data de inclusão do produto no sistema.

#### **Comando para Listar Tabelas Criadas**

```sql
SHOW TABLES;
```

#### **Visualizando Estrutura de uma Tabela**

```sql
DESCRIBE produtos;
```

---

### **Tabelas Temporárias no MySQL**

No MySQL, é possível criar tabelas temporárias que só existem durante a sessão atual do usuário. Elas são úteis para armazenar dados intermediários sem impactar as tabelas permanentes do banco de dados.

#### **Como Criar uma Tabela Temporária**

A instrução `CREATE TEMPORARY TABLE` é usada para criar tabelas temporárias:

```sql
CREATE TEMPORARY TABLE nome_temporario (
    coluna1 tipo1 [restrições],
    coluna2 tipo2 [restrições],
    ...
);
```

- **`TEMPORARY`**: Indica que a tabela é temporária.
- Essas tabelas são excluídas automaticamente ao encerrar a sessão do usuário.

#### **Exemplo Prático**

```sql
CREATE TEMPORARY TABLE temp_clientes (
    id INT NOT NULL AUTO_INCREMENT PRIMARY KEY,
    nome VARCHAR(50) NOT NULL,
    idade INT
);

INSERT INTO temp_clientes (nome, idade) VALUES ('João Silva', 30), ('Maria Lima', 25);

SELECT * FROM temp_clientes;
```

- Neste exemplo, a tabela `temp_clientes` é criada e preenchida com dados temporários para análise.
- Após o término da sessão, ela será automaticamente removida.

#### **Diferenças para o SQL Server**

- No SQL Server, tabelas temporárias são identificadas pelo símbolo de tralha (`#`) no nome da tabela, como `#TempTable`.
- No MySQL, utiliza-se a palavra-chave `TEMPORARY` na instrução `CREATE TABLE` para indicar que a tabela é temporária.

#### **Boas Práticas com Tabelas Temporárias**

1. Use tabelas temporárias apenas quando necessário, para evitar consumo desnecessário de memória.
2. Verifique se as tabelas foram criadas corretamente com o comando `SHOW TABLES;`. Note que tabelas temporárias aparecem apenas na sessão atual.
3. Evite nomes conflitantes com tabelas permanentes.

---

### **Tipos de Colunas e Dados no MySQL**

No MySQL, os tipos de dados usados em colunas determinam o tipo de valores que podem ser armazenados. Existem três categorias principais de tipos de dados: **numéricos**, **string e texto**, e **data e hora**.

#### **1. Tipos Numéricos**

Os tipos numéricos são usados para armazenar números inteiros ou com casas decimais. Podem ser assinados (permitindo valores negativos) ou não assinados (apenas valores positivos).

- **Inteiros:**
  - `TINYINT`: Intervalo de -128 a 127 (ou 0 a 255 se não for assinado).
  - `SMALLINT`: Intervalo de -32,768 a 32,767 (ou 0 a 65,535 se não for assinado).
  - `MEDIUMINT`: Intervalo de -8.388.608 a 8.388.607.
  - `INT` ou `INTEGER`: Intervalo de -2.147.483.648 a 2.147.483.647.
  - `BIGINT`: Intervalo de -9.223.372.036.854.775.808 a 9.223.372.036.854.775.807.

- **Com Decimais:**
  - `DECIMAL` ou `NUMERIC`: Precisão exata definida pelo usuário (ex.: `DECIMAL(10,2)` armazena até 10 dígitos, 2 dos quais são decimais).
  - `FLOAT`: Menor precisão, armazena números em ponto flutuante.
  - `DOUBLE` ou `REAL`: Alta precisão, usado para cálculos científicos.

#### **2. Tipos de String e Texto**

Armazenam caracteres alfanuméricos, podendo ter tamanhos fixos ou variáveis.

- **Strings de Comprimento Fixo:**
  - `CHAR(n)`: Armazena exatamente `n` caracteres. É eficiente para valores de tamanho fixo.

- **Strings de Comprimento Variável:**
  - `VARCHAR(n)`: Armazena até `n` caracteres, ocupando espaço proporcional ao tamanho do conteúdo armazenado.

- **Texto Longo:**
  - `TINYTEXT`: Até 255 caracteres.
  - `TEXT`: Até 65.535 caracteres.
  - `MEDIUMTEXT`: Até 16.777.215 caracteres.
  - `LONGTEXT`: Até 4.294.967.295 caracteres.

- **Outros Tipos de Strings:**
  - `ENUM`: Conjunto fixo de valores predefinidos (ex.: `ENUM('Pequeno', 'Médio', 'Grande')`).
  - `SET`: Conjunto de valores predefinidos, permitindo múltiplas seleções (ex.: `SET('Opção1', 'Opção2', 'Opção3')`).

#### **3. Tipos de Data e Hora**

Usados para armazenar informações relacionadas a datas e horários.

- **Datas Simples:**
  - `DATE`: Formato `YYYY-MM-DD`, intervalo de `1000-01-01` a `9999-12-31`.

- **Horários Simples:**
  - `TIME`: Formato `HH:MM:SS`, intervalo de `-838:59:59` a `838:59:59`.

- **Datas e Horários Combinados:**
  - `DATETIME`: Formato `YYYY-MM-DD HH:MM:SS`, intervalo de `1000-01-01 00:00:00` a `9999-12-31 23:59:59`.
  - `TIMESTAMP`: Igual a `DATETIME`, mas é armazenado em UTC e convertido para o fuso horário local ao ser recuperado.

- **Intervalos de Tempo:**
  - `YEAR`: Armazena um ano no formato `YYYY` (intervalo de 1901 a 2155).

#### **Boas Práticas ao Escolher Tipos de Dados**

1. Use o tipo de dado mais compacto possível, levando em conta os valores esperados.
2. Para texto variável, prefira `VARCHAR` ao invés de `TEXT`, a menos que seja necessário armazenar grandes volumes de dados.
3. Escolha `DECIMAL` para valores monetários ou cálculos que exijam precisão exata.
4. Use tipos de data e hora apropriados para facilitar cálculos e comparações temporais.

#### **Exemplo de Criação de Tabela com Tipos Diversos**

```sql
CREATE TABLE exemplo_tipos (
    id INT NOT NULL AUTO_INCREMENT PRIMARY KEY,
    nome VARCHAR(50) NOT NULL,
    descricao TEXT,
    preco DECIMAL(10, 2),
    data_criacao DATETIME
) ENGINE=InnoDB;
```

- **`id`**: Inteiro auto-incrementado como identificador único.
- **`nome`**: Texto curto com no máximo 50 caracteres.
- **`descricao`**: Texto longo para detalhes do item.
- **`preco`**: Valor monetário com duas casas decimais.
- **`data_criacao`**: Combina data e hora para registrar quando o item foi adicionado.

---

Coming soon: Como criar índices
