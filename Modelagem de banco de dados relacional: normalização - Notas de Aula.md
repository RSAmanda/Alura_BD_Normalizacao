# Modelagem de banco de dados relacional: normalização - Notas de Aula

# 01. Normalização de Dados

Dependendo da forma em que o banco de dados é projetado, ele pode trazer problemas de manutenção, como a **Mistura de dados** ou a **Redundância de dados** dentro de uma tabela. As **anomalias de inserção, remoção e alteração tornam as tabelas de um banco de dados pesadas.**

## Diretrizes Informais:

Um conjunto de regras que nos ajudam a identificar a qualidade de um projeto de banco de dados.

- Semântica clara com esquemas fáceis de explicar;
- Evitar informações redundantes;
- Evitar possibilidade informações NULL nas Tuplas;
- Atenção ao surgimento de Tuplas falsas.

## Anomalias:

- Anomalia de Inserção;
- Anomalia de Alteração;
- Anomalia de Remoção.

 > ⚠️ 
 > 
 > O conceito de normalização não se aplica a todos os tipos de bancos de dados. Os **bancos de dados NoSQL**, por exemplo, normalmente armazenam dados não estruturados e possuem uma estrutura de armazenamento bem diferente dos bancos de dados relacionais.

# 02. Dependências, 1FN e 2FN

As **Dependências Funcionais** são restrições aplicadas sobre os atributos da tabela. Ou seja, quando um atributo depende de outro para que a sua existência faça sentido. A dependência funcional estabelece uma relação de atributos na tabela.

Cada forma normal deve satisfazer as propriedades de uma determinada dependência. Assim sendo:

- A **primeira forma normal** deve satisfazer as propriedades baseadas na **dependência funcional.**
- A **segunda forma normal** deve satisfazer as propriedades baseadas na **dependência funcional parcial.**
- A **terceira forma normal** deve satisfazer as propriedades baseadas na **dependência transitiva.**
- A **forma normal de Boyce-Codd** deve satisfazer as propriedades baseadas na **dependência funcional trivial.**
- A **quarta forma normal** deve satisfazer as propriedades baseadas na **dependência Multivalorada**.
- A **quinta forma normal** deve satisfazer as propriedades baseadas na **dependência junção**.

> A dependências funcionais parcial e total só ocorrem quando temos uma chave primária composta. A **dependência funcional parcial** acontecerá quando os atributos não-chave dependem apenas de uma parte da chave primária composta. Já a **dependência funcional total** acontece quando os atributos não-chave dependem da chave primária composta em sua totalidade.
> 

## Primeira Forma Normal - 1FN

<aside>
❔ Quais cuidados devem ser tomados para que uma tabela esteja na primeira forma normal?

</aside>

O primeiro cuidado é **evitar a mistura de assuntos dentro de uma tabela**, porque isso pode causar **repetições ou campos que tenham mais de um valor**, gerando redundância dos dados.

Além disso, quais são os **procedimentos** mais recomendados para **aplicar a regra**? Nós Precisamos **identificar a chave primária** da tabela, o **grupo repetitivo** e **removê-lo** da tabela. Desta forma, criaremos uma tabela nova com esse grupo repetitivo e usaremos a chave primária da tabela que está sendo quebrada como chave estrangeira dentro da tabela nova com o grupo repetitivo.

## Segunda Forma Normal - 2FN

<aside>
❔ Quando uma tabela está na segunda forma normal?

</aside>

Uma tabela está na segunda forma normal - 2FN se ela estiver na primeira forma normal e também se os atributos não-chave dependem da chave composta em sua totalidade. Desta maneira, **a segunda forma normal previne a redundância de dados dentro do banco de dados**.

- Identificar se a tabela tem chave primária composta.
- Identificar os atributos que dependem parcialmente dessa chave primária e criar uma nova tabela com eles.
    - chave parcial será a chave primária dessa nova tabela que nós criaremos.

# 03. 3FN e Boyce-Codd

<aside>
❔ O que é Dependência Transitiva?

</aside>

A **Dependência Funcional Transitiva** ocorre quando um atributo não-chave não depende da chave primária, nem parcialmente, mas depende de outro atributo não-chave. Quando isso acontece, temos a Dependência Funcional Transitiva.

## Terceira Forma Normal - 3FN

<aside>
❔ Quais cuidados devem ser tomados para que uma tabela esteja na terceira forma normal?

</aside>

Para uma tabela estar na terceira forma normal, ela precisa, primeiro, estar na segunda forma normal e não ter nenhum atributo que dependa transitivamente de algum atributo não-chave.

- Identificar todos os atributos que são funcionalmente dependentes de outros atributos não chaves e removê-los.

<aside>
❗ banco de dados está normalizado quando atende à terceira regra normal.

</aside>

## Boyce-Codd

Definimos que uma tabela está na forma normal se e somente se todos os determinantes são chaves candidatas. Há **superposição** quando existem chaves candidatas compostas com o atributo que se repete entre elas.

- identificar todos os atributos determinados por outro atributo que não uma chave candidata.
- removê-los e levá-los para outra tabela.

# 04. Quarta Forma Normal - 4FN

<aside>
❔ O que é Dependência Multivalorada?

</aside>

Na **dependência multivalorada**, o atributo determina um conjunto de valores de um atributo.

> A dependência funcional é representada por **X -> Y** (X determina funcionalmente Y) e a dependência multivalorada é representada por **X ->> Y** (X determina multivalores em Y). Na multivalorada, há um sinal de "menor (>)" a mais que na dependência funcional. Neste caso, lemos que **X multi determina Y** ou que **Y é multi dependente de X**.
> 

## Quarta Forma Normal  - 4FN

<aside>
❔ Quais cuidados devem ser tomados para que uma tabela esteja na quarta forma normal?

</aside>

- Estar na terceira forma normal
- Não ter mais de um atributo multivalorado
    
    <aside>
    ❗ Ou seja, não pode existir dependência multivalorada.
    
    </aside>
    

Procedimentos:

- Identificar se existe um multi-determinante que aponte para mais de um multi-dependente.
- Identificar se existe independências entre esses multi-dependentes.

# 05. Quinta Forma Normal - 5FN

## Dependência de Junção

Uma tabela é **n-decomponível** quando pode ser dividida em mais de duas. Logo, n é maior que dois. Esse conceito só pode ser aplicado em tabelas com mais de três atributos.

## Quinta Forma Normal - 5FN

<aside>
❔ O que é a quinta forma normal?

</aside>

Uma tabela está na **Quinta Forma Normal - 5FN** se estiver na quarta forma normal e se não houver dependência de junção.

A **Quinta Forma Normal** trata de casos onde as informações podem ser recuperadas através de tabelas menores.

> Na quinta forma normal precisamos aplicar a constante simétrica, se existir uma nova regra de negócios na tabela, e atribuir as responsabilidades a esquemas específicos.
> 

<aside>
❗ Para aplicarmos a quinta forma normal, precisamos conhecer os conceitos de decomposição sem perdas e de junção. Levando assim a ser conhecida como a forma normal de projeção-junção.

</aside>
