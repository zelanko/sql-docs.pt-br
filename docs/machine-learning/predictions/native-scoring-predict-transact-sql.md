---
title: Pontuação nativa com T-SQL PREDICT
titleSuffix: SQL machine learning
description: Saiba como usar a pontuação nativa com a função PREDICT T-SQL a fim de gerar valores de previsão para novas entradas de dados quase em tempo real.
ms.prod: sql
ms.technology: machine-learning
ms.date: 07/29/2020
ms.topic: how-to
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2017||=azuresqldb-current||>=sql-server-linux-2017||=azuresqldb-mi-current||=azure-sqldw-latest||=sqlallproducts-allversions'
ms.openlocfilehash: 762d272661fd9bfaa61781391e42d3d9919d78c1
ms.sourcegitcommit: 039fb38c583019b3fd06894160568387a19ba04e
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/30/2020
ms.locfileid: "87442907"
---
# <a name="native-scoring-using-the-predict-t-sql-function-with-sql-machine-learning"></a>Pontuação nativa usando a função T-SQL PREDICT com o machine learning do SQL

[!INCLUDE [sqlserver2017-asdb-asdbmi-asa](../../includes/applies-to-version/sqlserver2017-asdb-asdbmi-asa.md)]

Saiba como usar a pontuação nativa com a [função PREDICT T-SQL](../../t-sql/queries/predict-transact-sql.md) a fim de gerar valores de previsão para novas entradas de dados quase em tempo real. A pontuação nativa exige que você tenha um modelo já treinado.

A função `PREDICT` usa as funcionalidades de extensão nativas do C++ no [machine learning do SQL](../index.yml). Essa metodologia oferece a velocidade de processamento mais rápida possível de cargas de trabalho de previsão e modelos de suporte no formato [ONNX (Open Neural Network Exchange)](https://onnx.ai/get-started.html) ou modelos treinados por meio dos pacotes [RevoScaleR](../r/ref-r-revoscaler.md) e [revoscalepy](../python/ref-py-revoscalepy.md).

## <a name="how-native-scoring-works"></a>Como funciona a pontuação nativa

A pontuação nativa usa bibliotecas que podem ler modelos no ONNX ou em um formato binário predefinido e gerar pontuações para novas entradas de dados fornecidas. Como o modelo é treinado, implantado e armazenado, ele pode ser usado para pontuação sem precisar chamar o interpretador do R ou do Python. Isso significa que a sobrecarga de várias interações de processo é reduzida, resultando em um desempenho de previsão mais rápido.

Para usar a pontuação nativa, chame a função `PREDICT` T-SQL e transmita as seguintes entradas necessárias:

+ Um modelo compatível baseado em um modelo e um algoritmo compatíveis.
+ Dados de entrada, normalmente definidos como uma consulta T-SQL.

A função retorna previsões para os dados de entrada, junto com as colunas de dados de origem que você deseja passar.

## <a name="prerequisites"></a>Pré-requisitos

A função `PREDICT` está disponível em:

+ Todas as edições do SQL Server 2017 e posterior no Windows e no Linux
+ Instância Gerenciada do Azure SQL
+ Banco de Dados SQL do Azure
+ SQL do Azure no Edge
+ Azure Synapse Analytics

Por padrão, a função está habilitada. Você não precisa instalar o R nem o Python, muito menos habilitar recursos adicionais.

## <a name="supported-models"></a>Modelos com suporte

Os formatos de modelo compatíveis com a função `PREDICT` dependem da plataforma SQL na qual a pontuação nativa é executada. Confira a tabela abaixo para ver quais formatos de modelo são compatíveis com qual plataforma.

| Plataforma | Formato de modelo ONNX | Formato de modelo RevoScale |
|-|-|-|
| SQL Server | Não | Sim |
| Instância Gerenciada do Azure SQL | Sim | Sim |
| Banco de Dados SQL do Azure | Não | Sim |
| SQL do Azure no Edge | Sim | Não |
| Azure Synapse Analytics | Sim | Não |

::: moniker range="=azuresqldb-mi-current||=azure-sqldw-latest||=sqlallproducts-allversions"
### <a name="onnx-models"></a>Modelos ONNX

O modelo precisa estar em um formato de modelo [ONNX (Open Neural Network Exchange)](https://onnx.ai/get-started.html).
::: moniker-end

::: moniker range=">=sql-server-2017||>=sql-server-linux-2017||=azuresqldb-mi-current||=azuresqldb-current||=sqlallproducts-allversions"
### <a name="revoscale-models"></a>Modelos do RevoScale

O modelo precisa ser treinado com antecedência usando um dos algoritmos **rx** compatíveis listados abaixo por meio do pacote [RevoScaleR](../r/ref-r-revoscaler.md) ou [revoscalepy](../python/ref-py-revoscalepy.md).

Serialize o modelo usando [rxSerialize](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxserializemodel) para o R e [rx_serialize_model](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-serialize-model) para o Python. Essas funções de serialização foram otimizadas para dar suporte à pontuação rápida.

<a name="bkmk_native_supported_algos"></a> 

#### <a name="supported-revoscale-algorithms"></a>Algoritmos compatíveis do RevoScale

Os algoritmos a seguir são compatíveis com o revoscalepy e o RevoScaleR.

+ Algoritmos do revoscalepy

  + [rx_lin_mod](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-lin-mod)
  + [rx_logit](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-logit) 
  + [rx_btrees](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-btrees) 
  + [rx_dtree](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-dtree) 
  + [rx_dforest](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-dforest) 

+ Algoritmos do RevoScaleR

  + [rxLinMod](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxlinmod)
  + [rxLogit](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxlogit)
  + [rxBTrees](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxbtrees)
  + [rxDtree](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxdtree)
  + [rxDForest](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxdforest)

Caso você precise usar um algoritmo do MicrosoftML ou do microsoftml, use a [pontuação em tempo real com sp_rxPredict](../predictions/real-time-scoring.md).

Os tipos de modelos sem suporte incluem os seguintes tipos:

+ Modelos que contêm outras transformações
+ Modelos que usam os algoritmos `rxGlm` ou `rxNaiveBayes` em equivalentes do RevoScaleR ou do revoscalepy
+ Modelos do PMML
+ Modelos criados com outras bibliotecas de software livre ou de terceiros
::: moniker-end

## <a name="examples"></a>Exemplos
::: moniker range="=azuresqldb-mi-current||=azure-sqldw-latest||=sqlallproducts-allversions"
### <a name="predict-with-an-onnx-model"></a>PREDICT com um modelo ONNX

Este exemplo mostra como usar um modelo ONNX armazenado na tabela `dbo.models` para pontuação nativa.

```sql
DECLARE @model VARBINARY(max) = (
        SELECT DATA
        FROM dbo.models
        WHERE id = 1
        );

WITH predict_input
AS (
    SELECT TOP (1000) [id]
        , CRIM
        , ZN
        , INDUS
        , CHAS
        , NOX
        , RM
        , AGE
        , DIS
        , RAD
        , TAX
        , PTRATIO
        , B
        , LSTAT
    FROM [dbo].[features]
    )
SELECT predict_input.id
    , p.variable1 AS MEDV
FROM PREDICT(MODEL = @model, DATA = predict_input, RUNTIME=ONNX) WITH (variable1 FLOAT) AS p;
```

> [!NOTE]
> Como as colunas e os valores retornados por **PREDICT** podem variar de acordo com o tipo de modelo, é necessário definir o esquema dos dados retornados usando uma cláusula **WITH**.
::: moniker-end

::: moniker range=">=sql-server-2017||=azuresqldb-mi-current||>=sql-server-linux-2017||=sqlallproducts-allversions"
### <a name="predict-with-revoscale-model"></a>PREDICT com o modelo RevoScale

Neste exemplo, você criará um modelo usando o **RevoScaleR** no R e chamará a função de previsão em tempo real no T-SQL.

#### <a name="step-1-prepare-and-save-the-model"></a>Etapa 1. Preparar e salvar o modelo

Execute o código a seguir para criar o banco de dados de exemplo e as tabelas necessárias.

```sql
CREATE DATABASE NativeScoringTest;
GO
USE NativeScoringTest;
GO
DROP TABLE IF EXISTS iris_rx_data;
GO
CREATE TABLE iris_rx_data (
    "Sepal.Length" float not null, "Sepal.Width" float not null
  , "Petal.Length" float not null, "Petal.Width" float not null
  , "Species" varchar(100) null
);
GO
```

Use a instrução a seguir para popular a tabela de dados com os dados do conjunto de dados **iris**.

```sql
INSERT INTO iris_rx_data ("Sepal.Length", "Sepal.Width", "Petal.Length", "Petal.Width" , "Species")
EXECUTE sp_execute_external_script
  @language = N'R'
  , @script = N'iris_data <- iris;'
  , @input_data_1 = N''
  , @output_data_1_name = N'iris_data';
GO
```

Agora, crie uma tabela para armazenar os modelos.

```sql
DROP TABLE IF EXISTS ml_models;
GO
CREATE TABLE ml_models ( model_name nvarchar(100) not null primary key
  , model_version nvarchar(100) not null
  , native_model_object varbinary(max) not null);
GO
```

O código a seguir cria um modelo baseado no conjunto de dados **iris** e o salva na tabela chamada **models**.

```sql
DECLARE @model varbinary(max);
EXECUTE sp_execute_external_script
  @language = N'R'
  , @script = N'
    iris.sub <- c(sample(1:50, 25), sample(51:100, 25), sample(101:150, 25))
    iris.dtree <- rxDTree(Species ~ Sepal.Length + Sepal.Width + Petal.Length + Petal.Width, data = iris[iris.sub, ])
    model <- rxSerializeModel(iris.dtree, realtimeScoringOnly = TRUE)
    '
  , @params = N'@model varbinary(max) OUTPUT'
  , @model = @model OUTPUT
  INSERT [dbo].[ml_models]([model_name], [model_version], [native_model_object])
  VALUES('iris.dtree','v1', @model) ;
```

> [!NOTE]
> Lembre-se de usar a função [rxSerializeModel](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxserializemodel) do RevoScaleR para salvar o modelo. A função `serialize` padrão do R não pode gerar o formato necessário.

Execute uma instrução como a seguinte para exibir o modelo armazenado em formato binário:

```sql
SELECT *, datalength(native_model_object)/1024. as model_size_kb
FROM ml_models;
```

#### <a name="step-2-run-predict-on-the-model"></a>Etapa 2. Executar PREDICT no modelo

A instrução PREDICT simples a seguir obtém uma classificação do modelo de árvore de decisão usando a função de **pontuação nativa**. Ele prevê as espécies de íris com base nos atributos fornecidos, tamanho e largura da pétala.

```sql
DECLARE @model varbinary(max) = (
  SELECT native_model_object
  FROM ml_models
  WHERE model_name = 'iris.dtree'
  AND model_version = 'v1');
SELECT d.*, p.*
  FROM PREDICT(MODEL = @model, DATA = dbo.iris_rx_data as d)
  WITH(setosa_Pred float, versicolor_Pred float, virginica_Pred float) as p;
go
```

Se você receber o erro "Erro durante a execução da função PREDICT. O modelo está corrompido ou é inválido", isso geralmente indicará que a consulta não retornou um modelo. Verifique se você digitou o nome do modelo corretamente ou se a tabela de modelos está vazia.

> [!NOTE]
> Como as colunas e os valores retornados por **PREDICT** podem variar de acordo com o tipo de modelo, é necessário definir o esquema dos dados retornados usando uma cláusula **WITH**.
::: moniker-end

## <a name="next-steps"></a>Próximas etapas

+ [Função PREDICT T-SQL](../../t-sql/queries/predict-transact-sql.md)
+ [Documentação do machine learning do SQL](../index.yml)
+ [Machine learning e IA com o ONNX no SQL no Edge](/azure/azure-sql-edge/onnx-overview)
+ [Implantar e fazer previsões com um modelo ONNX no SQL do Azure no Edge](/azure/azure-sql-edge/deploy-onnx)
