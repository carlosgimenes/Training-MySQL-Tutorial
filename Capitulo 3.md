# **Tutorial MySQL: Uma Introdução Objetiva aos Fundamentos do Banco de Dados MySQL**

## Capítulo 3 - Como projetar um banco de dados

Este capítulo revisa os princípios básicos de um projeto de banco de dados, incluindo a normalização. Um banco de dados bem projetado minimiza a redundância, sem perder nenhuma informação. Nosso objetivo será ter a menor quantidade de espaço de armazenamento enquanto mantemos todos os vínculos entre os dados.

### Conceitos e terminologias de banco de dados

Inicialmente, para compreender os princípios que veremos neste capítulo, precisamos estabelecer conceitos básicos e a terminologia que utilizaremos.

### Entidades e relacionamentos

Entidades e relacionamentos são a base do processo de modelagem de dados. As entidades são as coisas do mundo real sobre as quais armazenamos informações. Por exemplo, podemos escolher armazenar informações sobre os funcionários e os departamentos onde eles trabalham. Neste caso, um funcionário seria uma entidade e um departamento seria outra. Os relacionamentos são os vínculos existentes entre esteas entidades: um funcionário trabalha em um departamento, por exemplo. O _**trabalha em**_ é um relacionamento entre as entidades funcionário e departamento.

Os relacionamentos podem ser de tipos diferentes. Podem ser de um para um, um para muitos (ou muitos para um, dependendo da interpretação) ou de muitos para muitos. Um relacionamento de um para um conecta exatamente duas entidades. Se os funcionários nesta organização tivessem um pequeno compartimento cada um, isto seria um relacionamento de um para um. No caso dos funcionários e departamentos, o relacionamento _**trabalha para**_ é geralmente um relacionamento de muitos para um. Isto é, muitos funcionários trabalham para um único departamento, mas cada funcionário trabalha para apenas um departamento. Estes relacionamentos são mostrados abaixo.

![Relacionamento esta localizado em e trabalha para](./images/FiguraRelacionamentoLocalizadoTabalhaPara.png)
_**O relacionamento "está localizado(a) em" é de um para um. O relacionamento "trabalha para" é de muitos para um.**_

Note que as entidades, os relacionamentos e os tipos de relacionamentos dependem do seu ambiente e das regras de negócios que você está tentando modelar. Por exemplo, em algumas empresas, os funcionários podem trabalhar para mais de um departamento. Neste caso, o relacionamento _**trabalha para**_seria de muitos para muitos. Se alguém dividir seu compartimento com outra pessoa, por exemplo, o relacionamento _**está localizado em**_ não será de um para um.

Quando você estiver projetando um banco de dados, terá que levar em conta estas regras para o sistema que estiver modelando. Dois sistemas não serão exatamente iguais.