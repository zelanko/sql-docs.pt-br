---
title: 'Tutorial do Python: Modelo de treinamento (regressão linear)'
description: Neste tutorial, você usará a regressão linear e Python em SQL Server Serviços de Machine Learning para prever o número de locações de esqui. Você treinará um modelo de regressão linear no Python.
ms.prod: sql
ms.technology: machine-learning
ms.date: 09/03/2019
ms.topic: tutorial
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 30f390681dc63d6de9a95e805b6cc8f273b2b8d7
ms.sourcegitcommit: ecb19d0be87c38a283014dbc330adc2f1819a697
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/04/2019
ms.locfileid: "70242544"
---
# <a name="python-tutorial-train-a-linear-regression-model-in-sql-server-machine-learning-services"></a>Tutorial do Python: Treinar um modelo de regressão linear no SQL Server Serviços de Machine Learning
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Na parte três desta série de tutoriais de quatro partes, você treinará um modelo de regressão linear no Python. Na próxima parte desta série, você implantará esse modelo em um banco de dados SQL Server com Serviços de Machine Learning.

Neste artigo, você aprenderá a:

> [!div class="checklist"]
> * Treinar um modelo de regressão linear
> * Fazer previsões usando o modelo de regressão linear

Na [parte um](python-ski-rental-linear-regression.md), você aprendeu a restaurar o banco de dados de exemplo.

Na [parte dois](python-ski-rental-linear-regression-prepare-data.md), você aprendeu a carregar os dados de SQL Server em um quadro de dados do Python e a preparar os dados no Python.

Na [parte quatro](python-ski-rental-linear-regression-deploy-model.md), você aprenderá a armazenar o modelo para SQL Server e, em seguida, criar procedimentos armazenados a partir dos scripts Python desenvolvidos nas partes dois e três. Os procedimentos armazenados serão executados no SQL Server para fazer previsões com base em novos dados.

## <a name="prerequisites"></a>Pré-requisitos

* A parte três deste tutorial pressupõe que você concluiu a [parte um](python-ski-rental-linear-regression.md) e seus pré-requisitos.

## <a name="train-the-model"></a>Treinar o modelo

Para prever, você precisa encontrar uma função (modelo) que melhor descreva a dependência entre as variáveis em nosso conjunto de mesmos. Isso chamou treinar o modelo. O conjunto de dados de treinamento será um subconjunto de todo o DataSet do data frame do pandas **DF** que você criou na parte dois desta série.

Você treinará o modelo **lin_model** usando um algoritmo de regressão linear.

```python
# Store the variable we'll be predicting on.
target = "RentalCount"

# Generate the training set.  Set random_state to be able to replicate results.
train = df.sample(frac=0.8, random_state=1)

# Select anything not in the training set and put it in the testing set.
test = df.loc[~df.index.isin(train.index)]

# Print the shapes of both sets.
print("Training set shape:", train.shape)
print("Testing set shape:", test.shape)

# Initialize the model class.
lin_model = LinearRegression()

# Fit the model to the training data.
lin_model.fit(train[columns], train[target])
```

Você deverá ver resultados semelhantes ao seguinte.

```results
Training set shape: (362, 7)
Testing set shape: (91, 7)
```

## <a name="make-predictions"></a>Fazer previsões

Use uma função de previsão para prever as contagens de aluguel usando o modelo **lin_model**.

```python
# Generate our predictions for the test set.
lin_predictions = lin_model.predict(test[columns])
print("Predictions:", lin_predictions)
# Compute error between our test predictions and the actual values.
lin_mse = mean_squared_error(lin_predictions, test[target])
print("Computed error:", lin_mse)
```

```results
Predictions: [  40.   38.  240.   39.  514.   48.  297.   25.  507.   24.   30.   54.
   40.   26.   30.   34.   42.  390.  336.   37.   22.   35.   55.  350.
  252.  370.  499.   48.   37.  494.   46.   25.  312.  390.   35.   35.
  421.   39.  176.   21.   33.  452.   34.   28.   37.  260.   49.  577.
  312.   24.   24.  390.   34.   64.   26.   32.   33.  358.  348.   25.
   35.   48.   39.   44.   58.   24.  350.  651.   38.  468.   26.   42.
  310.  709.  155.   26.  648.  617.   26.  846.  729.   44.  432.   25.
   39.   28.  325.   46.   36.   50.   63.]
Computed error: 3.59831533436e-26
```

## <a name="next-steps"></a>Próximas etapas

Na parte três desta série de tutoriais, você concluiu estas etapas:

* Treinar um modelo de regressão linear
* Fazer previsões usando o modelo de regressão linear

Para implantar o modelo de aprendizado de máquina que você criou, siga a parte quatro desta série de tutoriais:

> [!div class="nextstepaction"]
> [Tutorial do Python: Implantar um modelo de aprendizado de máquina](python-ski-rental-linear-regression-deploy-model.md)