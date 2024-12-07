### 1. 1. [2v] De acordo com o modelo relacional normalizado apresentado indique se as seguintes afirmações são verdadeiras ou falsas (risque a resposta errada) e justifique:
#### a. “Na tabela Selecao o campo SiglaPais, apesar de pertencer à chave primária, pode-se repetir.”
Resposta: Verdadeiro  
Justificação: O campo SiglaPais pode repetir-se pois apesar de ser uma chave primária a tabela Selecao possui uma chave primária composta. Dessa forma, permite-se a 
repetição dos campos individualmente mas não permite a repetição do cojunto de campos SiglaPais e Ano. Isto significa que não pode haver duas edições de Copa num mesmo país em um mesmo ano.

#### b. “A tabela Jogador tem duas chaves candidatas.”
Resposta: Falso  
Justificação: Em gestão de bases de dados, as chaves candidatas são atributos ou combinações de atributos que podem ser usados para identificar de forma única cada registro em uma tabela.
Cada tabela pode ter várias chaves candidatas, mas apenas uma delas será escolhida como a chave primária. Considerando individualmente os campos, apenas o campo NumPassporte é chave candidata pois além de 
naturalmente ser um número único para cada pessoa, assim como NIF e identidade, está também com a restrição UNIQUE o que garante que este campo é único para cada registro na tabela. 
Por outro lado, se considerarmos um conjunto de atributos, podemos ter como chave candidata o agrupamento de {SiglaPais, Ano,  NumCamisola} que será único para cada jogador e também o NumPassaporte pelas razões acima mencionadas. 

#### c. “A tabela Patrocinio tem três chaves estrangeiras.”
Resposta: Verdadeiro
Justificação: A tabela Patrocínio possui duas chaves estrangeiras (FK1 e FK2) sendo que FK1 é uma chave estrangeira que referencia uma chave primária composta da tabela Selecao { SiglaPais, Ano} 

#### d. “Na tabela Grupo o campo Edicao está incorreto pois não corresponde a uma chave-primária e por isso não pode ser chave-estrangeira.”
Resposta: Falso
Justificação: A chave primária de uma tabela é um atributo ou conjunto de atributos que identifica de forma única cada tupla (linha) da tabela. No caso da tabela "Grupo", a chave primária é composta por dois atributos: "Edicao" e "Letra". Portanto, "Edicao" faz parte da chave primária e não está incorreto por esse motivo. Uma chave estrangeira é um atributo ou conjunto de atributos que referencia a chave primária de outra tabela. Na tabela "Grupo", o campo "Edicao" é uma chave estrangeira que referencia o campo "Ano" da tabela "EdicaoMundial". Isso indica que cada grupo pertence a uma edição específica da Copa do Mundo.
Edicao faz parte da chave primária de Grupo. Edicao referencia a chave primária de EdicaoMundial, ao mesmo tempo, o campo "Edicao" estabelece um relacionamento entre as tabelas "Grupo" e "EdicaoMundial", agindo como chave estrangeira.

#### 2. [2v] Sabendo que a ligação entre a tabela Golo e a tabela Jogador representa o Jogador que marcou o
Golo, identifique e justifique três erros na representação da tabela Golo:
1. A chave primária está incorretamente vinculada ao campo NumGolo pois um jogador pode ter número de gols idênticos o que não candidata o campo a ser chave primária desta tabela. 
2. Redundância de Informações. Os atributos "SiglaPais" e "NumCamisola" na tabela "Golo" são redundantes. Essa informação já existe na tabela "Jogador", que é referenciada pela chave estrangeira "FK3".
Justificativa: Manter essas informações duplicadas pode levar a inconsistências de dados. Se o número da camisa de um jogador for alterado na tabela "Jogador", essa alteração não será automaticamente refletida na tabela "Golo".
3. A chave estrangeira NumeroJogo está definida como tipo Long sendo que a chave primária que ela referencia na tabela Jogo está definida como Int e as chaves estrangeiras e primárias devem ter o mesmo tipo também o mesmo valor.
#### No espaço abaixo desenhe a tabela Golo corretamente definida:


|      |   Golo     |
|------|-------------|
| PK1  |id_Golo:Int |
|      | MinutoMarcado: Int | 
| FK1  | NumeroJogo: Int |
| FK2  | NumCamisola:Int |

#### 3. [2v] Avalie e justifique as seguintes afirmações, tendo em consideração o modelo relacional:
a. Uma seleção pode ter vários patrocinadores que financiam a participação no mundial com um valor distinto.
Cada seleção pode ter vários patrocinadores pois PatrocinadorOficial é um campo que não possui restrição de ser UNIQUE e também não é chave primária. Nessa mesma linha, para cada patrocinador há um valor distinto

#### b. É possível registar um patrocinador, como patrocinador oficial sem que ele tenha um valor de patrocínio registado.
Segundo a nota ao final do modelo relacional, quando nada é definido em contrário, os campos são de preenchimento obrigatório e os seus valores podem repetir-se. Dessa forma, o campo Valor é de preenchimento obrigatório.

#### [2v] Atendendo aos critérios para a definição de uma chave primária, como avalia a escolha da chave
primária composta da tabela Jogador por comparação com o campo NumPassaporte
A chave primária em um banco de dados relacional deve ser única, não nula, estável (não muda com frequência), simples (preferencialmente um único campo), minimalista (sem atributos redundantes) e eficiente para otimizar consultas e relacionamentos. A escolha deve considerar desempenho, pois campos menores (como inteiros) são mais eficientes que strings longas. Além disso, a chave primária deve facilitar a integridade referencial, sendo frequentemente usada como chave estrangeira em outras tabelas. Portanto, optar por um identificador único e gerado automaticamente (chave substituta) é, na maioria dos casos, a abordagem mais prática e robusta para manter consistência e eficiência no banco de dados. No caso, seria preferível a escolha do campo NumPassaporte como chave primária pois além de único em virtude da restrição UNIQUE (UNICIDADE), é uma chave primária simples e eficiente. 

#### Supondo que se optou por redefinir como chave primária da tabela Jogador o campo NumPassaporte
desenhe as implicações que traria para o modelo relacional:
Se mudarmos a chave primária da tabela Golo para NumPassaporte e garantir a integridade das relações com as demais tabelas, teríamos que criar uma nova tabela Jogador com os campos Nome e NumPassaporte
ligando-se à uma nova tabela intermediária (Jogador_Selecao) usando o campo NumPassaporte como chave estrangeira. 

|      |   Selecao_Jogador    |
|------|-------------|
| PK,FK1 |SiglaPais:Char(3)  |
| PK,FK1 | Ano:Int      | 
| PK  | NumCamisola:Int |
| FK2  | pass_id:Long  |

|      |   Jogador     |
|------|-------------|
| PK  |NumPassaporte:long, UNIQUE |
|      | Nome: Char(100)| 

#### 5. [1v] O que é necessário assegurar nesta base de dados para que seja possível alterar o campo código na
tabela Patrocinador sem que ocorram situações de erro devido ao não cumprimento das regras de
integridade referencial. Justifique
Como o código é chave primária e uma das características desejáveis de uma chave primária é a estabilidade, a sua alteração implica em propagações em outras tabelas pois esta chave primária é referenciada por chaves estrangeiras em outras tabelas. Deeve-se então alterar a chave primária para um valor autoincremental único de modo que a alteração do código do patrocinador não se propague para outras tabelas afetando a integridade das relações entre tabelas. 

#### [2v] A FIFA pretende ter os dados organizados numa estrutura eficiente que permita fazer a análise dos golos marcados por: (i) edição do mundial, (ii) país da seleção, e (iii) jogador. Sobre os golos é
importante saber, em média, a que minuto são marcados e o número total de golos.
Desenhe o modelo dimensional que proporia com base na representação “esquema em estrela” proposto por Kimball. (identifique no esquema as tabelas de factos e as de dimensão)


