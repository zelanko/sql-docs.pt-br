---
title: Pontuação em tempo real no aprendizado de máquina do SQL Server | Microsoft Docs
description: Gere previsões usando sp_rxPredict, pontuação de entradas de dados em relação a um modelo previamente treinado escritos em R no SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 08/15/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 576526801188bc9459ec9e26470e5d17dd775f74
ms.sourcegitcommit: 2a47e66cd6a05789827266f1efa5fea7ab2a84e0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/31/2018
ms.locfileid: "43348296"
---
# <a name="real-time-scoring-with-sprxpredict-in-sql-server-machine-learning"></a>Pontuação com sp_rxPredict no aprendizado de máquina do SQL Server em tempo real
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Pontuação em tempo real usa os recursos de extensão do CLR no SQL Server para previsões de alto desempenho ou pontuações em cargas de trabalho de previsão. Como a pontuação em tempo real é independente de linguagem, ele executa com nenhuma dependência no R ou Python executado vezes. Supondo que um modelo criado a partir de funções da Microsoft, treinados e serializado em formato binário no SQL Server, você pode usar a pontuação em tempo real para gerar resultados previstos em novas entradas de dados em instâncias do SQL Server que não têm os recursos do complemento R ou Python instalado.

## <a name="how-real-time-scoring-works"></a>Como pontuação em tempo real funciona

Pontuação em tempo real tem suporte no SQL Server 2017 e o SQL Server 2016, nos tipos de modelo específico com base em funções RevoScaleR ou MicrosoftML, como [rxLinMod (RevoScaleR)](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxlinmod) ou [rxNeuralNet (MicrosoftML)](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxneuralnet). Ele usa bibliotecas de C++ nativas para gerar pontuações, com base na entrada do usuário fornecida para um modelo armazenado em um formato binário especial de aprendizado de máquina.

Como um modelo treinado pode ser usado para pontuação sem precisar chamar um tempo de execução de linguagem externo, a sobrecarga de vários processos é reduzida. Isso dá suporte a muito mais rápido desempenho de previsão para cenários de pontuação de produção. Porque os dados nunca saiam do SQL Server, os resultados podem ser gerados e inseridos em uma nova tabela sem nenhuma conversão de dados entre R e SQL.

Pontuação em tempo real é um processo de várias etapa:

1. O procedimento armazenado que faz a pontuação deve ser habilitado em uma base por banco de dados.
2. Você carrega o modelo previamente treinado no formato binário.
3. Você pode fornecer novos dados de entrada, linhas de tabela ou únicas, como entrada para o modelo.
4. Para gerar pontuações, chame o sp_rxPredict procedimento armazenado.

> [!TIP]
> Para obter um exemplo de pontuação em tempo real em ação, consulte [End final empréstimo como Incobrável previsão criados usando Clusters do Azure HDInsight Spark e o serviço de R do SQL Server 2016](https://blogs.msdn.microsoft.com/rserver/2017/06/29/end-to-end-loan-chargeoff-prediction-built-using-azure-hdinsight-spark-clusters-and-sql-server-2016-r-service/)

## <a name="prerequisites"></a>Prerequisites

+ [Habilitar integração CLR do SQL Server](https://docs.microsoft.com/dotnet/framework/data/adonet/sql/introduction-to-sql-server-clr-integration).

+ [Habilitar a pontuação em tempo real](#bkmk_enableRtScoring).

+ O modelo deve ser treinado com antecedência usando um com suporte **rx** algoritmos. Para R, pontuação com em tempo real `sp_rxPredict` funciona com [RevoScaleR e MicrosoftML suporte para algoritmos](#bkmk_rt_supported_algos). Para Python, consulte [revoscalepy e microsoftml suporte para algoritmos](#bkmk_py_supported_algos)

+ Serialize o modelo usando [rxSerialize](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxserializemodel) para R, e [rx_serialize_model](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-serialize-model) para Python. Essas funções de serialização foram otimizadas para dar suporte a pontuação rápida.

> [!Note]
> Pontuação em tempo real no momento é otimizado para previsões rápidas em conjuntos de dados menores, variando de algumas linhas a centenas de milhares de linhas. Em grandes conjuntos de dados, usando [rxPredict](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxpredict) pode ser mais rápida.

<a name="bkmk_py_supported_algos"></a>

## <a name="supported-algorithms"></a>Algoritmos compatíveis

### <a name="python-algorithms-using-real-time-scoring"></a>Algoritmos de Python usando a pontuação em tempo real

+ modelos de revoscalepy

  + [rx_lin_mod](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-lin-mod) \*
  + [rx_logit](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-logit) \*
  + [rx_btrees](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-btrees) \*
  + [rx_dtree](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-dtree) \*
  + [rx_dforest](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-dforest) \*
  
  Modelos são marcados com \* também dão suporte a pontuação nativa com a função PREDICT.

+ modelos de microsoftml

  + [rx_fast_trees](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-fast-trees)
  + [rx_fast_forest](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-fast-forest)
  + [rx_logistic_regression](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-logistic-regression)
  + [rx_oneclass_svm](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-oneclass-svm)
  + [rx_neural_net](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-neural-network)
  + [rx_fast_linear](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-fast-linear)

+ Transformações fornecidas pelo microsoftml

  + [featurize_text](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/featurize-text)
  + [concat](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/concat)
  + [categorical](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/categorical)
  + [categorical_hash](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/categorical-hash)


<a name="bkmk_rt_supported_algos"></a>

### <a name="r-algorithms-using-real-time-scoring"></a>Algoritmos de R usando a pontuação em tempo real

+ Modelos de RevoScaleR

  + [rxLinMod](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxlinmod) \*
  + [rxLogit](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxlogit) \*
  + [rxBTrees](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxbtrees) \*
  + [rxDtree](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxdtree) \*
  + [rxdForest](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxdforest) \*
  
  Modelos são marcados com \* também dão suporte a pontuação nativa com a função PREDICT.

+ Modelos de MicrosoftML

  + [rxFastTrees](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxfasttrees)
  + [rxFastForest](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxfastforest)
  + [rxLogisticRegression](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxlogisticregression)
  + [rxOneClassSvm](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxoneclasssvm)
  + [rxNeuralNet](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxneuralnet)
  + [rxFastLinear](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxfastlinear)

+ Transformações fornecidas pelo MicrosoftML

  + [featurizeText](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxfasttrees)
  + [concat](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/concat)
  + [categorical](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/categorical)
  + [categoricalHash](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/categoricalHash)
  + [selectFeatures](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/selectFeatures)

### <a name="unsupported-model-types"></a>Tipos de modelo sem suporte

Pontuação em tempo real não usa um interpretador; Portanto, qualquer funcionalidade que pode exigir um interpretador não é suportada durante a etapa de pontuação.  Elas podem incluir:

  + Os modelos usando o `rxGlm` ou `rxNaiveBayes` algoritmos não têm suporte.

  + Usando uma função de transformação ou fórmula que contém uma transformação, como os modelos <code>A ~ log(B)</code> não têm suporte no sistema de pontuação em tempo real. Para usar um modelo desse tipo, é recomendável que você realize a transformação de dados de entrada antes de passar os dados para a pontuação em tempo real.


## <a name="example-sprxpredict"></a>Exemplo: sp_rxPredict

Esta seção descreve as etapas necessárias para configurar **em tempo real** previsão e fornece um exemplo em R de como chamar a função de T-SQL.

<a name ="bkmk_enableRtScoring"></a> 

### <a name="step-1-enable-the-real-time-scoring-procedure"></a>Etapa 1. Habilitar o procedimento de pontuação em tempo real

Você deve habilitar esse recurso para cada banco de dados que você deseja usar para pontuação. O administrador do servidor deve executar o utilitário de linha de comando, RegisterRExt.exe, que está incluído no pacote RevoScaleR.

> [!NOTE]
> Para a pontuação em tempo real para funcionar, funcionalidade de SQL CLR precisa ser habilitado na instância; Além disso, o banco de dados precisa ser marcado como confiável. Quando você executar o script, essas ações são executadas para você. No entanto, considere as implicações de segurança adicionais antes de fazer isso!

1. Abra um prompt de comando com privilégios elevados e navegue até a pasta onde se encontra RegisterRExt.exe. O caminho a seguir pode ser usado em uma instalação padrão:
    
    `<SQLInstancePath>\R_SERVICES\library\RevoScaleR\rxLibs\x64\`

2. Execute o seguinte comando, substituindo o nome da sua instância e o banco de dados de destino no qual você deseja habilitar os procedimentos armazenados estendidos:

    `RegisterRExt.exe /installRts [/instance:name] /database:databasename`

    Por exemplo, para adicionar o procedimento armazenado estendido para o banco de dados CLRPredict na instância padrão, digite:

    `RegisterRExt.exe /installRts /database:CLRPRedict`

    O nome da instância é opcional se o banco de dados na instância padrão. Se você estiver usando uma instância nomeada, você deve especificar o nome da instância.

3. RegisterRExt.exe cria os seguintes objetos:

    + Assemblies confiáveis
    + O procedimento armazenado `sp_rxPredict`
    + Uma nova função de banco de dados, `rxpredict_users`. O administrador de banco de dados pode usar essa função para conceder permissão aos usuários que usam a funcionalidade de pontuação em tempo real.

4. Adicionar quaisquer usuários que precisam executar `sp_rxPredict` à nova função.

> [!NOTE]
> 
> No SQL Server 2017, as medidas de segurança adicionais estão em vigor para evitar problemas com a integração CLR. Essas medidas impõem restrições adicionais sobre o uso desse procedimento armazenado também. 

### <a name="step-2-prepare-and-save-the-model"></a>Etapa 2. Preparar e salvar o modelo

O formato binário exigido pelo sp\_rxPredict é o mesmo que o formato necessário para usar a função PREDICT. Portanto, no seu código R, incluir uma chamada para [rxSerializeModel](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxserializemodel)e não se esqueça de especificar `realtimeScoringOnly = TRUE`, como neste exemplo:

```R
model <- rxSerializeModel(model.name, realtimeScoringOnly = TRUE)
```

### <a name="step-3-call-sprxpredict"></a>Etapa 3. Chamar sp_rxPredict

Você pode chamar sp\_rxPredict como você faria com qualquer outro procedimento armazenado. Na versão atual, o procedimento armazenado usa apenas dois parâmetros:  _\@modelo_ para o modelo em formato binário, e  _\@inputData_ para os dados a serem usados na pontuação, definido como uma consulta SQL válida.

Como o formato binário é o mesmo que é usado pela função de previsão, você pode usar a tabela de dados e modelos do exemplo anterior.

```SQL
DECLARE @irismodel varbinary(max)
SELECT @irismodel = [native_model_object] from [ml_models]
WHERE model_name = 'iris.dtree' 
AND model_version = 'v1''

EXEC sp_rxPredict
@model = @irismodel,
@inputData = N'SELECT * FROM iris_rx_data'
```

> [!NOTE]
> 
> A chamada para sp\_rxPredict falhará se os dados de entrada para pontuação não incluem colunas que correspondem aos requisitos do modelo. Atualmente, somente os seguintes tipos de dados de .NET têm suporte: double, float, short, ushort, long, ulong e cadeia de caracteres.
> 
> Portanto, você talvez precise filtrar os tipos sem suporte em seus dados de entrada antes de usá-lo para pontuação em tempo real.
> 
> Para obter informações sobre tipos SQL correspondentes, consulte [mapeamento de tipo de SQL-CLR](/dotnet/framework/data/adonet/sql/linq/sql-clr-type-mapping) ou [Mapeando dados de parâmetro CLR](https://docs.microsoft.com/sql/relational-databases/clr-integration-database-objects-types-net-framework/mapping-clr-parameter-data).

## <a name="disable-real-time-scoring"></a>Desabilitar a pontuação em tempo real

Para desabilitar a funcionalidade de pontuação em tempo real, abra um prompt de comando com privilégios elevados e execute o seguinte comando: `RegisterRExt.exe /uninstallrts /database:<database_name> [/instance:name]`

## <a name="next-steps"></a>Próximas etapas

Para obter um exemplo de como rxPredict pode ser usado para pontuação, consulte [final final empréstimo como Incobrável previsão criados usando Clusters do Azure HDInsight Spark e o serviço do SQL Server 2016 R](https://blogs.msdn.microsoft.com/rserver/2017/06/29/end-to-end-loan-chargeoff-prediction-built-using-azure-hdinsight-spark-clusters-and-sql-server-2016-r-service/).

Para obter mais informações sobre a pontuação no SQL Server, consulte [como gerar previsões no aprendizado de máquina do SQL Server](r/how-to-do-realtime-scoring.md).
