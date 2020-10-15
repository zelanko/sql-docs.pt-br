---
title: Pontuação em tempo real usando sp_rxPredict
description: Saiba como executar a pontuação em tempo real com o procedimento armazenado do sistema sp_rxPredict no SQL Server para previsões ou pontuações de alto desempenho em cargas de trabalho de previsão.
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 07/31/2020
ms.topic: how-to
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: e6809a66ce7f5fd425ce9bfeb2b1fea919c4dfaa
ms.sourcegitcommit: afb02c275b7c79fbd90fac4bfcfd92b00a399019
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2020
ms.locfileid: "91956920"
---
# <a name="real-time-scoring-with-sp_rxpredict-in-sql-server"></a>Pontuação em tempo real com sp_rxPredict no SQL Server
[!INCLUDE[sqlserver2016](../../includes/applies-to-version/sqlserver2016.md)]

Saiba como executar a pontuação em tempo real com o procedimento armazenado do sistema [sp_rxPredict](../../relational-databases/system-stored-procedures/sp-rxpredict-transact-sql.md) no SQL Server para previsões ou pontuações de alto desempenho em cargas de trabalho de previsão.

A pontuação em tempo real com `sp_rxPredict` é independente de linguagem e é executada sem nenhuma dependência nos tempos de execução de R ou Python no [Serviços de Machine Learning](../sql-server-machine-learning-services.md) ou [Serviços do R](../r/sql-server-r-services.md). Supondo que um modelo seja criado e treinado usando funções da Microsoft e, em seguida, serializado em um formato binário no SQL Server, você pode usar a pontuação em tempo real para gerar resultados previstos sobre novas entradas de dados em instâncias do SQL Server que não têm o complemento do R ou do Python instalado.

## <a name="how-real-time-scoring-works"></a>Como funciona a pontuação em tempo real

Há suporte para a pontuação em tempo real em tipos de modelo específicos com base em funções no [RevoScaleR](../r/ref-r-revoscaler.md) ou no [MicrosoftML](../r/ref-r-microsoftml.md) no R ou [revoscalepy](../python/ref-py-revoscalepy.md) ou [microsoftml](../python/ref-py-microsoftml.md) no Python. Ela usa bibliotecas C++ nativas para gerar pontuações, com base na entrada do usuário fornecida a um modelo de machine learning armazenado em um formato binário especial.

Como um modelo treinado pode ser usado para pontuação sem a necessidade de chamar um runtime de linguagem externo em [Serviços de Machine Learning](../sql-server-machine-learning-services.md) ou [R Services](../r/sql-server-r-services.md), a sobrecarga de vários processos é reduzida. 

A pontuação em tempo real é um processo de várias etapas:

1. O procedimento armazenado que faz a pontuação precisa ser habilitado em uma base por banco de dados.
2. Você carrega o modelo pré-treinado em formato binário.
3. Você fornece novos dados de entrada a serem pontuados, de tabela ou linhas únicas, como entrada para o modelo.
4. Para gerar pontuações, chame o procedimento armazenado [sp_rxPredict](../../relational-databases/system-stored-procedures/sp-rxpredict-transact-sql.md).

## <a name="prerequisites"></a>Pré-requisitos

+ [Habilitar a integração CLR do SQL Server](../../relational-databases/clr-integration/clr-integration-enabling.md).

+ [Habilitar a pontuação em tempo real](#bkmk_enableRtScoring).

+ O modelo precisa ser treinado com antecedência usando um dos algoritmos do **rx** compatíveis. Para o R, a pontuação em tempo real com `sp_rxPredict` funciona com os [algoritmos compatíveis com o RevoScaleR e o MicrosoftML](#bkmk_rt_supported_algos). Para o Python, confira [Algoritmos compatíveis com o revoscalepy e o microsoftml](#bkmk_py_supported_algos).

+ Serialize o modelo usando [rxSerialize](/machine-learning-server/r-reference/revoscaler/rxserializemodel) para o R e [rx_serialize_model](/machine-learning-server/python-reference/revoscalepy/rx-serialize-model) para o Python. Essas funções de serialização foram otimizadas para dar suporte à pontuação rápida.

+ Salve o modelo na instância do mecanismo de banco de dados da qual você deseja chamá-lo. Não é necessário que essa instância tenha a extensão de runtime do R ou do Python.

> [!Note]
> Atualmente, a pontuação em tempo real é otimizada para previsões rápidas em conjuntos de dados menores, variando de algumas linhas a centenas de milhares de linhas. Em conjuntos de dados grandes, o uso de [rxPredict](/machine-learning-server/r-reference/revoscaler/rxpredict) pode ser mais rápido.

<a name ="bkmk_enableRtScoring"></a> 

## <a name="enable-real-time-scoring"></a>Habilitar a pontuação em tempo real

Você precisa habilitar esse recurso para cada banco de dados que deseja usar para pontuação. O administrador do servidor deve executar o utilitário de linha de comando, RegisterRExt.exe, que está incluído no pacote do RevoScaleR.

> [!NOTE]
> Para que a pontuação em tempo real funcione, a funcionalidade do SQL CLR precisa ser habilitada na instância; além disso, o banco de dados precisa ser marcado como confiável. Quando você executa o script, essas ações são executadas para você. No entanto, considere as implicações de segurança adicionais antes de fazer isso.

1. Abra um prompt de comandos com privilégios elevados e navegue até a pasta na qual RegisterRExt.exe está localizado. O seguinte caminho pode ser usado em uma instalação padrão:

    `<SQLInstancePath>\R_SERVICES\library\RevoScaleR\rxLibs\x64\`

2. Execute o seguinte comando, substituindo o nome da instância e do banco de dados de destino no qual deseja habilitar os procedimentos armazenados estendidos:

    `RegisterRExt.exe /installRts [/instance:name] /database:databasename`

    Por exemplo, para adicionar o procedimento armazenado estendido ao banco de dados CLRPredict na instância padrão, digite:

    `RegisterRExt.exe /installRts /database:CLRPRedict`

    O nome da instância será opcional se o banco de dados estiver na instância padrão. Se você estiver usando uma instância nomeada, precisará especificar o nome da instância.

3. O RegisterRExt.exe cria os seguintes objetos:

    + Assemblies confiáveis
    + O procedimento armazenado `sp_rxPredict`
    + Uma função de banco de dados, `rxpredict_users`. O administrador de banco de dados pode usar essa função para conceder permissão a usuários que usam a funcionalidade de pontuação em tempo real.

4. Adicione os usuários que precisam executar `sp_rxPredict` à nova função.

> [!NOTE]
>
> No SQL Server 2017 e posteriores, medidas de segurança adicionais estão em vigor para evitar problemas com a integração CLR. Essas medidas impõem restrições adicionais no uso desse procedimento armazenado também.

## <a name="disable-real-time-scoring"></a>Desabilitar a pontuação em tempo real

Para desabilitar a funcionalidade de pontuação em tempo real, abra um prompt de comandos com privilégios elevados e execute o seguinte comando: `RegisterRExt.exe /uninstallrts /database:<database_name> [/instance:name]`

<a name="bkmk_py_supported_algos"></a>

## <a name="supported-algorithms"></a>Algoritmos compatíveis

### <a name="python-algorithms-using-real-time-scoring"></a>Algoritmos do Python usando a pontuação em tempo real

+ Modelos do revoscalepy

  + [rx_lin_mod](/machine-learning-server/python-reference/revoscalepy/rx-lin-mod) \*
  + [rx_logit](/machine-learning-server/python-reference/revoscalepy/rx-logit) \*
  + [rx_btrees](/machine-learning-server/python-reference/revoscalepy/rx-btrees) \*
  + [rx_dtree](/machine-learning-server/python-reference/revoscalepy/rx-dtree) \*
  + [rx_dforest](/machine-learning-server/python-reference/revoscalepy/rx-dforest) \*
  
  Os modelos marcados com \* também dão suporte à pontuação nativa com a função PREDICT.

+ Modelos do microsoftml

  + [rx_fast_trees](/machine-learning-server/python-reference/microsoftml/rx-fast-trees)
  + [rx_fast_forest](/machine-learning-server/python-reference/microsoftml/rx-fast-forest)
  + [rx_logistic_regression](/machine-learning-server/python-reference/microsoftml/rx-logistic-regression)
  + [rx_oneclass_svm](/machine-learning-server/python-reference/microsoftml/rx-oneclass-svm)
  + [rx_neural_net](/machine-learning-server/python-reference/microsoftml/rx-neural-network)
  + [rx_fast_linear](/machine-learning-server/python-reference/microsoftml/rx-fast-linear)

+ Transformações fornecidas pelo microsoftml

  + [featurize_text](/machine-learning-server/python-reference/microsoftml/featurize-text)
  + [concat](/machine-learning-server/python-reference/microsoftml/concat)
  + [categorical](/machine-learning-server/python-reference/microsoftml/categorical)
  + [categorical_hash](/machine-learning-server/python-reference/microsoftml/categorical-hash)

<a name="bkmk_rt_supported_algos"></a>

### <a name="r-algorithms-using-real-time-scoring"></a>Algoritmos do R usando a pontuação em tempo real

+ Modelos do RevoScaleR

  + [rxLinMod](/machine-learning-server/r-reference/revoscaler/rxlinmod) \*
  + [rxLogit](/machine-learning-server/r-reference/revoscaler/rxlogit) \*
  + [rxBTrees](/machine-learning-server/r-reference/revoscaler/rxbtrees) \*
  + [rxDtree](/machine-learning-server/r-reference/revoscaler/rxdtree) \*
  + [rxdForest](/machine-learning-server/r-reference/revoscaler/rxdforest) \*
  
  Os modelos marcados com \* também dão suporte à pontuação nativa com a função PREDICT.

+ Modelos do MicrosoftML

  + [rxFastTrees](/machine-learning-server/r-reference/microsoftml/rxfasttrees)
  + [rxFastForest](/machine-learning-server/r-reference/microsoftml/rxfastforest)
  + [rxLogisticRegression](/machine-learning-server/r-reference/microsoftml/rxlogisticregression)
  + [rxOneClassSvm](/machine-learning-server/r-reference/microsoftml/rxoneclasssvm)
  + [rxNeuralNet](/machine-learning-server/r-reference/microsoftml/rxneuralnet)
  + [rxFastLinear](/machine-learning-server/r-reference/microsoftml/rxfastlinear)

+ Transformações fornecidas pelo MicrosoftML

  + [featurizeText](/machine-learning-server/r-reference/microsoftml/rxfasttrees)
  + [concat](/machine-learning-server/r-reference/microsoftml/concat)
  + [categorical](/machine-learning-server/r-reference/microsoftml/categorical)
  + [categoricalHash](/machine-learning-server/r-reference/microsoftml/categoricalHash)
  + [selectFeatures](/machine-learning-server/r-reference/microsoftml/selectFeatures)

### <a name="unsupported-model-types"></a>Tipos de modelos sem suporte

A pontuação em tempo real não usa um interpretador; portanto, não há suporte para nenhuma funcionalidade que possa exigir um interpretador durante a etapa de pontuação.  Eles podem incluir:

+ Não há suporte para modelos que usam os algoritmos `rxGlm` ou `rxNaiveBayes`.

+ Não há suporte para modelos que usam uma função de transformação ou uma fórmula contendo uma transformação, como `A ~ log(B`, em pontuação em tempo real. Para usar um modelo desse tipo, recomendamos que você execute a transformação nos dados de entrada antes de passar os dados para a pontuação em tempo real.

## <a name="example"></a>Exemplo

Esta seção descreve as etapas necessárias para preparar e salvar um modelo para previsão em **tempo real** e fornece um exemplo em R de como chamar a função no T-SQL.

### <a name="step-1-prepare-and-save-the-model"></a>Etapa 1. Preparar e salvar o modelo

O formato binário exigido por sp\_rxPredict é o mesmo que o formato necessário para usar a função PREDICT. Portanto, no código R, inclua uma chamada a [rxSerializeModel](/machine-learning-server/r-reference/revoscaler/rxserializemodel) e especifique `realtimeScoringOnly = TRUE`, como neste exemplo:

```R
model <- rxSerializeModel(model.name, realtimeScoringOnly = TRUE)
```

### <a name="step-2-call-sp_rxpredict"></a>Etapa 2. Chamar sp_rxPredict

Você chama `sp_rxPredict` como chamaria qualquer outro procedimento armazenado. Na versão atual, o procedimento armazenado só usa dois parâmetros: _\@model_ para o modelo em formato binário e _\@inputData_ para os dados a serem usados na pontuação, definidos como uma consulta SQL válida.

Como o formato binário é o mesmo usado pela função PREDICT, você pode usar os modelos e a tabela de dados do exemplo anterior.

```sql
DECLARE @irismodel varbinary(max)
SELECT @irismodel = [native_model_object] from [ml_models]
WHERE model_name = 'iris.dtree' 
AND model_version = 'v1''

EXEC sp_rxPredict
@model = @irismodel,
@inputData = N'SELECT * FROM iris_rx_data'
```

> [!NOTE]
> A chamada a `sp_rxPredict` falhará se os dados de entrada para pontuação não incluírem colunas que correspondam aos requisitos do modelo. Atualmente, só há suporte para os seguintes tipos de dados .NET: double, float, short, ushort, long, ulong e string.
>
> Portanto, talvez seja necessário filtrar os tipos sem suporte nos dados de entrada antes de usá-los para a pontuação em tempo real.
>
> Para obter informações sobre os tipos SQL correspondentes, confira [Mapeamento de tipos SQL-CLR](/dotnet/framework/data/adonet/sql/linq/sql-clr-type-mapping) ou [Mapeamento de dados de parâmetro CLR](../../relational-databases/clr-integration-database-objects-types-net-framework/mapping-clr-parameter-data.md).

## <a name="next-steps"></a>Próximas etapas

+ [Pontuação nativa usando a função T-SQL PREDICT com o machine learning do SQL](native-scoring-predict-transact-sql.md)
+ [sp_rxPredict](../../relational-databases/system-stored-procedures/sp-rxpredict-transact-sql.md)
+ [Machine learning do SQL](../index.yml)