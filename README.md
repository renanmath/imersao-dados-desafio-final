
# Desafio Final Imersão Dados

**Olá a todos!**

Esse repositório contém meus resultados do trabalho realizado na terceira edição do Imersão Dados, promovido pela Alura. 
Foi uma semana inteira de trabalho intenso. Aprendi bastante, principalmente pensando nos desafios deixados em cada aula. Estou iniciando na área de dados e ainda tenho muito a aprender, só com esse evento a Alura já me ajudou bastante. 

Um dos motivos pelos quais resolvi participar da Imersão é minha paixão pela área de ciências biológicas. Apesar da minha formação acadêmica formal ser em matemática, biologia sempre foi uma das minhas disciplinas favoritas, e a área de genética também é uma das que mais se destaca em minhas preferências. Apesar disso, sabia pouco ou quase nada sobre drug discovery e pesquisa de fármacos. Durante o evento, agreguei muito conhecimento legal e importante sobre Python e Data Science, mas também aprendi muitas coisas novas sobre biologia, o que foi particularmente delicioso. 

## A pesquisa

Sem mais delongas, vamos falar sobre os detalhes do projeto. O objetivo do projeto é elaborar um estudo dos dados de um experimento de drug discovery, i.e., pesquisa de fármacos. A ideia do projeto foi inspirada em uma competição proposta pelo Laboratory innovation science at Harvard e disponibilizado no keggle nesse link:
https://www.kaggle.com/c/lish-moa


A ideia central é tentar prever quais serão os mecanismos de ação de uma droga (mechanisms of actions, MOA). Nesse tipo de estudo, os cientistas visam identificar uma proteína alvo que está associada a uma doença específica; sabendo disso, busca-se desenvolver fármacos que atuem nessa proteína. A maneira como a molécula do fármaco atua é o seu mecanismo de ação (MOA), que pode ser uma ação inibidora, ativadora, agonista, antagonista, etc. 

A maneira como o estudo no qual esse projeto está baseado atacou o problema foi a seguinte: diversas culturas de células humanas foram testadas com vários compostos e analizou-se a resposta celular à esses compostos, a saber, as expressões gênicas e as viabilidades celulares. Tem-se então um grande conjunto de dados coletados desses ensaios, e esses dados podem ser utilizados por modelos preditivos para prever o comportamento de novos compostos a partir do que o modelo aprendeu com os dados de treino. 

## Os dados
Foram disponibilizados dois conjuntos de dados, coletados a partir desse experimento. O primeiro cojunto contém os dados das expressões gênicas e das viabilidades celulares de cada ensaio realizado. Foram realizados 23814 ensaios, com 3289 compostos distintos, em diferentes dosagens e diferentes tempos de experimento. Desse total de ensaios, 1866 são do grupo de controle. Temos um total de 777 expressões gênicas e 99 tecidos celulares cujas viabilidades foram mensuradas. 
O segundo conjunto de dados reúne os resultados dos experimentos. Temos um total de 206 MOAs e a informaçao de quais deles foram ativados por cada composto analisado. 

## O meu projeto
Eu dividi esse projeto em três partes, que podem ser encontrados nos três arquivos desse repositório. 
No primeiro arquivo (https://github.com/renanmath/imersao-dados-desafio-final/blob/main/Alura_DesafioDados_analise_experimentos.ipynb) encontra-se a análise exploratória dos dados do primeiro data set.
No segundo arquivo (https://github.com/renanmath/imersao-dados-desafio-final/blob/main/Alura_DesafioDados_analise_resultados.ipynb) encontra-se a análise exploratória dos dados do segudo data set.
No terceiro arquivo (https://github.com/renanmath/imersao-dados-desafio-final/blob/main/Alura_ImersaoDados_modelos_preditivos.ipynb) são propostos algums problemas de negócio e são construídos alguns modelos de machine learning que visam resolver esses problemas. Também são propostos problemas futuros, a serem explorados muito em breve. 

Vejamos um resumo dos principais pontos das análises exploratórias:
- Os dados dos experimentos já vieram com um pré-tratamento e a variáveis float estavam normalizadas, seguindo uma curva guassiana. 
- Verificou-se que os experimentos foram realizados em dois cenários de dose do composto (D1 e D2) e três cenários de tempo (24, 48 e 72 horas). As quantidades de experimentos nos seis cenários possíveis estavam balanceados. 
- Constatou-se que apesar de terem sido utilizados 3289 compostos nesses experimento, apenas nove deles possuíam uma frequência relevante, acima de 100 ocorrências. 
- No que diz respeito à expressão gênica g0, os nove compostos mais frequentes apresentaram uma quantidade proporcionalmente baixa de outliers no gráfico boxplot. Porém, quando se analisou o mesmo para os compostos menos frequêntes, constatou-se haver uma proporção enorme de outliers. 
- As viabilidades celulares são altamente correlacionadas. 
- Os MOS que mais foram ativados pelos compostos foram do tipo inibidor, seguindo dos tipos antagonista e agonista. 
- O grupo de controle não ativou nenhum MOA, como era de se esperar.
- Dentre os nove compostos mais frequentes, um deles também não ativou nenhum MOA. Constatou-se que esse composto teve um comportamento semelhante ao do grupo de controle para a expressão gênica g0, no gráfico boxplot.
- Verificou-se que nenhum composto ativou grupos distintos de MOA para diferentes cenários de dose e tempo de experimento, o que também é algo esperado.

Considerei quatro problemas a serem resolvidos usando machine learning:
- Problema 1: prever, a partir das expressões gênicas e viabilidades celuares, se o composto vai ativar pelo menos um MOA. 
- Problema 2: prever, a partir das expressões gênicas e viabilidades celuares, se o composto vai ativar pelo menos um MOA. 
- Problema 3: prever, a partir das expressões gênicas e viabilidades celuares, se o composto vai ativar um MOA específico. Para este problema, foi escolhido um MOA do tipo inibidor, que estava na lista dos mais frequentes. 
- Problema 4: prever, a partir das expressões gênicas e viabilidades celuares, se o composto é ou não do grupo de controle.

Dentre esses, os problemas 3 e 4 são os que considero mais relevantes. Os modelos preditivos tiveram, em média, um desempenho excelente para os problemas 2 e 3, mas deixaram a desejar nos problemas 1 e 4. 

Para cada um dos 4 problemas acima, contruí máquinas preditivas utilizando 8 estratégias distintas de machine learning, a saber:
- Regressão Logística
- Árvore de decisão 
- Floresta aleatória
- Classificador LGBM
- Classificador XGBC
- Gradient Boosting
- Vizinho mais próximo
- Máquina de vetores de suporte

Em todos eles, utilizei os parâmetros padrões. Para cada problema, construí uma tabela com o resumo do desempenho dos 8 modelos. As tabelas contem o nome do modelo, a acurácia, a precisão e a revocação do referido modelo. No geral, para cada problema, todos os modelos tiveram desempenho semelhante, com excessão da árvore de decisão, que foi bem pior que todos os outros modelos no problema 2 e 4. No problema 3, todos os modelos foram excelentes, com mais de 90% em todas as métricas. 

Importante destacar também que como dados de entrada, utilizei todas as expressões gênicas, mas apenas uma viabilidade celular. Tomei essa decisão baseado no fato que as viabilidades celulares são muito correlacionadas.

Ao final do terceiro arquivo, proponho outros 4 problemas que pretendo resolver muito em breve. Pretendo ainda estudar o desempenho das máquinas mudando os parâmetros. 
