---
title: 'Tutorial do Python: Treinar um modelo'
titleSuffix: SQL machine learning
description: Na parte três desta série de tutoriais de quatro partes, você treinará um modelo de regressão linear em Python para prever os aluguéis de esqui com o aprendizado de máquina do SQL.
ms.prod: sql
ms.technology: machine-learning
ms.date: 05/21/2020
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=azuresqldb-mi-current'
ms.openlocfilehash: ef7dd974d77b60d3b03cf8799f7707481f32e91d
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97470367"
---
# <a name="python-tutorial-train-a-linear-regression-model-with-sql-machine-learning"></a>Tutorial do Python: Treinar um modelo de regressão linear com o aprendizado de máquina do SQL
[!INCLUDE [SQL Server 2017 SQL MI](../../includes/applies-to-version/sqlserver2017-asdbmi.md)]

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15"
Na parte três desta série de tutoriais de quatro partes, você treinará um modelo de regressão linear no Python. Na próxima parte desta série, você implantará esse modelo em um banco de dados do SQL Server com os Serviços de Machine Learning ou nos Clusters de Big Data.
::: moniker-end
::: moniker range="=sql-server-2017"
Na parte três desta série de tutoriais de quatro partes, você treinará um modelo de regressão linear no Python. Na próxima parte desta série, você implantará esse modelo em um banco de dados do SQL Server com os Serviços de Machine Learning.
::: moniker-end
::: moniker range="=azuresqldb-mi-current"
Na parte três desta série de tutoriais de quatro partes, você treinará um modelo de regressão linear no Python. Na próxima parte desta série, você implantará esse modelo em um banco de dados da Instância Gerenciada de SQL do Azure com Serviços de Machine Learning.
::: moniker-end

Neste artigo, você aprenderá a:

> [!div class="checklist"]
> * Treinar um modelo de regressão linear
> * Fazer previsões usando o modelo de regressão linear

Na [parte um](python-ski-rental-linear-regression.md), você aprendeu a restaurar o banco de dados de exemplo.

Na [parte dois](python-ski-rental-linear-regression-prepare-data.md), você aprendeu a carregar os dados de um banco de dados em uma estrutura de dados do Python e a prepará-los no Python.

Na [parte quatro](python-ski-rental-linear-regression-deploy-model.md), você aprenderá a armazenar o modelo em um banco de dados e, em seguida, criará procedimentos armazenados com base nos scripts do Python desenvolvidos nas partes dois e três. Os procedimentos armazenados serão executados no servidor para fazer previsões com base em novos dados.

## <a name="prerequisites"></a>Pré-requisitos

* A parte três deste tutorial pressupõe que você concluiu a [parte um](python-ski-rental-linear-regression.md) e os respectivos pré-requisitos.

## <a name="train-the-model"></a>Treinar o modelo

Para prever, você precisa encontrar uma função (modelo) que melhor descreva a dependência entre as variáveis em nosso conjunto de dados. Isso se chama treinar o modelo. O conjunto de dados de treinamento será um subconjunto de todo o conjunto de dados da estrutura de dados **df** do Pandas que você criou na parte dois desta série.

Você treinará o modelo **lin_model** usando um algoritmo de regressão linear.

```python
# Store the variable we'll be predicting on.
target = "Rentalcount"

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

Você deverá ver resultados semelhantes aos seguintes.

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

Você deverá ver resultados semelhantes aos seguintes.

```results
Predictions: [ 40.  38. 240.  39. 514.  48. 297.  25. 507.  24.  30.  54.  40.  26.
  30.  34.  42. 390. 336.  37.  22.  35.  55. 350. 252. 370. 499.  48.
  37. 494.  46.  25. 312. 390.  35.  35. 421.  39. 176.  21.  33. 452.
  34.  28.  37. 260.  49. 577. 312.  24.  24. 390.  34.  64.  26.  32.
  33. 358. 348.  25.  35.  48.  39.  44.  58.  24. 350. 651.  38. 468.
  26.  42. 310. 709. 155.  26. 648. 617.  26. 846. 729.  44. 432.  25.
  39.  28. 325.  46.  36.  50.  63.]
Computed error: 2.9960763804270902e-27
```

## <a name="next-steps"></a>Próximas etapas

Na parte três desta série de tutoriais, você concluiu estas etapas:

* Treinar um modelo de regressão linear
* Fazer previsões usando o modelo de regressão linear

Para implantar o modelo de machine learning que você criou, siga a parte quatro desta série de tutoriais:

> [!div class="nextstepaction"]
> [Tutorial do Python: Implantar um modelo de machine learning](python-ski-rental-linear-regression-deploy-model.md)
