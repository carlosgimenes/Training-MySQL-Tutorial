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
   
   ![Resultado SHOW TABLES](./images/TelaResultadoShowTables.png)

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

   ![Resultado DESCRIBE department](./images/TelaResultadoDescribleDepartment.png)

---

Coming soon
