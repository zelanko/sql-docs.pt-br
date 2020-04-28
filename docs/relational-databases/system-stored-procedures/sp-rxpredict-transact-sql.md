---
title: sp_rxPredict | Microsoft Docs
ms.date: 03/31/2020
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: machine-learning
ms.topic: language-reference
f1_keywords:
- sp_rxPredict
- sp_rxPredict_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_rxPredict procedure
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: 9663b4cd51a7aca9e9e30ccafcdcb0652ec4229a
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81488524"
---
# <a name="sp_rxpredict"></a>sp_rxPredict  
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly.md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Gera um valor previsto para uma determinada entrada que consiste em um modelo de aprendizado de máquina armazenado em um formato binário em um banco de dados SQL Server.

Fornece Pontuação em modelos de aprendizado de máquina R e Python quase em tempo real. `sp_rxPredict`é um procedimento armazenado fornecido como um wrapper para a `rxPredict` função R em [RevoScaleR](https://docs.microsoft.com/r-server/r-reference/revoscaler/revoscaler) e [MicrosoftML](https://docs.microsoft.com/r-server/r-reference/microsoftml/microsoftml-package), e a função [rx_predict](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-predict) Python em [revoscalepy](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/revoscalepy-package) e [MicrosoftML](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package). Ele é escrito em C++ e é otimizado especificamente para operações de pontuação.

Embora o modelo deva ser criado usando R ou Python, depois que ele é serializado e armazenado em um formato binário em uma instância do mecanismo de banco de dados de destino, ele pode ser consumido nessa instância do mecanismo de banco de dados, mesmo quando a integração do R ou do Python não está instalada. Para obter mais informações, consulte [Pontuação em tempo real com sp_rxPredict](https://docs.microsoft.com/sql/machine-learning/real-time-scoring).

## <a name="syntax"></a>Sintaxe

```
sp_rxPredict  ( @model, @input )
```

### <a name="arguments"></a>Argumentos

**modelo**

Um modelo pretreinado em um formato com suporte. 

**entrada**

Uma consulta SQL válida

### <a name="return-values"></a>Valores retornados

Uma coluna de pontuação é retornada, bem como quaisquer colunas de passagem da fonte de dados de entrada.
Colunas de Pontuação adicionais, como o intervalo de confiança, podem ser retornadas se o algoritmo der suporte à geração desses valores.

## <a name="remarks"></a>Comentários

Para habilitar o uso do procedimento armazenado, o SQLCLR deve estar habilitado na instância.

> [!NOTE]
> Há implicações de segurança para enabing essa opção. Use uma implementação alternativa, como a função de [previsão Transact-SQL](https://docs.microsoft.com/sql/t-sql/queries/predict-transact-sql?view=sql-server-2017) , se o SQLCLR não puder ser habilitado no servidor.

O usuário precisa `EXECUTE` de permissão no banco de dados.

### <a name="supported-algorithms"></a>Algoritmos compatíveis

Para criar e treinar o modelo, use um dos algoritmos com suporte para R ou Python, fornecido por [SQL Server serviços de Machine Learning (r ou Python)](https://docs.microsoft.com/sql/machine-learning/sql-server-machine-learning-services), [SQL Server 2016 r Services](https://docs.microsoft.com/sql/machine-learning/r/sql-server-r-services), [SQL Server Machine Learning Server (autônomo) (r ou Python)](https://docs.microsoft.com/sql/machine-learning/r/r-server-standalone)ou [SQL Server 2016 r Server (autônomo)](https://docs.microsoft.com/sql/machine-learning/r/r-server-standalone?view=sql-server-2016).

#### <a name="r-revoscaler-models"></a>R: modelos de RevoScaleR

  + [rxLinMod](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxlinmod)
  + [rxLogit](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxlogit)
  + [rxBTrees](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxbtrees)
  + [rxDtree](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxdtree)
  + [rxdForest](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxdforest)

#### <a name="r-microsoftml-models"></a>R: modelos de MicrosoftML

  + [rxFastTrees](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxfasttrees)
  + [rxFastForest](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxfastforest)
  + [rxLogisticRegression](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxlogisticregression)
  + [rxOneClassSvm](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxoneclasssvm)
  + [rxNeuralNet](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxneuralnet)
  + [rxFastLinear](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxfastlinear)

#### <a name="r-transformations-supplied-by-microsoftml"></a>R: transformações fornecidas por MicrosoftML

  + [featurizeText](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxfasttrees)
  + [Concat](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/concat)
  + [categorical](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/categorical)
  + [categoricalHash](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/categoricalHash)
  + [selectFeatures](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/selectFeatures)

#### <a name="python-revoscalepy-models"></a>Python: modelos de revoscalepy

  + [rx_lin_mod](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-lin-mod)
  + [rx_logit](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-logit)
  + [rx_btrees](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-btrees)
  + [rx_dtree](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-dtree)
  + [rx_dforest](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-dforest)


#### <a name="python-microsoftml-models"></a>Python: modelos de microsoftml

  + [rx_fast_trees](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-fast-trees)
  + [rx_fast_forest](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-fast-forest)
  + [rx_logistic_regression](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-logistic-regression)
  + [rx_oneclass_svm](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-oneclass-svm)
  + [rx_neural_network](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-neural-network)
  + [rx_fast_linear](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-fast-linear)

#### <a name="python-transformations-supplied-by-microsoftml"></a>Python: transformações fornecidas por microsoftml

  + [featurize_text](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-fast-trees)
  + [Concat](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/concat)
  + [categorical](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/categorical)
  + [categorical_hash](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/categorical-hash)
  
### <a name="unsupported-model-types"></a>Tipos de modelos sem suporte

Não há suporte para os seguintes tipos de modelo:

+ Modelos que usam `rxGlm` os `rxNaiveBayes` algoritmos ou no RevoScaleR
+ Modelos de PMML em R
+ Modelos criados usando outras bibliotecas de terceiros 

## <a name="examples"></a>Exemplos

```sql
DECLARE @model = SELECT @model 
FROM model_table 
WHERE model_name = 'rxLogit trained';

EXEC sp_rxPredict @model = @model,
@inputData = N'SELECT * FROM data';
```

Além de ser uma consulta SQL válida, os dados de entrada em * \@inputData* devem incluir colunas compatíveis com as colunas no modelo armazenado.

`sp_rxPredict`dá suporte apenas aos seguintes tipos de coluna .NET: Double, float, short, ushort, Long, ULong e String. Talvez seja necessário filtrar tipos sem suporte em seus dados de entrada antes de usá-los para pontuação em tempo real. 

  Para obter informações sobre os tipos SQL correspondentes, confira [Mapeamento de tipos SQL-CLR](/dotnet/framework/data/adonet/sql/linq/sql-clr-type-mapping) ou [Mapeamento de dados de parâmetro CLR](../clr-integration-database-objects-types-net-framework/mapping-clr-parameter-data.md).

