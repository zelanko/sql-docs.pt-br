---
title: sp_rxPredict | Microsoft Docs
ms.date: 03/31/2020
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: machine-learning-services
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
monikerRange: '>=sql-server-2016'
ms.openlocfilehash: 55514f89487a06e16413f199f744013d2c4f8c90
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97461497"
---
# <a name="sp_rxpredict"></a>sp_rxPredict  
[!INCLUDE [SQL Server 2016 Windows only](../../includes/applies-to-version/sqlserver2016-windows-only.md)]

Gera um valor previsto para uma determinada entrada que consiste em um modelo de aprendizado de máquina armazenado em um formato binário em um banco de dados SQL Server.

Fornece Pontuação em modelos de aprendizado de máquina R e Python quase em tempo real. `sp_rxPredict` é um procedimento armazenado fornecido como um wrapper para a `rxPredict` função R em [RevoScaleR](/r-server/r-reference/revoscaler/revoscaler) e [MicrosoftML](/r-server/r-reference/microsoftml/microsoftml-package), e a função [rx_predict](/machine-learning-server/python-reference/revoscalepy/rx-predict) Python em [revoscalepy](/machine-learning-server/python-reference/revoscalepy/revoscalepy-package) e [MicrosoftML](/machine-learning-server/python-reference/microsoftml/microsoftml-package). Ele é escrito em C++ e é otimizado especificamente para operações de pontuação.

Embora o modelo deva ser criado usando R ou Python, depois que ele é serializado e armazenado em um formato binário em uma instância do mecanismo de banco de dados de destino, ele pode ser consumido nessa instância do mecanismo de banco de dados, mesmo quando a integração do R ou do Python não está instalada. Para obter mais informações, consulte [Pontuação em tempo real com sp_rxPredict](../../machine-learning/predictions/real-time-scoring.md).

## <a name="syntax"></a>Sintaxe

```
sp_rxPredict  ( @model, @input )
```

### <a name="arguments"></a>Argumentos

**modelo**

Um modelo pretreinado em um formato com suporte. 

**input**

Uma consulta SQL válida

### <a name="return-values"></a>Valores retornados

Uma coluna de pontuação é retornada, bem como quaisquer colunas de passagem da fonte de dados de entrada.
Colunas de Pontuação adicionais, como o intervalo de confiança, podem ser retornadas se o algoritmo der suporte à geração desses valores.

## <a name="remarks"></a>Comentários

Para habilitar o uso do procedimento armazenado, o SQLCLR deve estar habilitado na instância.

> [!NOTE]
> Há implicações de segurança para enabing essa opção. Use uma implementação alternativa, como a função de [previsão Transact-SQL](../../t-sql/queries/predict-transact-sql.md?view=sql-server-2017) , se o SQLCLR não puder ser habilitado no servidor.

O usuário precisa de `EXECUTE` permissão no banco de dados.

### <a name="supported-algorithms"></a>Algoritmos compatíveis

Para criar e treinar o modelo, use um dos algoritmos com suporte para R ou Python, fornecido por [SQL Server serviços de Machine Learning (r ou Python)](../../machine-learning/sql-server-machine-learning-services.md), [SQL Server 2016 r Services](../../machine-learning/r/sql-server-r-services.md), [SQL Server Machine Learning Server (autônomo) (r ou Python)](../../machine-learning/r/r-server-standalone.md)ou [SQL Server 2016 r Server (autônomo)](../../machine-learning/r/r-server-standalone.md?view=sql-server-2016).

#### <a name="r-revoscaler-models"></a>R: modelos de RevoScaleR

  + [rxLinMod](/machine-learning-server/r-reference/revoscaler/rxlinmod)
  + [rxLogit](/machine-learning-server/r-reference/revoscaler/rxlogit)
  + [rxBTrees](/machine-learning-server/r-reference/revoscaler/rxbtrees)
  + [rxDtree](/machine-learning-server/r-reference/revoscaler/rxdtree)
  + [rxdForest](/machine-learning-server/r-reference/revoscaler/rxdforest)

#### <a name="r-microsoftml-models"></a>R: modelos de MicrosoftML

  + [rxFastTrees](/machine-learning-server/r-reference/microsoftml/rxfasttrees)
  + [rxFastForest](/machine-learning-server/r-reference/microsoftml/rxfastforest)
  + [rxLogisticRegression](/machine-learning-server/r-reference/microsoftml/rxlogisticregression)
  + [rxOneClassSvm](/machine-learning-server/r-reference/microsoftml/rxoneclasssvm)
  + [rxNeuralNet](/machine-learning-server/r-reference/microsoftml/rxneuralnet)
  + [rxFastLinear](/machine-learning-server/r-reference/microsoftml/rxfastlinear)

#### <a name="r-transformations-supplied-by-microsoftml"></a>R: transformações fornecidas por MicrosoftML

  + [featurizeText](/machine-learning-server/r-reference/microsoftml/rxfasttrees)
  + [concat](/machine-learning-server/r-reference/microsoftml/concat)
  + [categorical](/machine-learning-server/r-reference/microsoftml/categorical)
  + [categoricalHash](/machine-learning-server/r-reference/microsoftml/categoricalHash)
  + [selectFeatures](/machine-learning-server/r-reference/microsoftml/selectFeatures)

#### <a name="python-revoscalepy-models"></a>Python: modelos de revoscalepy

  + [rx_lin_mod](/machine-learning-server/python-reference/revoscalepy/rx-lin-mod)
  + [rx_logit](/machine-learning-server/python-reference/revoscalepy/rx-logit)
  + [rx_btrees](/machine-learning-server/python-reference/revoscalepy/rx-btrees)
  + [rx_dtree](/machine-learning-server/python-reference/revoscalepy/rx-dtree)
  + [rx_dforest](/machine-learning-server/python-reference/revoscalepy/rx-dforest)


#### <a name="python-microsoftml-models"></a>Python: modelos de microsoftml

  + [rx_fast_trees](/machine-learning-server/python-reference/microsoftml/rx-fast-trees)
  + [rx_fast_forest](/machine-learning-server/python-reference/microsoftml/rx-fast-forest)
  + [rx_logistic_regression](/machine-learning-server/python-reference/microsoftml/rx-logistic-regression)
  + [rx_oneclass_svm](/machine-learning-server/python-reference/microsoftml/rx-oneclass-svm)
  + [rx_neural_network](/machine-learning-server/python-reference/microsoftml/rx-neural-network)
  + [rx_fast_linear](/machine-learning-server/python-reference/microsoftml/rx-fast-linear)

#### <a name="python-transformations-supplied-by-microsoftml"></a>Python: transformações fornecidas por microsoftml

  + [featurize_text](/machine-learning-server/python-reference/microsoftml/rx-fast-trees)
  + [concat](/machine-learning-server/python-reference/microsoftml/concat)
  + [categorical](/machine-learning-server/python-reference/microsoftml/categorical)
  + [categorical_hash](/machine-learning-server/python-reference/microsoftml/categorical-hash)
  
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

Além de ser uma consulta SQL válida, os dados de entrada em *\@ inputData* devem incluir colunas compatíveis com as colunas no modelo armazenado.

`sp_rxPredict` dá suporte apenas aos seguintes tipos de coluna .NET: Double, float, short, ushort, Long, ULong e String. Talvez seja necessário filtrar tipos sem suporte em seus dados de entrada antes de usá-los para pontuação em tempo real. 

  Para obter informações sobre os tipos SQL correspondentes, confira [Mapeamento de tipos SQL-CLR](/dotnet/framework/data/adonet/sql/linq/sql-clr-type-mapping) ou [Mapeamento de dados de parâmetro CLR](../clr-integration-database-objects-types-net-framework/mapping-clr-parameter-data.md).