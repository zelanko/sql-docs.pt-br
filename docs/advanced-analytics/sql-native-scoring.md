---
title: Pontuação nativa usando T-SQL PREDICT
description: Gere previsões usando a função T-SQL PREDICT, pontuando as entradas DTA em um modelo pré-treinado escrito em R ou Python no SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 08/15/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 766adecbc91f88ed0796e4214b7e4074fc564f01
ms.sourcegitcommit: 09ccd103bcad7312ef7c2471d50efd85615b59e8
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/07/2019
ms.locfileid: "73727289"
---
# <a name="native-scoring-using-the-predict-t-sql-function"></a>Pontuação nativa usando a função T-SQL PREDICT
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

A pontuação nativa usa a [função T-SQL PREDICT](https://docs.microsoft.com/sql/t-sql/queries/predict-transact-sql) e as funcionalidades de extensão do C++ nativo no SQL Server 2017 para gerar valores de previsão ou *pontuações* para novas entradas de dados em tempo quase real. Essa metodologia oferece a velocidade de processamento mais rápida possível das cargas de trabalho de previsão, mas vem com requisitos de plataforma e biblioteca: somente as funções do RevoScaleR e do revoscalepy têm implementações C++.

A pontuação nativa exige que você tenha um modelo já treinado. No SQL Server 2017 Windows ou Linux ou no Banco de Dados SQL do Azure, você pode chamar a função PREDICT no Transact-SQL para invocar a pontuação nativa em novos dados fornecidos como um parâmetro de entrada. A função PREDICT retorna as pontuações para entradas de dados fornecidas.

## <a name="how-native-scoring-works"></a>Como funciona a pontuação nativa

A pontuação nativa usa bibliotecas C++ nativas da Microsoft que podem ler um modelo já treinado (anteriormente armazenado em um formato binário especial ou salvo em disco como um fluxo de bytes brutos) e gerar pontuações para novas entradas de dados fornecidas. Como o modelo é treinado, publicado e armazenado, ele pode ser usado para pontuação sem precisar chamar o interpretador do R ou do Python. Assim, a sobrecarga de várias interações de processos é reduzida, resultando em um desempenho de previsão muito mais rápido em cenários de produção empresarial.

Para usar a pontuação nativa, chame a função T-SQL PREDICT e passe as seguintes entradas necessárias:

+ Um modelo compatível baseado em um algoritmo com suporte.
+ Dados de entrada, normalmente definidos como uma consulta SQL.

A função retorna previsões para os dados de entrada, junto com as colunas de dados de origem que você deseja passar.

## <a name="prerequisites"></a>Prerequisites

A função PREDICT está disponível em todas as edições do mecanismo de banco de dados do SQL Server 2017 e habilitada por padrão, incluindo os Serviços de Machine Learning do SQL Server no Windows, o SQL Server 2017 (Windows), o SQL Server 2017 (Linux) ou o Banco de Dados SQL do Azure. Você não precisa instalar o R, o Python nem habilitar recursos adicionais.

+ O modelo precisa ser treinado com antecedência usando um dos algoritmos do **rx** compatíveis listados abaixo.

+ Serialize o modelo usando [rxSerialize](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxserializemodel) para o R e [rx_serialize_model](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-serialize-model) para o Python. Essas funções de serialização foram otimizadas para dar suporte à pontuação rápida.

<a name="bkmk_native_supported_algos"></a> 

## <a name="supported-algorithms"></a>Algoritmos compatíveis

+ Modelos do revoscalepy

  + [rx_lin_mod](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-lin-mod)
  + [rx_logit](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-logit) 
  + [rx_btrees](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-btrees) 
  + [rx_dtree](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-dtree) 
  + [rx_dforest](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-dforest) 

+ Modelos do RevoScaleR

  + [rxLinMod](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxlinmod)
  + [rxLogit](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxlogit)
  + [rxBTrees](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxbtrees)
  + [rxDtree](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxdtree)
  + [rxDForest](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxdforest)

Caso você precise usar modelos do MicrosoftML ou do microsoftml, use a [pontuação em tempo real com sp_rxPredict](real-time-scoring.md).

Os tipos de modelos sem suporte incluem os seguintes tipos:

+ Modelos que contêm outras transformações
+ Modelos que usam os algoritmos `rxGlm` ou `rxNaiveBayes` em equivalentes do RevoScaleR ou do revoscalepy
+ Modelos do PMML
+ Modelos criados com outras bibliotecas de software livre ou de terceiros

## <a name="example-predict-t-sql"></a>Exemplo: PREDICT (T-SQL)

Neste exemplo, você criará um modelo e, em seguida, chamará a função de previsão em tempo real no T-SQL.

### <a name="step-1-prepare-and-save-the-model"></a>Etapa 1. Preparar e salvar o modelo

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

### <a name="step-2-run-predict-on-the-model"></a>Etapa 2. Executar PREDICT no modelo

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

## <a name="next-steps"></a>Próximas etapas

Para obter uma solução completa que inclui a pontuação nativa, confira estas amostras da equipe de desenvolvimento do SQL Server:

+ Implante seu script ML: [Como usar um modelo do Python](https://microsoft.github.io/sql-ml-tutorials/python/rentalprediction/step/3.html)
+ Implante seu script ML: [Como usar um modelo do R](https://microsoft.github.io/sql-ml-tutorials/R/rentalprediction/step/3.html)