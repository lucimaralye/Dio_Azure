# Dio_Azure
Exercicios de testes na plataforma Azure

1) Laboratorio de Testes de Machine Learning utilizando a plataforma Azure, onde faremos a leitura de um arquivo csv, e através dos algorítimos de regressão, faremos a previsão de dados futuros.

Para tal experimento, usaremos o arquivo extraído do kaggle, que pode ser acessado através do link: https://www.kaggle.com/code/siamhosaain/house-price-predict-using-knn-and-linearregresion. 
Este arquivo contem informações sobre preço de aluguel de imóveis, baseado em sua metragem, ano de construção, número de quartos, número de banheiros e tipo de vizinhança. 

![image](https://github.com/lucimaralye/Dio_Azure/assets/142181198/2a873ea2-7ee4-4685-8fa5-4f99bf287e02)


Passo 1: Criaremos uma nova atividade de treinamento de Machine Learning no Estúdio de aprendizado de Máquina da plataforma Azure, que pode ser acessada pelo link: azure.microsoft.com.
Esta será uma tarefa de Regressão, onde utilizaremos dois modelos de treinamento: Random Forest (é um modelo de aprendizado de máquina baseado em árvores de decisão) e o Light GBM (é uma implementação eficiente de um algoritmo de boosting que pertence à família de Gradient Boosting Machines. É especialmente eficiente em termos de tempo de treinamento e uso eficiente de memória). 
Para avaliação, utilizaremos a métrica "Root Mean Squared Error - RMSE", que é uma métrica amplamente utilizada na avaliação de modelos de regressão ou previsão, e ela é particularmente útil porque penaliza fortemente erros grandes. 
Para o tipo de validação, escolheremos a opção "Divisão de validação de Treinamento", e isto se justifica porque separar os dados em conjuntos de treinamento e teste é uma prática fundamental em aprendizado de máquina e estatística, isto porque nos permitirá uma simulação de desempenho em ambiente real, prevenção de overfiting, ajuste de hiperparâmetros e avaliação de desempenho do modelo. 
Após o treinamento do modelo, nossa expectativa é informar os dados de entrada, e o modelo nos retornar o valor previsto do aluguel.

https://ml.azure.com/automl/runs/HousingPricePrediction?wsid=/subscriptions/ebe4b236-8ef7-4602-bdad-33a64015fd58/resourceGroups/Laboratorio/providers/Microsoft.MachineLearningServices/workspaces/LaboratioTeste&tid=953d45c9-489b-450c-8508-3412a3ab77e8

Passo 2: Após finalizar o treinamento, será necessário criar um modelo, e então, implantar um "ponto de extremidade", para que possamos fazer o teste de previsão de valores:

![image](https://github.com/lucimaralye/Dio_Azure/assets/142181198/7c7c8e43-4911-4891-ae7a-fc046a29ebdb)

Passo 3: Após a geração do ponto de extremidade, poderemos implantar os dados via Json para recebermos o valor previsto do aluguel: 

![image](https://github.com/lucimaralye/Dio_Azure/assets/142181198/44bb8c2b-3e1b-4daa-93c3-75277685fe53)

Json utilizado:
{
  "input_data": {
    "columns": [
      "SquareFeet",
      "Bedrooms",
      "Bathrooms",
      "Neighborhood",
      "YearBuilt"
    ],
    "data": [
      [1500, 3, 2, "Suburb", 1990],
      [2000, 4, 3, "Urban", 1985],
      [1800, 3, 2, "Rural", 2005]
    ]
  }
}
