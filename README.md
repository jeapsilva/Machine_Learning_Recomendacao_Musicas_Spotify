<h1 align='center'> Recomendação de Playlist no Spotify </h1>

<!-- <h4 align="center"> 
    :construction:  Projeto em construção  :construction:
</h4>
 -->

![Badge em Desenvolvimento](http://img.shields.io/static/v1?label=STATUS&message=EM%20DESENVOLVIMENTO&color=GREEN&style=for-the-badge)

# Descrição do Projeto 

Projeto que utiliza Clustering, técnica de Machine Learning com Aprendizagem Não Supervisionado. Para isso foi utilizado o algoritmo KMeans. As bases de dados utilizadas foram extraídas com a API do Spotify, e assim desenvolveu-se um "Recomendador de Playlist", que utiliza como variável de entrada uma música desejada pelo usuário e gera uma playlist contendo 10 músicas para este usuário.

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

| Feature  | Descrição |
| ------------- | ------------- |
| year  | ano da música |
| acousticness  | variável que identifica, a partir de uma faixa de confiança se a música é acústica  |
| danceability | mede o quão a faixa é boa para dançar com base em uma combinação de elementos musicais |
| duration_ms | duração da trilha em milissegundos |
| energy | representa uma medida perceptiva de intensidade e atividade |
| instrumentalness | prevê se uma faixa não contém vocais |
| liveness | detecta a presença de um público na gravação |
| loudness | volume geral de uma faixa em decibéis (dB) |
| popularity | baseada no número total de execuções que a faixa teve e quão recentes são essas execuções |
| tempo | tempo estimado geral de uma faixa em batidas por minuto (BPM). |
| speechiness | detecta a presença de palavras faladas em uma faixa |
| valence | descreve a positividade musical transmitida por uma faixa |

# Descrição da Solução 

Solução 
O problema foi classificado como um problema de classificação com aprendizado não supervisionado, usando aprendizado de máquina com o algoritmo KMeans. A solução foi realizada em ciclos de desenvolvimento de ponta a ponta e pode ser descrita resumidamente, a solução completa pode ser encontrada no algoritmo disponibilizado nesse repositório.

**Limpeza e manipulação dos dados**
O conjunto de dados principal contém 20311 de linhas e 19 colunas. A limpeza e manipulação realizada foi para verificação de dados ausentes, busca por outliers, e valores NaN. 

**Feature Engineering**

O trabalho inicialmente realizado foi para a adequação de variáveis do tipo categóricas, que não são aceitos por modelos de Machine Learning. Para isso utilizamos o encoder OneHotEncoder para a transformação dessas variáveis em variáveis dummies. A variável que foi submetida essa transformação foi a "artists" que contêm 875 variações presentes no dataset. 

**Análise Exploratória de Dados (EDA)**

Na análise exploratória de dados foi realizada uma análise para a distribuição de cada uma das variáveis, as relações entre variáveis a partir da matriz de correlação. A partir disso, no

**Seleção de features e transformação**

Inicialmente, todas as features sofreram algum tipo de transformação:

Rescala: As features sofreram normalização dos dados para que todos fiquem em uma distribuição em escala próximas. Para isso utilizou-se o StandardScaler. Vale lembrar também que como o KMeans utiliza a distância euclidiana, essa rescala é necessária pois este algoritmo é sensível a escalas diferentes. 
Redução de dimensionalidade: Conforme dito anteriormente, ao transformar variáveis em dummies, a base de dados ficou com mais de 875 colunas. Para a redução de dimensionalidade utilizou-se a análise de componentes princiais (PCA).

Com todas as features devidamente transformadas e rescaladas, utilizou-se um Classificador KMeans.

**Análise do Modelo**

Um bom cluster tem uma baixa inertia_ (SSE) e também o menor número de clusters. Logo não queremos muitos clusters. A Curva de Cotovelo ou Método Elbow Curve é uma técnica usada para encontrar a quantidade ideal de clusters K. Este método testa a variância dos dados em relação ao número de clusters. O valor ideal de K é aquele que tem um menor Within Sum of Squares (WSS) e ao mesmo tempo o menor número de clusters. Chamamos de curva de cotovelo, porque a partir do ponto que seria o “cotovelo” não existe uma discrepância tão significativa em termos de variância. Dessa forma, a melhor quantidade de clusters K seria exatamente onde o cotovelo estaria. A curva de cotovelo 

<p align="center">
  <img src="img_elbow" />
</p>

# Resultado

Por fim, conforme podemos analisar no gráfico de elbow, quando há uma curva acentuada que forme quase o cotovelo, há portanto o valor ótimo de cluster para o desenvolvimento do modelo. Com isso nosso cluster já está treinado e classificando os dados de modo desejável. A seguir mostramos a playlist recomendada para a música do cantor Ed Sheeran - Shape of You.

<p align="center">
  <img src="playlist-ed-sheeran" />
</p>

# Ferramentas utilizadas 

**Data manipulation and cleaning:** pandas, numpy, PCA, StandarScaler.

**Data visualization:** Plotly.

**Machine learning:** Clustering (Kmeans).

# Pessoas Desenvolvedoras do Projeto

<a href="https://github.com/jesapsilva">Jéssica Aparecida Silva - Cientista de dados</a>
<a href="https://www.linkedin.com/in/jessica-aparecida-silva/">Linkedin</a>

# Licença

# Conclusão
