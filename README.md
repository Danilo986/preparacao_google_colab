Engenharia de Atributos e Modelagem Preditiva em Big Data com PySpark

Este projeto contempla o pipeline de "limpeza, transformação de dados, engenharia de atributos (Feature Engineering) e regressão preditiva" utilizando "PySpark", processando dados de engajamento de vídeos e comentários de redes sociais.



	 Objetivo do Projeto

Analisar métricas de engajamento de conteúdo (curtidas, visualizações, palavras-chave) para criar atributos numéricos e "prever a quantidade de comentários (`Comments`)" que um vídeo receberá, utilizando algoritmos de Machine Learning distribuído.



Tecnologias e Ferramentas Utilizadas

Linguagem: Python 3.12
Framework de Big Data: PySpark (Spark SQL & Spark MLlib)
Formato de Armazenamento: Apache Parquet
Ambiente de Desenvolvimento: Google Colab / Jupyter Notebook



	Etapas do Pipeline de Dados

1.   Leitura e Tratamento Inicial:
     Leitura de arquivo otimizado no formato `.parquet`.
     Remoção de duplicatas com base no `Video ID`.
     Descarte de colunas não estruturadas de comentários e sentimentos para foco nas métricas do vídeo.
     Caching do DataFrame em memória para otimização de performance.

2.  Engenharia de Atributos (Feature Engineering):
       Extração Temporal: Criação da coluna `Month` a partir da data de publicação (`Published At`).
       Categorização Coded: Codificação da coluna categórica `Keyword` em valores numéricos utilizando `StringIndexer`.
       Vetorização: Agrupamento das variáveis preditoras (`Likes`, `Views`, `Year`, `Month`, `Keyword Index`) em um vetor de características com `VectorAssembler`.
       Normalização: Escalonamento dos dados preditores via `MinMaxScaler`.
       Redução de Dimensionalidade: Aplicação de PCA (Principal Component Analysis) para compressão dos atributos.

3.   Modelagem Preditiva (Machine Learning):
     Divisão dos dados em conjuntos de "Treino (80%)" e "Teste (20%)" com `randomSplit`.
     Treinamento de um algoritmo de Regressão Linear (`LinearRegression`) para predição da variável alvo `Comments`.

4. Persistência dos Dados:
     Salvamento do DataFrame final transformado em formato distribuído `.parquet`.



    Resultados da Modelagem

A avaliação do modelo no conjunto de dados de teste apresentou as seguintes métricas:

 Métrica | Valor | Descrição |

  RMSE (Erro Quadrático Médio da Raiz) | `13146.33`| Margem média de erro na estimativa de comentários. |
  $R^2$ (Coeficiente de Determinação) | `0.8056`  | 80.56% da variação na quantidade de comentários é explicada pelo modelo. |

>   Conclusão:   O modelo apresentou uma forte capacidade explicativa ($R^2 \approx 80,5\%$), demonstrando que o volume de visualizações, curtidas e a categoria/palavra-chave são preditores de alto impacto para o engajamento de usuários.
