<h1 align='center'> Recomendação de Playlist no Spotify </h1>

<!-- <h4 align="center"> 
    :construction:  Projeto em construção  :construction:
</h4>
 -->

![Badge em Desenvolvimento](http://img.shields.io/static/v1?label=STATUS&message=EM%20DESENVOLVIMENTO&color=GREEN&style=for-the-badge)

# Descrição do Projeto 

Projeto que utiliza a técnica de Machine Learning com Aprendizagem Não Supervisionado. Para isso foi utilizada a técnica de clusterização com o algoritmo KMeans. As bases de dados utilizadasf foram extraídas da API do Spotify, e assim foi desenvolvido um "Recomendador de Playlist", que utiliza como variável de entrada uma música desejada pelo usuário e gera 10 músicas para este usuário.

De posse da base de dados da API do Spofity, buscou-se responder a seguinte pergunta para o problema:

* Dado uma música X que eu gosto, quais outras 10 são semelhantes no meu Spotify?

# Tecnologias utilizadas
<div style="display: inline_block"><br/>
    <img align="center" alt="Jupyter" src="https://img.shields.io/badge/Jupyter-F37626.svg?&style=for-the-badge&logo=Jupyter&logoColor=white" />  
    <img align="center" alt="Spotify" src="https://img.shields.io/badge/Spotify-1ED760?&style=for-the-badge&logo=spotify&logoColor=white" />  
    <img align="center" alt="Scikit Learn" src="https://img.shields.io/badge/scikit_learn-F7931E?style=for-the-badge&logo=scikit-learn&logoColor=white" /> 
    <img align="center" alt="Plotly" src="https://img.shields.io/badge/Plotly-239120?style=for-the-badge&logo=plotly&logoColor=white" />
</div><br/>

# Features
Do Spotify foram extraídos 3 bases de dados. Sendo uma que contêm a descrição dos gêneros músicas através de features como acousticness, danceability, energy,popularity, etc. Outra base de dados é a que traz os dados das músicas, contendo features como nome do artista, nome da musica, acousticness, danceability, energy, etc. Por fim , temos também uma base de dados que traz dados a referência entre os anos e features como acousticness, danceability, energy, etc. 

Logo segue a lista das features analisadas no modelo desenvolvido. 

| Feature  | Description |
| ------------- | ------------- |
| year  | ano da música |
| acousticness  | variável que identifica faixa de confiança se a música é acústica  |
| danceability | escreve o quão adequada uma faixa é para dançar com base em uma combinação de elementos musicais |
| duration_ms | duração da trilha em milissegundos |
| energy | representa uma medida perceptiva de intensidade e atividade |
| instrumentalness |prevê se uma faixa não contém vocais |
| liveness | detecta a presença de um público na gravação |
| loudness | volume geral de uma faixa em decibéis (dB) |
| popularity | baseada no número total de execuções que a faixa teve e quão recentes são essas execuções. |
| tempo | tempo estimado geral de uma faixa em batidas por minuto (BPM). |
| speechiness | detecta a presença de palavras faladas em uma faixa |
| valence | descreve a positividade musical transmitida por uma faixa |

# Descrição da Solução 

Solução 
O problema foi classificado como um problema de classificação com aprendizado não supervisionado,  usando aprendizado de máquina com o algoritmo KMeans. A solução foi realizada em ciclos de desenvolvimento de ponta a ponta e pode ser descrita resumidamente (a solução completa junto com os códigos desenvolvidos pode ser vista aqui.) em:

Limpeza e manipulação dos dados
O conjunto de dados contém mais de 1 milhão de linhas e 18 colunas e o trabalho inicialmente realizado foi para a adequação dos tipos de dados no dataframe, seguido pelo tratamento dos valores nulos existentes para as features relacionados aos competidores e promoções estendidas.

Feature Engineering
Aqui, as principais features criadas foram derivadas da data, como o número da semana no ano, o mês e o ano. Devido ao alto número de valores nulos para os atributos de promoções estendidas, foram criadas features mesclando informações sobre promoções e promoções estendidas.

Análise Exploratória de Dados (EDA)
Na análise exploratória de dados foi realizada uma análise para a distribuição de cada uma das variáveis, as relações entre variáveis a partir de uma análise bivariada, matriz de correlações entre variáveis numéricas e correlações entre variáveis categóricas. Também foram realizadas análises acerca do comportamento da variável resposta (sales) para as diferentes variáveis categóricas, como tipo de loja e variedade de produtos.

Por fim, foram levantadas uma śerie de afirmações acerca do que se espera para as vendas de uma loja e algumas delas foram testadas, ajudando a trazer insights para a modelagem do problema.

Seleção de features e transformação
Inicialmente, todas as features sofreram algum tipo de transformação:

Logarítmica: a feature alvo, sales, sofreu transformação logarítimica com o objetivo de tornar a curva mais próxima de uma curva normal.
Rescala: outras features foram aplicados os métodos de RobustScaler e MinMaxScaler, como o ano e a distância até o competidor.
Natureza: features mais relacionadas à data, como o número da semana, mês-ano, sofreu uma transformação de natureza ao serem divididas em uma parcela cosseno e outra parcela seno, com o objetivo de manter a ideia de ciclicidade destas variáveis
Normalização: nenhuma feature foi normalizada.
Com todas as features devidamente transformadas e rescaladas, utilizou-se um regressor de Random Forest e o algoritmo Boruta sobre os dados com o objetivo de extrair informações acerca de quais são as features ou combinações delas que mais trazem informação à tarefa de regressão. Com isso, é possível decidir quais features seguirão para o treinamento e quais serão removidas.

Treinamento dos modelos e validação cruzada ao longo do tempo
A partir das features selecionadas foram treinados diferentes modelos de regressores sobre os dados, como regressão linear, regressão linear regulzarizada, random forest regressor e o XGBoost. Inicialmente, foi realizado um treinamento sobre todos os dados de treinamento, seguindo pela avaliação dos modelos com o conjunto de testes, salvando-se métricas de erro como: erro médio absoluto percentual e erro médio quadrático. Em seguida, foi realizado um treinamento dos modelos em uma valização cruzada ao longo do tempo, dividido em 5 intervalos. As métricas de erro para cada intervalo foram salvas.

Com isso, observou-se que os modelos baseados em regressão linear apresentavam erros muitos altos, da ordem de um modelo simples de média, indicando que estes modelos não estariam ou aprendendo os dados, ou seriam incapazes de capturar bem o fenômeno. O que faz sentido, uma vez que foram observadas relações não lineares entre diferentes variáveis. Os modelos de Random Forest ou XGBoost apresentam métricas muito melhores, sendo o modelo escolhido o XGBoost.

Análise da performance do modelo
Finalmente, com o modelo treinado, tunado, pode-se responder à pergunta levantada pela empresa:

Qual será o total de vendas realizado pela loja X ao longo das próximas 6 semanas? O modelo foi colocado em produção a partir do ambiente de Cloud do Heroku, além da criação de um bot do Telegram que é capaz de responder a pergunta para cada uma das lojas disponíveis para o treinamento. O robô pode ser acessado a partir deste canal do Telegram. Com isso, é possível consultar, a qualquer momento, a previsão de vendas de cada uma das lojas através de uma metodologia única.

Outros pontos a serem observados, considerando a métrica do erro percentual médio absoluto, é possível obter valores para um range estimado para a previsão de vendas para o próximo período (neste caso, 6 semanas). Com isso, o valor previsto de vendas para todas as lojas foi de aproximadamente $279 milhões, com o pior cenário de vendas para $240 milhões e o melhor cenário de vendas aproximadamente a $317 milhões.



Ao observar os resultados do modelo e previsão e seus respectivos erros, observa-se que o modelo apresenta uma pequena tendência em prever valores de vendas menores que o realizado (conforme verifica-se o skewness do erro tendendo para o lado negativo), dessa forma há um certo nível de conservadorismo pelas respostas apresentadas.
# Acesso ao projeto

# Pessoas Contribuidoras

# Pessoas Desenvolvedoras do Projeto

# Licença

# Conclusão
