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
