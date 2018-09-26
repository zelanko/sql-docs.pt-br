---
title: Pontuação nativa no aprendizado de máquina do SQL Server | Microsoft Docs
description: Gere previsões usando a função PREVER T-SQL, pontuação dta entradas em relação a um modelo previamente treinado escritos em R ou Python no SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 08/15/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 372c81310fea86094543319f21e409142810de97
ms.sourcegitcommit: b7fd118a70a5da9bff25719a3d520ce993ea9def
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/24/2018
ms.locfileid: "46713148"
---
# <a name="native-scoring-using-the-predict-t-sql-function"></a>Pontuação nativa usando a função PREVER T-SQL
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

Nativo de pontuação usos [função T-SQL PREVER](https://docs.microsoft.com/sql/t-sql/queries/predict-transact-sql) e os recursos de extensão C++ nativos no SQL Server 2017 para gerar valores de previsão ou *pontuações* para novas entradas de dados em tempo quase real. Essa metodologia oferece a velocidade de processamento possíveis mais rápida de cargas de trabalho de previsão e previsão, mas é fornecido com os requisitos de plataforma e a biblioteca: somente funções de RevoScaleR e revoscalepy têm implementações de C++.

Pontuação nativa requer que você tenha um modelo já treinado. No SQL Server 2017 Windows ou Linux ou no banco de dados SQL, você pode chamar a função PREDICT no Transact-SQL para invocar nativo em relação aos novos dados que você fornece como um parâmetro de entrada de pontuação. A função PREDICT retorna as pontuações sobre entradas de dados que você fornecer.

## <a name="how-native-scoring-works"></a>Funciona como nativa de pontuação

Nativo pontuação usa bibliotecas nativas C++ da Microsoft que pode ler um modelo já treinado, anteriormente armazenados em um formato binário especial ou salvos em disco como um fluxo de bytes brutos e gerar pontuações para novas entradas de dados que você fornecer. Porque o modelo é treinado, publicados e armazenados, ele pode ser usado para pontuação sem a necessidade de chamar o interpretador de R ou Python. Como tal, a sobrecarga de várias interações de processo é reduzida, resultando em desempenho de previsão muito mais rápido em cenários de produção corporativo.

Para usar a pontuação nativa, chame a função PREVER T-SQL e passar as entradas necessárias a seguir:

+ Um modelo compatível com base em um algoritmo com suporte.
+ Dados de entrada, geralmente definidos como uma consulta SQL.

A função retorna previsões para os dados de entrada, junto com qualquer coluna de dados de origem que você deseja passar.

## <a name="prerequisites"></a>Prerequisites

PREVER está disponível em todas as edições do mecanismo de banco de dados do SQL Server 2017 e habilitado por padrão, incluindo os serviços do SQL Server 2017 Machine Learning no Windows, SQL Server 2017 (Windows), SQL Server 2017 (Linux) ou banco de dados SQL. Você não precisa instalar o R, Python, ou habilitar recursos adicionais.

+ O modelo deve ser treinado com antecedência usando um com suporte **rx** algoritmos listados abaixo.

+ Serialize o modelo usando [rxSerialize](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxserializemodel) para R, e [rx_serialize_model](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-serialize-model) para Python. Essas funções de serialização foram otimizadas para dar suporte a pontuação rápida.

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

Se você precisar usar modelos do MicrosoftML ou microsoftml, use [pontuação em tempo real com sp_rxPredict](real-time-scoring.md).

Tipos de modelo sem suporte incluem os seguintes tipos:

+ Modelos que contêm outras transformações
+ Os modelos usando o `rxGlm` ou `rxNaiveBayes` algoritmos em equivalentes de RevoScaleR ou revoscalepy
+ Modelos PMML
+ Modelos criados usando outras bibliotecas de terceiros ou de código-fonte aberto

## <a name="example-predict-t-sql"></a>Exemplo: PREVER (T-SQL)

Neste exemplo, você deve cria um modelo e, em seguida, chame a função de previsão em tempo real do T-SQL.

### <a name="step-1-prepare-and-save-the-model"></a>Etapa 1. Preparar e salvar o modelo

Execute o seguinte código para criar o banco de dados de exemplo e as tabelas necessárias.

```SQL
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

Use a seguinte instrução para popular a tabela de dados com os dados do **iris** conjunto de dados.

```SQL
INSERT INTO iris_rx_data ("Sepal.Length", "Sepal.Width", "Petal.Length", "Petal.Width" , "Species")
EXECUTE sp_execute_external_script
  @language = N'R'
  , @script = N'iris_data <- iris;'
  , @input_data_1 = N''
  , @output_data_1_name = N'iris_data';
GO
```

Agora, crie uma tabela para armazenar modelos.

```SQL
DROP TABLE IF EXISTS ml_models;
GO
CREATE TABLE ml_models ( model_name nvarchar(100) not null primary key
  , model_version nvarchar(100) not null
  , native_model_object varbinary(max) not null);
GO
```

O código a seguir cria um modelo baseado na **íris** conjunto de dados e salva-à tabela denominada **modelos**.

```SQL
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
> Certifique-se de usar o [rxSerializeModel](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxserializemodel) função do RevoScaleR para salvar o modelo. O padrão do R `serialize` função não é possível gerar o formato necessário.

Você pode executar uma instrução a seguir para exibir o modelo armazenado em formato binário:

```SQL
SELECT *, datalength(native_model_object)/1024. as model_size_kb
FROM ml_models;
```

### <a name="step-2-run-predict-on-the-model"></a>Etapa 2. Executar previsão no modelo

A seguinte instrução de previsão simple obtém uma classificação do modelo de árvore de decisão usando o **pontuação nativa** função. Ele prevê a espécie de íris com base em atributos que você fornecer, comprimento da pétala e largura.

```SQL
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

Se você receber o erro, "Erro durante a execução da função PREDICT. Modelo está corrompido ou inválido", isso normalmente significa que sua consulta não retornou um modelo. Verifique se você digitou o nome do modelo corretamente ou se a tabela de modelos está vazia.

> [!NOTE]
> Como as colunas e valores retornados por **PREDICT** pode variar por tipo de modelo, você deve definir o esquema dos dados retornados usando uma **WITH** cláusula.

## <a name="next-steps"></a>Próximas etapas

Para uma solução completa que inclui a pontuação nativa, consulte estes exemplos da equipe de desenvolvimento do SQL Server:

+ Implantar o seu script de ML: [usando um modelo de Python](https://microsoft.github.io/sql-ml-tutorials/python/rentalprediction/step/3.html)
+ Implantar o seu script de ML: [usando um modelo do R](https://microsoft.github.io/sql-ml-tutorials/R/rentalprediction/step/3.html)