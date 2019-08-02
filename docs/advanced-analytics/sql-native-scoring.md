---
title: Pontuação nativa usando a instrução T-SQL de previsão
description: Gere previsões usando a função prever T-SQL, classificando as entradas DTA em um modelo pré-treinado escrito em R ou Python em SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 08/15/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: f84b799fa901f7461f448683cceffe78e1dddfd3
ms.sourcegitcommit: 321497065ecd7ecde9bff378464db8da426e9e14
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/01/2019
ms.locfileid: "68714956"
---
# <a name="native-scoring-using-the-predict-t-sql-function"></a>Pontuação nativa usando a função T-SQL de previsão
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

A pontuação nativa usa a [função de previsão T-SQL](https://docs.microsoft.com/sql/t-sql/queries/predict-transact-sql) e os recursos de extensão nativa C++ no SQL Server 2017 para gerar valores de previsão ou *pontuações* para novas entradas de dados em tempo quase real. Essa metodologia oferece a velocidade de processamento mais rápida possível das cargas de trabalho de previsão e previsão, mas vem com requisitos de plataforma e biblioteca: somente as funções de RevoScaleR C++ e revoscalepy têm implementações.

A pontuação nativa requer que você tenha um modelo já treinado. No SQL Server 2017 Windows ou Linux, ou no banco de dados SQL do Azure, você pode chamar a função PREDICT no Transact-SQL para invocar a pontuação nativa em novos dados que você fornecer como um parâmetro de entrada. A função PREDICT retorna pontuações sobre as entradas de dados que você fornece.

## <a name="how-native-scoring-works"></a>Como a pontuação nativa funciona

A pontuação nativa usa C++ bibliotecas nativas da Microsoft que podem ler um modelo já treinado, anteriormente armazenado em um formato binário especial ou salvo em disco como fluxo de bytes brutos, e gerar pontuações para novas entradas de dados que você fornecer. Como o modelo é treinado, publicado e armazenado, ele pode ser usado para Pontuação sem precisar chamar o intérprete R ou Python. Assim, a sobrecarga de várias interações de processo é reduzida, resultando em um desempenho de previsão muito mais rápido em cenários de produção corporativa.

Para usar a pontuação nativa, chame a função T-SQL de previsão e passe as seguintes entradas necessárias:

+ Um modelo compatível baseado em um algoritmo com suporte.
+ Dados de entrada, normalmente definidos como uma consulta SQL.

A função retorna previsões para os dados de entrada, junto com todas as colunas de dados de origem que você deseja passar.

## <a name="prerequisites"></a>Pré-requisitos

A previsão está disponível em todas as edições do mecanismo de banco de dados do SQL Server 2017 e habilitada por padrão, incluindo SQL Server Serviços de Machine Learning no Windows, SQL Server 2017 (Windows), SQL Server 2017 (Linux) ou banco de dados SQL do Azure. Você não precisa instalar o R, Python ou habilitar recursos adicionais.

+ O modelo deve ser treinado com antecedência usando um dos algoritmos de **RX** com suporte listados abaixo.

+ Serialize o modelo usando [rxSerialize](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxserializemodel) para R e [rx_serialize_model](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-serialize-model) para Python. Essas funções de serialização foram otimizadas para dar suporte à pontuação rápida.

<a name="bkmk_native_supported_algos"></a> 

## <a name="supported-algorithms"></a>Algoritmos compatíveis

+ modelos de revoscalepy

  + [rx_lin_mod](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-lin-mod)
  + [rx_logit](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-logit) 
  + [rx_btrees](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-btrees) 
  + [rx_dtree](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-dtree) 
  + [rx_dforest](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-dforest) 

+ Modelos de RevoScaleR

  + [rxLinMod](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxlinmod)
  + [rxLogit](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxlogit)
  + [rxBTrees](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxbtrees)
  + [rxDtree](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxdtree)
  + [rxDForest](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxdforest)

Se você precisar usar modelos de MicrosoftML ou MicrosoftML, use a [Pontuação em tempo real com sp_rxPredict](real-time-scoring.md).

Os tipos de modelo sem suporte incluem os seguintes tipos:

+ Modelos que contêm outras transformações
+ Modelos que usam `rxGlm` os `rxNaiveBayes` algoritmos ou em equivalentes RevoScaleR ou revoscalepy
+ Modelos de PMML
+ Modelos criados usando outras bibliotecas de código-fonte aberto ou de terceiros

## <a name="example-predict-t-sql"></a>Exemplo: PREVISÃO (T-SQL)

Neste exemplo, você cria um modelo e, em seguida, chama a função de previsão em tempo real do T-SQL.

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

Use a instrução a seguir para popular a tabela de dados com os dados do DataSet **íris** .

```sql
INSERT INTO iris_rx_data ("Sepal.Length", "Sepal.Width", "Petal.Length", "Petal.Width" , "Species")
EXECUTE sp_execute_external_script
  @language = N'R'
  , @script = N'iris_data <- iris;'
  , @input_data_1 = N''
  , @output_data_1_name = N'iris_data';
GO
```

Agora, crie uma tabela para armazenar modelos.

```sql
DROP TABLE IF EXISTS ml_models;
GO
CREATE TABLE ml_models ( model_name nvarchar(100) not null primary key
  , model_version nvarchar(100) not null
  , native_model_object varbinary(max) not null);
GO
```

O código a seguir cria um modelo baseado no conjunto de uma **íris** e o salva na tabela denominada **modelos**.

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
> Certifique-se de usar a função [rxSerializeModel](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxserializemodel) de RevoScaleR para salvar o modelo. A função R `serialize` padrão não pode gerar o formato necessário.

Você pode executar uma instrução como a seguinte para exibir o modelo armazenado em formato binário:

```sql
SELECT *, datalength(native_model_object)/1024. as model_size_kb
FROM ml_models;
```

### <a name="step-2-run-predict-on-the-model"></a>Etapa 2. Executar previsão no modelo

A instrução de previsão simples a seguir obtém uma classificação do modelo de árvore de decisão usando a função de **Pontuação nativa** . Ele prevê as espécies de íris com base nos atributos fornecidos, comprimento e largura da pétala.

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

Se você receber o erro "ocorreu um erro durante a execução da previsão de função. O modelo está corrompido ou inválido ", geralmente significa que a consulta não retornou um modelo. Verifique se você digitou o nome do modelo corretamente ou se a tabela de modelos está vazia.

> [!NOTE]
> Como as colunas e os valores retornados por **previsão** podem variar por tipo de modelo, você deve definir o esquema dos dados retornados usando uma cláusula **with** .

## <a name="next-steps"></a>Próximas etapas

Para obter uma solução completa que inclui pontuação nativa, consulte estes exemplos da equipe de desenvolvimento do SQL Server:

+ Implante seu script ML: [Usando um modelo Python](https://microsoft.github.io/sql-ml-tutorials/python/rentalprediction/step/3.html)
+ Implante seu script ML: [Usando um modelo de R](https://microsoft.github.io/sql-ml-tutorials/R/rentalprediction/step/3.html)