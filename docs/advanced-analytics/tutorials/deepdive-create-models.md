---
title: Criar modelos de R (SQL e R mergulho profundo) | Microsoft Docs
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: a2f6e9b23e1592073c1b21bc41e4975ffaf17075
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32446840"
---
# <a name="create-r-models-sql-and-r-deep-dive"></a>Criar modelos de R (SQL e R mergulho profundo)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Este artigo faz parte do tutorial mergulho profundo de ciência de dados, como usar [RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) com o SQL Server.

Agora que você incrementou os dados de treinamento, é hora de analisar os dados usando a regressão linear. Modelos lineares são uma ferramenta importante no mundo da análise preditiva e o pacote **RevoScaleR** do [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] inclui um algoritmo escalonável e de alto desempenho.

## <a name="create-a-linear-regression-model"></a>Criar um modelo de regressão linear

Nesta etapa, você cria um modelo linear simples que calcula o saldo de cartão de crédito para os clientes, usando como variáveis independentes, os valores de *sexo* e *creditLine* colunas.
  
Para fazer isso, use o [rxLinMod](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxlinmod) função, que oferece suporte para contextos de computação remota.
  
1. Crie uma variável de R para armazenar concluído modelo e chame **rxLinMod**, passando uma fórmula apropriada.
  
    ```R
    linModObj <- rxLinMod(balance ~ gender + creditLine,  data = sqlFraudDS)
    ```
  
2. Para exibir um resumo dos resultados, chame o R padrão `summary` função no objeto de modelo.
  
     ```R
     summary(linModObj)
     ```

Você pode pensar peculiares que uma função R simples como `summary` funcionaria aqui, como na etapa anterior, você deve definir o contexto de computação para o servidor. No entanto, mesmo que a função **rxLinMod** use o contexto de computação remota para criar o modelo, ela também retorna um objeto que contém o modelo para sua estação de trabalho local e o armazena no diretório compartilhado.

Portanto, você pode executar comandos padrão do R com relação ao modelo como se ele tivesse sido criado usando o contexto "local".

**Resultados**

```
Linear Regression Results for: balance ~ gender + creditLineData: sqlFraudDS (RxSqlServerData Data Source)
Dependent variable(s): balance
Total independent variables: 4 (Including number dropped: 1)
Number of valid observations: 10000
Number of missing observations: 0
Coefficients: (1 not defined because of singularities)

Estimate Std. Error t value Pr(>|t|) (Intercept)
3253.575 71.194 45.700 2.22e-16
gender=Male -88.813 78.360 -1.133 0.257
gender=Female Dropped Dropped Dropped Dropped
creditLine 95.379 3.862 24.694 2.22e-16
Signif. codes: 0  0.001  0.01 ‘*’ 0.05 ‘.’ 0.1 ‘ ’ 1

Residual standard error: 3812 on 9997 degrees of freedom
Multiple R-squared: 0.05765
Adjusted R-squared: 0.05746
F-statistic: 305.8 on 2 and 9997 DF, p-value: < 2.2e-16
Condition number: 1.0184
```

## <a name="create-a-logistic-regression-model"></a>Criar um modelo de regressão logística

Em seguida, você pode criar um modelo de regressão logística que indica se um cliente específico é um risco de fraude. Você usará o **RevoScaleR** [rxLogit](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxlogit) função, que suporta o ajuste dos modelos de regressão logística remoto contextos de computação.

1.  Deixe o contexto de computação como está. Você continuará usando a mesma fonte de dados também.

2.  Chame a função **rxLogit** e passe a fórmula necessária para definir o modelo.

    ```R
    logitObj <- rxLogit(fraudRisk ~ state + gender + cardholder + balance + numTrans + numIntlTrans + creditLine, data = sqlFraudDS, dropFirst = TRUE)
    ```
  
    Como ele é um modelo grande, que contém 60 variáveis independentes, incluindo três variáveis fictícias removidas, talvez você precise aguardar até que o contexto de computação retorne o objeto.
    
    O motivo pelo qual o modelo é tão grande é que, no R e no pacote **RevoScaleR** , todos os níveis de uma variável de fator categórico são tratados automaticamente como uma variável fictícia separada.
  
3.  Para exibir um resumo do modelo retornado, chame o R `summary` função.
  
    ```R
    summary(logitObj)
    ```
  
**Resultados parciais**

```
Logistic Regression Results for: fraudRisk ~ state + gender + cardholder + balance + numTrans + numIntlTrans + creditLine
Data: sqlFraudDS (RxSqlServerData Data Source)
Dependent variable(s): fraudRisk
Total independent variables: 60 (Including number dropped: 3)
Number of valid observations: 10000 -2

LogLikelihood: 2032.8699 (Residual deviance on 9943 degrees of freedom)

Coefficients:
Estimate Std. Error z value Pr(>|z|)     (Intercept)
-8.627e+00  1.319e+00  -6.538 6.22e-11
state=AK                Dropped    Dropped Dropped  Dropped
state=AL             -1.043e+00  1.383e+00  -0.754   0.4511

(other states omitted)

gender=Male             Dropped    Dropped Dropped  Dropped
gender=Female         7.226e-01  1.217e-01   5.936 2.92e-09
cardholder=Principal    Dropped    Dropped Dropped  Dropped
cardholder=Secondary  5.635e-01  3.403e-01   1.656   0.0977
balance               3.962e-04  1.564e-05  25.335 2.22e-16
numTrans              4.950e-02  2.202e-03  22.477 2.22e-16
numIntlTrans          3.414e-02  5.318e-03   6.420 1.36e-10
creditLine            1.042e-01  4.705e-03  22.153 2.22e-16

Signif. codes:  0 ‘\*\*\*’ 0.001 ‘\*\*’ 0.01 ‘\*’ 0.05 ‘.’ 0.1 ‘ ’ 1
Condition number of final variance-covariance matrix: 3997.308
Number of iterations: 15
```

## <a name="next-step"></a>Próxima etapa

[Novos dados de pontuação](../../advanced-analytics/tutorials/deepdive-score-new-data.md)

## <a name="previous-step"></a>Etapa anterior

[Visualizar dados do SQL Server usando o R](../../advanced-analytics/tutorials/deepdive-visualize-sql-server-data-using-r.md)
