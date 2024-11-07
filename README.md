
## Sumário
- [Modelo Prêmio de Risco de Colisões Parciais](#modelo-prêmio-de-risco-de-colisões-parciais)
- [CatBoost](#catboost)
  - [Variáveis](#variáveis)
  - [Hiperparâmetros](#hiperparâmetros)
- [Instruções](#instruções)
- [Equipe](#equipe)

# Modelo Prêmio de Risco de Colisões Parciais

O seguinte repositório tem como projeto desenvolver um modelo eficaz para estimar o Prêmio de Risco de Colisões Parciais em um mercado de seguros, para estimar com precisão o risco que cada cliente ou perfil representa para uma seguradora, buscando um equilíbrio vantajoso entre aceitação e rentabilidade.

# CatBoost

Para estimar o modelo foi utilizado o CatBoost, um algoritmo de aprendizado de máquina desenvolvido para lidar com dados categóricos de forma eﬁciente. O CatBoost utiliza uma abordagem de *gradient boosting* que se diferencia pelo tratamento especial de variáveis categóricas. Ele transforma essas variáveis em números de maneira inteligente, permitindo que o modelo aprenda padrões complexos sem a necessidade de pré-processamento extenso dos dados. 
Esses fatores levam a vantagens como alta precisão, capacidade de lidar com dados categóricos diretamente e resistência ao *overﬁtting*. O nosso código configura e treina um modelo `CatBoostRegressor` com função de perda Tweedie para modelagem preditiva, ajustando diversos hiperparâmetros para otimizar a precisão e evitar sobreajuste.

## Variáveis

Em nosso código realizamos as seguintes operações:

1.  **Definição das Variáveis**:
    
    -   Definimos as listas de variáveis independentes (`features`), variáveis categóricas (`cat_features`) e a variável dependente (`target`), que será o alvo da previsão.
2.  **Divisão dos Dados**:
    
    -   O DataFrame `df` é dividido em dois conjuntos: um para treinamento (`df_train`) e outro para teste (`df_test`). A divisão é feita de forma aleatória, garantindo que os dados de treino e teste sejam representativos.

Essas operações preparam os dados para treinamento de um modelo preditivo, separando as variáveis relevantes e organizando os dados em conjuntos de treino e teste.

## Hiperparâmetros

Na função CatBoostRegressor, é possível modificar hiperparâmetros presentes para a melhora da estimativa do modelo de cada perfil. Em seguida explico brevimente cada hiperparâmetro modificado e sua função.
-   **`loss_function='Tweedie:variance_power=1.5'`**: Define a função de perda Tweedie, com `variance_power=1.5`, apropriada para modelagem de dados com variabilidade alta ou características de dispersão.
-   **`n_estimators=500`**: Número de árvores a serem construídas, ajustado para um valor menor para evitar sobreajuste.
-   **`depth=6`**: Profundidade das árvores, reduzindo a complexidade do modelo para equilibrar generalização e desempenho.
-   **`learning_rate=0.1`**: Taxa de aprendizado aumentada, acelerando a convergência do modelo.
-   **`l2_leaf_reg=3`**: Regularização L2 aplicada nas folhas, ajudando a evitar overfitting.
-   **`bagging_temperature=0.8`**: Controle do processo de bagging, ajustando a aleatoriedade na amostragem dos dados.
-   **`random_strength=1.5`**: Controla a força de aleatoriedade na divisão dos nós, útil para reduzir a variabilidade entre árvores.
-   **`min_data_in_leaf=10`**: Define o número mínimo de amostras por folha, evitando divisões em nós com poucas amostras.
-   **`task_type='CPU'`**: Define o uso de CPU para o processamento do modelo.

# Instruções

Para executar a main, é necessário baixar o arquivo train.csv e adiciona-lo ao seu drive em uma pasta nomeada "sest_datathon_24". O arquivo pode ser encontrado [nesse link](https://drive.google.com/file/d/1vJOiOOsifeKh7lROcnnP3kPj1QdYTXtn/view).

# Equipe

Esse projeto foi desenvolvido durante o Datathon da SEst - 2024, por Angêlo Ântonio Bertoli Guido, Bruna Gongora Bariccatti e Eduarda Fritzen Neumann.
