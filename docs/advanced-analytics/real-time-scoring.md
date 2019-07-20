---
title: Pontuação em tempo real usando o procedimento armazenado sp_rxPredict
description: Gere previsões usando sp_rxPredict, pontuação de entradas de dados em um modelo pré-treinado escrito em R em SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 03/29/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.openlocfilehash: 2e9c9353acdc0a2641203788c8e4883a9accb021
ms.sourcegitcommit: c1382268152585aa77688162d2286798fd8a06bb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/19/2019
ms.locfileid: "68345683"
---
# <a name="real-time-scoring-with-sprxpredict-in-sql-server-machine-learning"></a>Pontuação em tempo real com sp_rxPredict no aprendizado de máquina SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

A pontuação em tempo real usa o procedimento armazenado do sistema [sp_rxPredict](https://docs.microsoft.com//sql/relational-databases/system-stored-procedures/sp-rxpredict-transact-sql) e os recursos de extensão do CLR em SQL Server para previsões ou pontuações de alto desempenho em cargas de trabalho de previsão. A pontuação em tempo real é independente de linguagem e é executada sem nenhuma dependência em tempos de execução de R ou Python. Supondo que um modelo seja criado e treinado usando o Microsoft Functions e, em seguida, serializado em um formato binário no SQL Server, você pode usar a pontuação em tempo real para gerar resultados previstos sobre novas entradas de dados em instâncias de SQL Server que não têm o complemento R ou Python recém-instalado.

## <a name="how-real-time-scoring-works"></a>Como a pontuação em tempo real funciona

A pontuação em tempo real tem suporte no SQL Server 2017 e SQL Server 2016, em tipos de modelo específicos com base em funções RevoScaleR ou MicrosoftML como [rxLinMod (RevoScaleR)](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxlinmod)[rxNeuralNet (MicrosoftML)](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxneuralnet). Ele usa bibliotecas C++ nativas para gerar pontuações, com base na entrada do usuário fornecida a um modelo de aprendizado de máquina armazenado em um formato binário especial.

Como um modelo treinado pode ser usado para Pontuação sem a necessidade de chamar um tempo de execução de linguagem externo, a sobrecarga de vários processos é reduzida. Isso dá suporte a um desempenho de previsão muito mais rápido para cenários de Pontuação de produção. Como os dados nunca saem SQL Server, os resultados podem ser gerados e inseridos em uma nova tabela sem nenhuma conversão de dados entre R e SQL.

A pontuação em tempo real é um processo de várias etapas:

1. O procedimento armazenado que faz a pontuação deve ser habilitado em uma base por banco de dados.
2. Você carrega o modelo pré-treinado em formato binário.
3. Você fornece novos dados de entrada a serem pontuados, tabulares ou linhas únicas, como entrada para o modelo.
4. Para gerar pontuações, chame o procedimento armazenado [sp_rxPredict](https://docs.microsoft.com//sql/relational-databases/system-stored-procedures/sp-rxpredict-transact-sql) .

## <a name="prerequisites"></a>Pré-requisitos

+ [Habilite a integração do SQL Server CLR](https://docs.microsoft.com/dotnet/framework/data/adonet/sql/introduction-to-sql-server-clr-integration).

+ [Habilitar Pontuação em tempo real](#bkmk_enableRtScoring).

+ O modelo deve ser treinado com antecedência usando um dos algoritmos de **RX** com suporte. Para R, a pontuação em tempo real `sp_rxPredict` com o funciona com os algoritmos com [suporte RevoScaleR e MicrosoftML](#bkmk_rt_supported_algos). Para Python, consulte [algoritmos com suporte do revoscalepy e microsoftml](#bkmk_py_supported_algos)

+ Serialize o modelo usando [rxSerialize](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxserializemodel) para R e [rx_serialize_model](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-serialize-model) para Python. Essas funções de serialização foram otimizadas para dar suporte à pontuação rápida.

+ Salve o modelo na instância do mecanismo de banco de dados da qual você deseja chamá-lo. Não é necessário que essa instância tenha a extensão de tempo de execução R ou Python.

> [!Note]
> A pontuação em tempo real atualmente é otimizada para previsões rápidas em conjuntos de dados menores, variando de algumas linhas a centenas de milhares de linhas. Em conjuntos de grandes DataSets, o uso de [rxPredict](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxpredict) pode ser mais rápido.

<a name="bkmk_py_supported_algos"></a>

## <a name="supported-algorithms"></a>Algoritmos compatíveis

### <a name="python-algorithms-using-real-time-scoring"></a>Algoritmos do Python usando pontuação em tempo real

+ modelos de revoscalepy

  + [rx_lin_mod](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-lin-mod) \*
  + [rx_logit](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-logit) \*
  + [rx_btrees](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-btrees)\*
  + [rx_dtree](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-dtree) \*
  + [rx_dforest](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-dforest) \*
  
  Os modelos marcados \* com o também dão suporte à pontuação nativa com a função Predict.

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

### <a name="r-algorithms-using-real-time-scoring"></a>Algoritmos de R usando pontuação em tempo real

+ Modelos de RevoScaleR

  + [rxLinMod](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxlinmod) \*
  + [rxLogit](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxlogit) \*
  + [rxBTrees](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxbtrees) \*
  + [rxDtree](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxdtree) \*
  + [rxdForest](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxdforest) \*
  
  Os modelos marcados \* com o também dão suporte à pontuação nativa com a função Predict.

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

A pontuação em tempo real não usa um intérprete; Portanto, qualquer funcionalidade que possa exigir um intérprete não tem suporte durante a etapa de pontuação.  Eles podem incluir:

  + Não há suporte `rxGlm` para `rxNaiveBayes` modelos que usam os algoritmos ou.

  + Modelos que usam uma função de transformação ou fórmula contendo uma transformação, <code>A ~ log(B)</code> como não têm suporte em pontuação em tempo real. Para usar um modelo desse tipo, recomendamos que você execute a transformação nos dados de entrada antes de passar os dados para a pontuação em tempo real.


## <a name="example-sprxpredict"></a>Exemplo: sp_rxPredict

Esta seção descreve as etapas necessárias para configurar a previsão em **tempo real** e fornece um exemplo em R de como chamar a função do T-SQL.

<a name ="bkmk_enableRtScoring"></a> 

### <a name="step-1-enable-the-real-time-scoring-procedure"></a>Etapa 1. Habilitar o procedimento de pontuação em tempo real

Você deve habilitar esse recurso para cada banco de dados que deseja usar para pontuação. O administrador do servidor deve executar o utilitário de linha de comando, RegisterRExt. exe, que está incluído no pacote RevoScaleR.

> [!NOTE]
> Para que a pontuação em tempo real funcione, a funcionalidade SQL CLR precisa ser habilitada na instância; Além disso, o banco de dados precisa ser marcado como confiável. Quando você executa o script, essas ações são executadas para você. No entanto, considere as implicações de segurança adicionais antes de fazer isso!

1. Abra um prompt de comando com privilégios elevados e navegue até a pasta onde o RegisterRExt. exe está localizado. O caminho a seguir pode ser usado em uma instalação padrão:
    
    `<SQLInstancePath>\R_SERVICES\library\RevoScaleR\rxLibs\x64\`

2. Execute o comando a seguir, substituindo o nome da sua instância e o banco de dados de destino onde você deseja habilitar os procedimentos armazenados estendidos:

    `RegisterRExt.exe /installRts [/instance:name] /database:databasename`

    Por exemplo, para adicionar o procedimento armazenado estendido ao banco de dados CLRPredict na instância padrão, digite:

    `RegisterRExt.exe /installRts /database:CLRPRedict`

    O nome da instância será opcional se o banco de dados estiver na instância padrão. Se você estiver usando uma instância nomeada, deverá especificar o nome da instância.

3. O RegisterRExt. exe cria os seguintes objetos:

    + Assemblies confiáveis
    + O procedimento armazenado`sp_rxPredict`
    + Uma nova função de banco `rxpredict_users`de dados,. O administrador de banco de dados pode usar essa função para conceder permissão a usuários que usam a funcionalidade de pontuação em tempo real.

4. Adicione qualquer usuário que precise executar `sp_rxPredict` a nova função.

> [!NOTE]
> 
> No SQL Server 2017, as medidas de segurança adicionais estão em vigor para evitar problemas com a integração CLR. Essas medidas impõem restrições adicionais ao uso desse procedimento armazenado também. 

### <a name="step-2-prepare-and-save-the-model"></a>Etapa 2. Preparar e salvar o modelo

O formato binário exigido pelo SP\_rxPredict é o mesmo que o formato necessário para usar a função Predict. Portanto, no código do R, inclua uma chamada para [rxSerializeModel](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxserializemodel)e certifique-se de especificar `realtimeScoringOnly = TRUE`, como neste exemplo:

```R
model <- rxSerializeModel(model.name, realtimeScoringOnly = TRUE)
```

### <a name="step-3-call-sprxpredict"></a>Etapa 3. Chamar sp_rxPredict

Você chama o\_SP rxPredict como faria com qualquer outro procedimento armazenado. Na versão atual, o procedimento armazenado usa apenas dois parâmetros:  _\@modelo_ para o modelo em formato binário e  _\@inputData_ para os dados a serem usados na pontuação, definidos como uma consulta SQL válida.

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
> 
> A chamada para SP\_rxPredict falhará se os dados de entrada para pontuação não incluírem colunas que correspondam aos requisitos do modelo. Atualmente, há suporte apenas para os seguintes tipos de dados .NET: duplo, float, short, ushort, Long, ULong e String.
> 
> Portanto, talvez seja necessário filtrar os tipos sem suporte nos dados de entrada antes de usá-los para pontuação em tempo real.
> 
> Para obter informações sobre os tipos SQL correspondentes, consulte [mapeamento de tipo SQL-CLR](/dotnet/framework/data/adonet/sql/linq/sql-clr-type-mapping) ou [mapeamento de dados de parâmetro CLR](https://docs.microsoft.com/sql/relational-databases/clr-integration-database-objects-types-net-framework/mapping-clr-parameter-data).

## <a name="disable-real-time-scoring"></a>Desabilitar Pontuação em tempo real

Para desabilitar a funcionalidade de pontuação em tempo real, abra um prompt de comando com privilégios elevados e execute o seguinte comando:`RegisterRExt.exe /uninstallrts /database:<database_name> [/instance:name]`

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre Pontuação em SQL Server, consulte [como gerar previsões no Machine Learning de SQL Server](r/how-to-do-realtime-scoring.md).
