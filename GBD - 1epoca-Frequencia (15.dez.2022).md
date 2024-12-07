*1. 1. [2v] De acordo com o modelo relacional normalizado apresentado indique se as seguintes afirmações são verdadeiras ou falsas (risque a resposta errada) e justifique:*
a. “Na tabela Selecao o campo SiglaPais, apesar de pertencer à chave primária, pode-se repetir.”
Resposta: Verdadeiro
Justificação: O campo SiglaPais pode repetir-se pois apesar de ser uma chave primária a tabela Selecao possui uma chave primária composta. Dessa forma, permite-se a 
repetição dos campos individualmente mas não permite a repetição do cojunto de campos SiglaPais e Ano. Isto significa que não pode haver duas edições de Copa num mesmo país em um mesmo ano.

*b. “A tabela Jogador tem duas chaves candidatas.”*
Resposta: Falso
Justificação: Em gestão de bases de dados, as chaves candidatas são atributos ou combinações de atributos que podem ser usados para identificar de forma única cada registro em uma tabela.
Cada tabela pode ter várias chaves candidatas, mas apenas uma delas será escolhida como a chave primária. Considerando individualmente os campos, apenas o campo NumPassporte é chave candidata pois além de 
naturalmente ser um número único para cada pessoa, assim como NIF e identidade, está também com a restrição UNIQUE o que garante que este campo é único para cada registro na tabela. 
Por outro lado, se considerarmos um conjunto de atributos, podemos ter como chave candidata o agrupamento de {SiglaPais, Ano,  NumCamisola} que será único para cada jogador e também o NumPassaporte pelas razões acima mencionadas. 


