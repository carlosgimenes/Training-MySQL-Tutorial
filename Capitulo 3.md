# **Tutorial MySQL: Uma Introdução Objetiva aos Fundamentos do Banco de Dados MySQL**

## Capítulo 3 - Como Projetar um Banco de Dados

Este capítulo aborda os princípios fundamentais do design de bancos de dados, incluindo a normalização. Um banco de dados bem projetado reduz a redundância e garante que todas as informações sejam mantidas. O objetivo é otimizar o uso do espaço de armazenamento enquanto preserva os vínculos entre os dados.

---

### Conceitos e Terminologia de Banco de Dados

Antes de mergulhar nos princípios de design, é essencial compreender alguns conceitos e termos básicos que serão utilizados ao longo deste capítulo.

---

### Entidades e Relacionamentos

Entidades e relacionamentos são os pilares da modelagem de dados. As **entidades** representam objetos do mundo real sobre os quais armazenamos informações, como funcionários e departamentos. Os **relacionamentos** são os vínculos entre essas entidades. Por exemplo, um funcionário está associado ao departamento onde trabalha. Neste caso:

- **Entidades**: Funcionário e Departamento  
- **Relacionamento**: _Trabalha em_ (entre Funcionário e Departamento)

#### Tipos de Relacionamentos

Os relacionamentos podem ser classificados como:  

- **Um para Um (1:1)**: Cada entidade em um conjunto está associada a exatamente uma entidade em outro conjunto. Exemplo: um funcionário tem um único compartimento.  
- **Um para Muitos (1:N)**: Uma entidade em um conjunto pode estar associada a várias entidades em outro conjunto, mas cada entidade no segundo conjunto está associada a apenas uma do primeiro. Exemplo: muitos funcionários trabalham para um único departamento.  
- **Muitos para Muitos (M:N)**: Entidades de ambos os conjuntos podem estar associadas a múltiplas entidades do outro. Exemplo: funcionários podem trabalhar para vários departamentos, e departamentos podem ter vários funcionários.

#### Exemplo Visual

![Relacionamento esta localizado em e trabalha para](./images/FiguraRelacionamentoLocalizadoTabalhaPara.png)  
_**O relacionamento "está localizado em" é de um para um. O relacionamento "trabalha para" é de muitos para um.**_

#### Considerações sobre Regras de Negócios

Os tipos de relacionamentos variam de acordo com o ambiente e as regras de negócios. Por exemplo:

- **1:N**: Funcionários geralmente trabalham para um único departamento.  
- **M:N**: Em algumas organizações, funcionários podem trabalhar em múltiplos departamentos.  
- **1:1**: Um funcionário pode ter um compartimento exclusivo, mas também pode dividi-lo com outra pessoa, tornando o relacionamento _**está localizado em**_ algo diferente de um para um.

Ao projetar um banco de dados, leve em consideração as regras de negócios e os requisitos do sistema. Cada sistema é único, e seu design deve refletir as especificidades do ambiente que está sendo modelado.

---

### Colunas e Atributos

As **colunas** (ou atributos) são os elementos fundamentais de uma tabela em um banco de dados. Elas representam as características ou propriedades que queremos armazenar sobre uma entidade. Cada coluna é definida por um **nome**, um **tipo de dado** e, frequentemente, por **restrições** que ajudam a garantir a integridade e a validade dos dados.

#### Definindo Colunas

Ao projetar uma tabela, é necessário escolher cuidadosamente as colunas que irão compô-la. Cada coluna deve refletir uma única característica da entidade que a tabela representa.

**Exemplo:**  
Para uma tabela `Funcionários`, as colunas podem incluir:

- Nome  
- Data de Nascimento  
- CPF  
- Cargo  
- Salário  

#### Tipos de Dados

Os tipos de dados definem o tipo de informação que pode ser armazenada em uma coluna. Escolher o tipo de dado correto ajuda a economizar espaço e evitar erros. Exemplos de tipos de dados incluem:

- **Inteiros:** `INT`, `SMALLINT`, `BIGINT`  
- **Decimais:** `DECIMAL`, `FLOAT`  
- **Texto:** `VARCHAR`, `CHAR`, `TEXT`  
- **Datas e Horários:** `DATE`, `DATETIME`, `TIMESTAMP`  
- **Booleanos:** `BOOLEAN`  

**Exemplo de Escolha Correta:**

- Para o CPF de um funcionário, usar `CHAR(11)` pode ser mais eficiente do que `VARCHAR(11)`, já que o número de caracteres é fixo.

#### Restrições em Colunas

Restrições ajudam a garantir a integridade dos dados no banco de dados. Alguns exemplos incluem:  

- **NOT NULL:** Garante que a coluna não terá valores nulos.  
- **UNIQUE:** Assegura que todos os valores de uma coluna sejam únicos.  
- **PRIMARY KEY:** Define a coluna (ou conjunto de colunas) como identificador único da tabela.  
- **FOREIGN KEY:** Assegura que o valor da coluna corresponda a uma chave primária em outra tabela, estabelecendo um relacionamento.  
- **DEFAULT:** Define um valor padrão para a coluna.  

**Exemplo de Restrições:**  
Para a tabela `Funcionários`, podemos definir:

- `CPF` como `PRIMARY KEY` para identificar unicamente cada funcionário.  
- `Salário` com uma restrição `NOT NULL`, já que todo funcionário deve ter um salário.  

#### Boas Práticas no Uso de Colunas

1. **Nomeação Consistente:**  
   Use nomes descritivos e consistentes, como `Data_Nascimento` em vez de `DN` ou `DataNasc`.  
1. **Normalização:**  
   Evite armazenar dados derivados em colunas, como a idade do funcionário, que pode ser calculada com base na `Data_Nascimento`.
1. **Tipos de Dados Apropriados:**  
   Escolha tipos de dados que melhor representem os valores esperados. Evite tipos excessivamente amplos, como `TEXT` para nomes.
1. **Documentação:**  
   Documente as finalidades e restrições de cada coluna para facilitar a manutenção do banco de dados.

---

### Linhas, Registros e Tuplas

As **linhas** de uma tabela representam instâncias individuais de dados armazenados no banco de dados. Cada linha é um conjunto de valores que correspondem às colunas (ou atributos) de uma tabela e descreve uma única entidade ou evento.

#### O Que São Linhas?  

As linhas (também chamadas de **registros** ou **tuplas**) contêm os dados reais de uma tabela. Enquanto as colunas definem a estrutura e os tipos de dados de uma tabela, as linhas preenchem essa estrutura com informações concretas.

**Exemplo de Estrutura e Dados:**  
Considere a tabela `Funcionários` com as seguintes colunas:  

- Nome  
- CPF  
- Cargo  
- Salário  

**Exemplo de Linhas na Tabela:**  

| Nome       | CPF         | Cargo         | Salário  |  
|------------|-------------|---------------|----------|  
| João Silva | 12345678900 | Analista      | 5000.00  |  
| Maria Lima | 98765432100 | Desenvolvedora| 6500.00  |  

Neste caso:  

- Cada linha representa um funcionário.  
- Cada célula da linha contém o valor para uma coluna específica, como o nome ou o salário do funcionário.

---

#### Características de Linhas

1. **Identificação Única:**  
   Cada linha pode ser identificada exclusivamente por uma **chave primária** definida na tabela, como o `CPF` no exemplo acima.  

2. **Integridade Referencial:**  
   Os valores de uma linha podem depender de informações em outras tabelas por meio de **chaves estrangeiras**. Por exemplo, uma tabela `Departamentos` poderia ser referenciada por uma linha em `Funcionários`.

3. **Armazenamento de Dados:**  
   Os bancos de dados organizam fisicamente as linhas em seus sistemas de armazenamento. Embora a ordem das linhas em uma tabela não seja garantida, ela pode ser manipulada em consultas usando o comando `ORDER BY`.

---

#### Diferença Entre Linhas e Colunas

- **Linhas:** Contêm os valores concretos. Cada linha é uma instância ou registro.  
- **Colunas:** Definem a estrutura e as propriedades que todas as linhas devem seguir.  

---

#### Terminologia: Tuplas

No contexto teórico de bancos de dados, as linhas também são chamadas de **tuplas**. Este termo vem da teoria relacional, onde cada tupla é um conjunto ordenado de valores que segue um esquema relacional.  

Embora o termo **linha** seja mais comum em contextos práticos, entender **tuplas** é importante para compreender a base teórica do modelo relacional.

---

#### Boas Práticas no Gerenciamento de Linhas

1. **Evite Dados Redundantes:** Certifique-se de que cada linha armazene apenas os dados necessários. Redundâncias podem ser resolvidas por meio da normalização.  
2. **Garanta a Integridade:** Utilize restrições como chaves primárias e estrangeiras para evitar duplicação de linhas ou valores inconsistentes.  
3. **Documente Regras de Negócios:** Explique como cada linha deve ser interpretada e quais regras de negócios ela deve seguir, especialmente em sistemas complexos.  

---

### Chaves no Banco de Dados

As **chaves** são elementos fundamentais no design de bancos de dados relacionais. Elas garantem a integridade e a consistência dos dados e são usadas para identificar registros de forma única, estabelecer relacionamentos entre tabelas e aplicar regras de negócio.

#### Tipos de Chaves

1. **Chave Primária (Primary Key)**  
   - Identifica unicamente cada registro em uma tabela.  
   - Deve conter valores únicos e não pode ser nula (`NOT NULL`).  
   - Exemplo: Em uma tabela `Funcionários`, o campo `CPF` pode ser definido como a chave primária.

   **Tabela com Chave Primária:**  

   | CPF         | Nome       | Cargo         | Salário  |  
   |-------------|------------|---------------|----------|  
   | 12345678900 | João Silva | Analista      | 5000.00  |  
   | 98765432100 | Maria Lima | Desenvolvedora| 6500.00  |  

1. **Chave Estrangeira (Foreign Key)**  
   - Estabelece um relacionamento entre duas tabelas.  
   - Refere-se à chave primária de outra tabela, garantindo integridade referencial.  
   - Exemplo: Uma tabela `Departamentos` pode ter um campo `ID_Departamento` que é referenciado pela tabela `Funcionários`.

   **Exemplo de Relacionamento:**  
   **Tabela Departamentos:**  

   | ID_Departamento | Nome            |  
   |-----------------|-----------------|  
   | 1               | TI              |  
   | 2               | Recursos Humanos|  

   **Tabela Funcionários:**  

   | Nome       | CPF         | Cargo         | Salário  | ID_Departamento |  
   |------------|-------------|---------------|----------|-----------------|  
   | João Silva | 12345678900 | Analista      | 5000.00  | 1               |  
   | Maria Lima | 98765432100 | Desenvolvedora| 6500.00  | 1               |  

1. **Chave Candidata (Candidate Key)**  
   - Qualquer campo ou combinação de campos que possa ser usada como chave primária.  
   - Exemplo: Em uma tabela `Clientes`, tanto o `CPF` quanto o `E-mail` podem ser candidatos a chave primária.

1. **Chave Alternativa (Alternate Key)**  
   - É uma chave candidata que não foi escolhida como chave primária.  
   - Exemplo: Se o `CPF` for a chave primária, o `E-mail` será uma chave alternativa.

1. **Chave Composta (Composite Key)**  
   - Consiste em dois ou mais campos que, juntos, identificam unicamente um registro.  
   - Exemplo: Em uma tabela de `Pedidos`, `ID_Produto` e `ID_Cliente` juntos podem formar uma chave composta.

   **Tabela Pedidos:**  

   | ID_Produto | ID_Cliente | Quantidade |  
   |------------|------------|------------|  
   | 101        | 5001       | 3          |  
   | 102        | 5002       | 5          |  

1. **Chave Surrogate (Surrogate Key)**  
   - Uma chave artificial gerada pelo sistema, frequentemente usada em substituição a chaves compostas ou complexas.  
   - Exemplo: Um campo `ID` gerado automaticamente como chave primária.

---

#### Boas Práticas com Chaves

1. Escolha chaves primárias simples e intuitivas, sempre que possível.  
2. Use chaves estrangeiras para garantir integridade referencial entre tabelas.  
3. Documente todas as chaves candidatas e alternadas, especialmente em projetos complexos.  
4. Considere usar chaves surrogate em vez de chaves compostas para simplificar o design e melhorar a performance.  

---

### Dependências Funcionais

As **dependências funcionais** são um conceito fundamental no design de bancos de dados relacionais. Elas descrevem as relações entre os atributos de uma tabela e desempenham um papel crucial no processo de normalização.

---

#### O Que São Dependências Funcionais?

Uma dependência funcional ocorre quando o valor de um atributo (ou conjunto de atributos) determina unicamente o valor de outro atributo em uma tabela.  
Formalmente, dizemos que o atributo `B` é funcionalmente dependente do atributo `A` (denotado como `A → B`) se, para cada valor de `A`, existe exatamente um valor correspondente de `B`.

**Exemplo:**  
Na tabela `Funcionários`, o `CPF` determina unicamente o `Nome` do funcionário.  

- `CPF → Nome`

| CPF         | Nome         | Cargo     | Salário |  
|-------------|--------------|-----------|---------|  
| 12345678900 | João Silva   | Analista  | 5000.00 |  
| 98765432100 | Maria Lima   | Desenvolvedora | 6500.00 |  

---

#### Tipos de Dependências Funcionais

1. **Dependência Funcional Completa**  
   - Ocorre quando um atributo depende totalmente da chave primária.  
   - Exemplo: Na tabela `Pedidos`, `Data_Pedido` depende completamente de `ID_Pedido`.  
   - **`ID_Pedido → Data_Pedido`**

2. **Dependência Funcional Parcial**  
   - Ocorre quando um atributo depende apenas de parte da chave primária em uma tabela com chave composta.  
   - Exemplo: Se `ID_Produto` e `ID_Cliente` formam a chave primária em uma tabela `Pedidos`, e o `Nome_Produto` depende apenas de `ID_Produto`, isso é uma dependência parcial.  
   - **`ID_Produto → Nome_Produto`** (mas não depende de `ID_Cliente`).

3. **Dependência Transitiva**  
   - Ocorre quando um atributo depende de outro atributo que, por sua vez, depende da chave primária.  
   - Exemplo: Em uma tabela `Funcionários`, se `CPF` determina `ID_Departamento` e `ID_Departamento` determina `Nome_Departamento`, então `Nome_Departamento` é transitivamente dependente de `CPF`.  
   - **`CPF → ID_Departamento → Nome_Departamento`**

---

#### Por Que as Dependências Funcionais São Importantes?

As dependências funcionais ajudam a:

- **Identificar Redundâncias:** Permitem identificar colunas que podem ser isoladas em tabelas separadas durante o processo de normalização.  
- **Evitar Anomalias:** Garantem que alterações, exclusões ou inserções em uma tabela não levem a inconsistências.  
- **Projetar Tabelas:** São usadas para determinar a chave primária e dividir tabelas em formas normais.

---

#### Exemplo Prático

Considere a tabela `Pedidos` abaixo:  

| ID_Pedido | ID_Cliente | Nome_Cliente | Data_Pedido |  
|-----------|------------|--------------|-------------|  
| 1         | 101        | João Silva   | 2025-01-01  |  
| 2         | 102        | Maria Lima   | 2025-01-02  |  

**Dependências Funcionais Identificadas:**  

- `ID_Pedido → Data_Pedido`  
- `ID_Cliente → Nome_Cliente`  

**Problemas:**  
Se `Nome_Cliente` mudar, será necessário alterar todos os pedidos associados a ele. Isso pode levar a inconsistências.

**Solução:**  
Divida a tabela em duas:  
**Tabela Pedidos:**  

| ID_Pedido | ID_Cliente | Data_Pedido |  
|-----------|------------|-------------|  
| 1         | 101        | 2025-01-01  |  
| 2         | 102        | 2025-01-02  |  

**Tabela Clientes:**  

| ID_Cliente | Nome_Cliente |  
|------------|--------------|  
| 101        | João Silva   |  
| 102        | Maria Lima   |  

---

### Esquemas de Banco de Dados

Um **esquema** é a estrutura organizacional que define como os dados são armazenados em um banco de dados. Ele inclui tabelas, colunas, tipos de dados, restrições, relacionamentos e outras informações necessárias para o design e a implementação do banco.

#### O Que é um Esquema?

No contexto de bancos de dados relacionais, um esquema é o plano ou blueprint que descreve a organização dos dados. Ele é usado tanto para representar os dados logicamente quanto para implementar o banco no nível físico.

**Componentes de um Esquema:**

1. **Tabelas:** Contêm os dados organizados em linhas e colunas.  
2. **Chaves:** Garantem a integridade dos dados e estabelecem relacionamentos entre tabelas.  
3. **Relacionamentos:** Descrevem como as tabelas estão conectadas.  
4. **Restrições:** Garantem a consistência e a validade dos dados.  
5. **Índices:** Melhoram o desempenho das consultas.  

#### Tipos de Esquemas

1. **Esquema Lógico:**  
   - Representa a estrutura dos dados no nível lógico.  
   - Define tabelas, colunas, chaves, tipos de dados e relacionamentos.  
   - Exemplo: Um diagrama entidade-relacionamento (ERD).  

2. **Esquema Físico:**  
   - Descreve como os dados são armazenados no sistema de banco de dados.  
   - Inclui detalhes como estruturas de índice, organização de arquivos e estratégias de particionamento.  

---

#### Exemplo de Esquema

Considere um sistema de banco de dados para uma empresa com duas tabelas principais: `Funcionários` e `Departamentos`.

**Esquema Lógico:**

```sql
CREATE TABLE Funcionarios (
    CPF CHAR(11) PRIMARY KEY,
    Nome VARCHAR(100) NOT NULL,
    Cargo VARCHAR(50),
    Salario DECIMAL(10, 2),
    ID_Departamento INT,
    FOREIGN KEY (ID_Departamento) REFERENCES Departamentos(ID_Departamento)
);

CREATE TABLE Departamentos (
    ID_Departamento INT PRIMARY KEY,
    Nome_Departamento VARCHAR(50) NOT NULL
);
```

**Esquema Físico:**

- **Índices:** Um índice no campo `CPF` para melhorar buscas por funcionários.  
- **Particionamento:** A tabela `Funcionários` pode ser particionada por departamento.  
- **Armazenamento:** As tabelas podem ser armazenadas em discos diferentes para balancear a carga.

---

#### Boas Práticas na Definição de Esquemas

1. **Clareza:** Use nomes de tabelas e colunas que sejam descritivos e consistentes.  
   - Exemplo: Prefira `Nome_Departamento` a `ND` ou `DeptName`.  
2. **Documentação:** Mantenha um diagrama do esquema atualizado para facilitar a manutenção.  
3. **Normalização:** Certifique-se de que o esquema segue os princípios de normalização para evitar redundâncias.  
4. **Otimização:** Planeje o esquema físico para otimizar consultas frequentes e minimizar o uso de recursos.  

---

#### Esquemas em Diferentes Contextos

1. **Esquema por Usuário:** Alguns bancos, como PostgreSQL, permitem que diferentes usuários tenham seus próprios esquemas para organizar tabelas de forma independente.  
2. **Esquemas Multitenant:** Em aplicativos SaaS, cada cliente pode ter seu próprio esquema, garantindo isolamento e segurança dos dados.

---

### Redundância versus Perda de Dados

O equilíbrio entre **redundância** e **perda de dados** é um dos maiores desafios no design de bancos de dados. Ambos os extremos podem causar problemas significativos para a eficiência, consistência e usabilidade do banco de dados.

#### O Que é Redundância?

**Redundância** ocorre quando os mesmos dados são armazenados em múltiplos locais dentro do banco de dados.

- **Exemplo:** Se a tabela `Funcionários` contém o nome do departamento e o mesmo nome é armazenado na tabela `Departamentos`, essa informação está redundante.

| CPF         | Nome         | Cargo     | Departamento  |  
|-------------|--------------|-----------|---------------|  
| 12345678900 | João Silva   | Analista  | TI            |  
| 98765432100 | Maria Lima   | Desenvolvedora | TI            |  

**Impactos Negativos da Redundância:**  

1. **Maior Espaço de Armazenamento:** Os dados redundantes ocupam mais espaço, aumentando os custos.  
1. **Anomalias de Atualização:** Alterar dados redundantes em um local sem atualizar os outros pode causar inconsistências.  
1. **Dificuldade na Manutenção:** Mais esforço é necessário para gerenciar informações duplicadas.  

---

#### O Que é Perda de Dados?

**Perda de dados** ocorre quando informações importantes são eliminadas ou não são armazenadas devido a falhas no design do banco de dados. Isso geralmente acontece devido à remoção de registros relacionados ou à ausência de informações críticas.  

**Exemplo de Perda de Dados:**  
Se a tabela `Funcionários` não possui um campo para registrar o salário, essa informação essencial ficará inacessível.  

**Impactos Negativos da Perda de Dados:**  

1. **Incompletude:** Informações importantes para operações ou análises podem não estar disponíveis.  
1. **Falhas de Relacionamento:** Dados ausentes podem romper vínculos entre tabelas relacionadas.  
1. **Dificuldade de Recuperação:** Dados perdidos frequentemente exigem esforços manuais para serem reconstruídos.

---

#### Como Evitar Redundância Excessiva e Perda de Dados?

1. **Normalização:**  
   - Reduz a redundância ao dividir tabelas e estabelecer relacionamentos claros.  
   - **Exemplo:** Em vez de armazenar o nome do departamento em `Funcionários`, utilize uma chave estrangeira para relacioná-lo à tabela `Departamentos`.

   **Tabela Funcionários:**  

   | CPF         | Nome         | Cargo     | ID_Departamento |  
   |-------------|--------------|-----------|-----------------|  
   | 12345678900 | João Silva   | Analista  | 1               |  

   **Tabela Departamentos:**  

   | ID_Departamento | Nome         |  
   |-----------------|--------------|  
   | 1               | TI           |  

2. **Documentação de Regras de Negócio:**  
   - Certifique-se de que todas as regras de negócio estão documentadas e refletidas no design do banco de dados.  

3. **Integridade Referencial:**  
   - Use chaves estrangeiras para manter os relacionamentos consistentes entre tabelas.

4. **Backup Regular:**  
   - Mantenha backups frequentes para minimizar o impacto de perda de dados devido a falhas ou erros humanos.

---

#### Quando Considerar Redundância Controlada?

Embora a normalização seja fundamental, existem cenários onde uma certa **redundância controlada** pode ser benéfica:

- **Performance:** Em bancos de dados com alto volume de leitura, armazenar dados frequentemente acessados em múltiplos locais pode acelerar consultas.  
- **Backup Local:** Manter cópias redundantes de dados críticos pode ajudar na recuperação rápida em caso de falhas.

**Exemplo de Redundância Controlada:**  
Uma tabela `Relatórios` pode armazenar dados consolidados, como nomes de clientes e total de compras, mesmo que essas informações possam ser derivadas de outras tabelas.  

---

#### Conclusão

O design ideal de um banco de dados deve minimizar a redundância sem comprometer a integridade ou a disponibilidade dos dados. O uso de técnicas como normalização e redundância controlada deve ser cuidadosamente avaliado com base nos requisitos do sistema e nas regras de negócio.

---

### Anomalias Associadas à Redundância

Quando a redundância não é controlada em um banco de dados, ela pode levar a **anomalias** durante operações de atualização, inserção ou eliminação de dados. Essas anomalias são comuns em tabelas que não foram devidamente normalizadas.

---

#### 1. Anomalia de Atualização

**O Que É?**  
Ocorre quando é necessário atualizar dados redundantes em vários locais, e alguma atualização é omitida, resultando em inconsistências.

**Exemplo:**  
Considere uma tabela que armazena os nomes dos departamentos repetidamente em vez de usar uma referência a outra tabela.

| CPF         | Nome         | Departamento |  
|-------------|--------------|--------------|  
| 12345678900 | João Silva   | TI           |  
| 98765432100 | Maria Lima   | TI           |  

Se o nome do departamento `TI` mudar para `Tecnologia da Informação`, todas as linhas relacionadas precisarão ser atualizadas. Se uma delas for esquecida, haverá inconsistência no banco de dados.

---

#### 2. Anomalia de Inserção

**O Que É?**  
Ocorre quando a redundância impede a inserção de dados devido à dependência de outros dados inexistentes.

**Exemplo:**  
Imagine que a tabela `Funcionários` armazene o nome do departamento diretamente, sem uma tabela separada para departamentos. Não será possível adicionar um novo departamento sem que um funcionário esteja associado a ele.

| CPF         | Nome         | Departamento |  
|-------------|--------------|--------------|  
| (Vazio)     | (Vazio)      | Marketing    |  

Neste caso, se o departamento `Marketing` ainda não tiver funcionários, não será possível registrá-lo.

---

#### 3. Anomalia de Eliminação

**O Que É?**  
Ocorre quando a remoção de um registro resulta na perda acidental de informações importantes.

**Exemplo:**  
Se um funcionário for excluído e a tabela `Funcionários` armazenar o nome do departamento diretamente, a exclusão pode levar à perda do nome do departamento caso nenhum outro funcionário esteja associado a ele.

| CPF         | Nome         | Departamento |  
|-------------|--------------|--------------|  
| 12345678900 | João Silva   | TI           |  

Se João Silva for excluído, a informação sobre o departamento `TI` também será perdida.

---

### Como Evitar Anomalias?

1. **Normalização:**  
   Divida os dados em tabelas separadas com relacionamentos bem definidos.  
   - **Solução para os Exemplos:** Crie uma tabela `Departamentos` separada, e use chaves estrangeiras na tabela `Funcionários`.

   **Tabela Funcionários:**  

   | CPF         | Nome         | ID_Departamento |  
   |-------------|--------------|-----------------|  
   | 12345678900 | João Silva   | 1               |  

   **Tabela Departamentos:**  

   | ID_Departamento | Nome         |  
   |-----------------|--------------|  
   | 1               | TI           |  

2. **Restrições de Integridade:**  
   Use chaves estrangeiras e restrições para garantir que relacionamentos sejam mantidos e consistentes.

3. **Documentação de Regras de Negócio:**  
   Certifique-se de que todas as regras de negócio estejam refletidas no design do banco de dados.

---

### Valores Nulos

Os **valores nulos** representam a ausência de um valor em uma coluna de uma tabela no banco de dados. Eles são úteis para lidar com dados incompletos ou desconhecidos, mas devem ser usados com cuidado para evitar problemas de integridade e interpretação.

---

#### O Que é um Valor Nulo?

Um valor nulo significa "sem dado" ou "não aplicável". Ele não é o mesmo que:

- **Zero:** Que é um valor numérico válido.  
- **String vazia (`''`):** Que é uma entrada válida, mas sem caracteres.  
- **Espaço em branco:** Que é um caractere válido.

**Exemplo:**  

| Nome         | CPF         | Cargo      | Salário  |  
|--------------|-------------|------------|----------|  
| João Silva   | 12345678900 | Analista   | 5000.00  |  
| Maria Lima   | 98765432100 | (Nulo)     | 6500.00  |  

No exemplo acima, o campo `Cargo` de Maria Lima é nulo, indicando que essa informação está ausente ou ainda não foi fornecida.

---

#### Quando Usar Valores Nulos?

1. **Dados Desconhecidos:** Quando um valor ainda não é conhecido, mas pode ser adicionado posteriormente.  
   - Exemplo: O número de telefone de um cliente que não foi fornecido no momento do cadastro.

2. **Dados Não Aplicáveis:** Quando uma coluna não se aplica a um registro específico.  
   - Exemplo: O campo "Número da Placa" em um banco de dados de veículos, mas o registro é de uma bicicleta.

---

#### Problemas Associados a Valores Nulos

1. **Ambiguidade:** Pode ser difícil distinguir entre dados ausentes e dados não aplicáveis.  
2. **Impacto em Consultas:** Operações envolvendo valores nulos podem produzir resultados inesperados.  
   - Exemplo: `NULL + 1` resulta em `NULL`, não em `1`.  
3. **Integridade dos Dados:** Se muitas colunas aceitam valores nulos, isso pode levar a inconsistências.  

**Exemplo de Consulta com Nulos:**  
Se você executar uma consulta para encontrar funcionários sem salário registrado:

```sql
SELECT Nome FROM Funcionarios WHERE Salario IS NULL;
```

---

#### Boas Práticas para Usar Valores Nulos

1. **Evite Nulos Sempre que Possível:** Use valores padrão (`DEFAULT`) para evitar lacunas de informação.  
   - Exemplo: Para a coluna `Salário`, um valor padrão de `0.00` pode ser usado quando o salário não é aplicável.  
2. **Defina Restrições Claras:** Use restrições `NOT NULL` para colunas que sempre devem ter valores.  
3. **Documente o Significado do Nulo:** Deixe claro se um nulo significa "ausente", "não aplicável" ou outra interpretação.  
4. **Trate Nulos em Consultas:**  
   - Use `IS NULL` ou `IS NOT NULL` para manipular registros com valores nulos.  
   - Utilize funções como `COALESCE` para substituir nulos por valores padrão em resultados de consultas.  

**Exemplo de Uso de COALESCE:**

```sql
SELECT Nome, COALESCE(Salario, 0) AS Salario_Ajustado FROM Funcionarios;
```

---

#### Impacto em Normalização

Valores nulos também devem ser considerados durante a normalização:

- Evite criar colunas que frequentemente terão valores nulos dividindo os dados em tabelas separadas.  
- **Exemplo:** Crie uma tabela específica para armazenar dados opcionais, como "Benefícios" de funcionários.

**Tabela Funcionários:**  

| CPF         | Nome         | Cargo      | Salário  |  
|-------------|--------------|------------|----------|  
| 12345678900 | João Silva   | Analista   | 5000.00  |  
| 98765432100 | Maria Lima   | Desenvolvedora | 6500.00  |  

**Tabela Benefícios:**  

| CPF         | Benefício          |  
|-------------|--------------------|  
| 98765432100 | Auxílio Creche     |  
| 12345678900 | Vale Transporte    |  

---

#### Conclusão

Embora os valores nulos sejam essenciais para representar a ausência de dados, seu uso deve ser cuidadosamente planejado para evitar inconsistências e dificuldades de interpretação. Ao aplicar boas práticas, os valores nulos podem ser uma ferramenta valiosa para a flexibilidade do design de banco de dados.

---

### Normalização de Banco de Dados

A **normalização** é o processo de organizar os dados de um banco de dados para reduzir redundâncias e melhorar a integridade dos dados. Este processo é baseado em uma série de **formas normais** (normal forms) que ajudam a estruturar os dados de maneira eficiente e lógica.

#### Objetivos da Normalização

- Eliminar **redundâncias desnecessárias** de dados.
- Garantir a **consistência** e a **integridade** dos dados.
- Facilitar a **manutenção** e as **atualizações** no banco de dados.
- Melhorar o **desempenho** para consultas específicas, ao evitar a duplicação de informações.

#### Formas Normais (Normal Forms)

As formas normais são etapas no processo de normalização, cada uma com critérios específicos. Aqui estão as mais comuns:

---

**1ª Forma Normal (1NF)**

- As tabelas devem possuir apenas **valores atômicos** (não divisíveis).  
- Cada coluna deve conter apenas um tipo de dado.  
- Exemplo de violação:  
  Uma tabela que armazena múltiplos telefones em uma única célula.

  **Tabela Incorreta:**  

  | Cliente | Telefones       |  
  |---------|-----------------|  
  | João    | 1234, 5678      |  

  **Tabela Corrigida (1NF):**  

  | Cliente | Telefone |  
  |---------|----------|  
  | João    | 1234     |  
  | João    | 5678     |  

---

**2ª Forma Normal (2NF)**  

- Atende à 1ª Forma Normal.  
- Elimina dependências parciais em chaves compostas.  
- Cada coluna deve depender da **chave primária inteira**.  
- Exemplo de violação:  
  Uma tabela onde o nome de um cliente está associado apenas ao ID do pedido.  

  **Tabela Incorreta:**  

  | ID Pedido | Cliente | Produto   |  
  |-----------|---------|-----------|  
  | 1         | João    | Produto A |  
  | 2         | Maria   | Produto B |  

  **Tabelas Corrigidas (2NF):**  

  **Tabela de Pedidos:**  

  | ID Pedido | Produto   |  
  |-----------|-----------|  
  | 1         | Produto A |  
  | 2         | Produto B |  

  **Tabela de Clientes:**  

  | ID Cliente | Cliente |  
  |------------|---------|  
  | 1          | João    |  
  | 2          | Maria   |  

---

**3ª Forma Normal (3NF)**  

- Atende à 2ª Forma Normal.  
- Remove dependências transitivas.  
- Cada coluna não chave deve depender **somente** da chave primária.  
- Exemplo de violação:  
  Uma tabela onde o endereço de um cliente depende do código postal.  
  
  **Tabela Incorreta:**  

  | Cliente | Endereço     | Código Postal |  
  |---------|--------------|---------------|  
  | João    | Rua A        | 12345         |  

  **Tabelas Corrigidas (3NF):**  

  **Tabela de Clientes:**  

  | Cliente | Código Postal |  
  |---------|---------------|  
  | João    | 12345         |  

  **Tabela de Endereços:**  

  | Código Postal | Endereço     |  
  |---------------|--------------|  
  | 12345         | Rua A        |  

---

#### Quando Normalizar?

- **Recomenda-se normalizar** quando o banco de dados for frequentemente alterado ou quando houver um risco elevado de inconsistências nos dados.  
- **Evite excessiva normalização** se o sistema exigir alta performance em leituras (muitas consultas podem se tornar mais lentas).

#### Conclusão

A normalização é uma ferramenta poderosa para projetar bancos de dados consistentes e fáceis de manter. No entanto, a decisão de normalizar deve equilibrar os benefícios da integridade dos dados com as necessidades de desempenho.

---

### **Resumo do Capítulo: Como Projetar um Banco de Dados**

Este capítulo abordou os conceitos fundamentais para o design de um banco de dados eficiente e confiável, destacando as melhores práticas e evitando problemas comuns. Aqui estão os principais pontos discutidos:

---

#### **1. Entidades e Relacionamentos**

- **Entidades:** Representam objetos do mundo real sobre os quais armazenamos dados (ex.: Funcionários, Departamentos).  
- **Relacionamentos:** Vinculam entidades, podendo ser de tipos diferentes:
  - **Um para Um (1:1):** Um funcionário tem um único compartimento.
  - **Um para Muitos (1:N):** Muitos funcionários trabalham para um único departamento.
  - **Muitos para Muitos (M:N):** Funcionários podem trabalhar em vários projetos, e cada projeto pode ter vários funcionários.

---

#### **2. Normalização e Dependências Funcionais**

- **Normalização:** Processo de organizar dados para reduzir redundâncias e evitar anomalias de atualização, inserção e exclusão.
  - **1ª Forma Normal (1NF):** Elimina grupos repetitivos e exige valores atômicos.
  - **2ª Forma Normal (2NF):** Remove dependências parciais em tabelas com chave composta.
  - **3ª Forma Normal (3NF):** Remove dependências transitivas.
- **Dependências Funcionais:** Relações entre atributos de uma tabela.
  - **Completa:** Depende totalmente da chave primária.
  - **Parcial:** Depende apenas de parte da chave primária.
  - **Transitiva:** Depende de outro atributo que, por sua vez, depende da chave primária.

---

#### **3. Esquemas**

- **Esquema Lógico:** Define a estrutura de tabelas, colunas, chaves e relacionamentos.  
- **Esquema Físico:** Representa como os dados serão armazenados e organizados no sistema de banco de dados.  
- **Boas Práticas:** Documentação, consistência na nomeação e planejamento do desempenho.

---

#### **4. Redundância versus Perda de Dados**

- **Redundância:** Dados armazenados em mais de um local, levando a:
  - Maior uso de espaço.
  - Anomalias de atualização, inserção e exclusão.
- **Perda de Dados:** Falhas no design que resultam na ausência de informações importantes.  
- **Solução:** Normalização e uso de chaves para garantir integridade e evitar inconsistências.

---

#### **5. Valores Nulos**

- Representam a ausência de dados em uma coluna.  
- **Impactos Negativos:** Ambiguidade, problemas em consultas e dificuldades de manutenção.  
- **Boas Práticas:** Definir restrições claras (`NOT NULL`) e usar valores padrão ou funções como `COALESCE` para tratar nulos.

---

### **Conclusão**

Um banco de dados bem projetado equilibra eficiência, integridade e flexibilidade. Aplicar conceitos como normalização, dependências funcionais e esquemas bem definidos reduz riscos de inconsistências e melhora a manutenção do sistema. Projetar com base nas regras de negócio e nas necessidades específicas de cada aplicação é essencial para o sucesso do banco de dados.

---
