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
