---
title: Pontuação em tempo real no aprendizado de máquina do SQL Server | Microsoft Docs
description: Gere previsões usando sp_rxPredict, pontuação dta entradas em relação a um modelo previamente treinado escritos em R no SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 08/15/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: d5a3d0318f925918ef98ae18744e4287d6b81108
ms.sourcegitcommit: 9cd01df88a8ceff9f514c112342950e03892b12c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/20/2018
ms.locfileid: "40395040"
---
# <a name="real-time-scoring-with-sprxpredict-in-sql-server-machine-learning"></a>Pontuação com sp_rxPredict no aprendizado de máquina do SQL Server em tempo real
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Este artigo explica como pontuação funciona quase em tempo real para dados relacionais do SQL Server, usando o machine learning modelos escritos em R. 

> [!Note]
> Pontuação nativa é uma implementação especial de pontuação em tempo real que usa a função nativa de PREVER o T-SQL para pontuação muito rápido. Para obter mais informações e disponibilidade, consulte [pontuação nativa](sql-native-scoring.md).

## <a name="how-real-time-scoring-works"></a>Como pontuação em tempo real funciona

Pontuação em tempo real tem suporte no SQL Server 2017 e o SQL Server 2016, nos tipos de modelo específico com base em funções RevoScaleR ou MicrosoftML, como [rxLinMod (RevoScaleR)](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxlinmod) ou [rxNeuralNet (MicrosoftML)](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxneuralnet). Ele usa bibliotecas de C++ nativas para gerar pontuações, com base na entrada do usuário fornecida para um modelo armazenado em um formato binário especial de aprendizado de máquina.

Como um modelo treinado pode ser usado para pontuação sem precisar chamar um tempo de execução de linguagem externo, a sobrecarga de vários processos é reduzida. Isso dá suporte a muito mais rápido desempenho de previsão para cenários de pontuação de produção. Porque os dados nunca saiam do SQL Server, os resultados podem ser gerados e inseridos em uma nova tabela sem nenhuma conversão de dados entre R e SQL.

Pontuação em tempo real é um processo de várias etapa:

1. O procedimento armazenado que faz a pontuação deve ser habilitado em uma base por banco de dados.
2. Você carrega o modelo previamente treinado no formato binário.
3. Você pode fornecer novos dados de entrada, linhas de tabela ou únicas, como entrada para o modelo.
4. Para gerar pontuações, chame o sp_rxPredict procedimento armazenado.

## <a name="get-started"></a>Introdução

Para exemplos de código e instruções, consulte [como executar pontuação em tempo real ou a pontuação nativa](r/how-to-do-realtime-scoring.md).

Para obter um exemplo de como rxPredict pode ser usado para pontuação, consulte [End final empréstimo como Incobrável previsão criados usando Clusters do Azure HDInsight Spark e o serviço de R do SQL Server 2016](https://blogs.msdn.microsoft.com/rserver/2017/06/29/end-to-end-loan-chargeoff-prediction-built-using-azure-hdinsight-spark-clusters-and-sql-server-2016-r-service/)

> [!TIP]
> Se você estiver trabalhando exclusivamente no código R, você também pode usar o [rxPredict](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxpredict) função de pontuação rápida.

## <a name="requirements"></a>Requisitos

Pontuação em tempo real é compatível com essas plataformas:

+ Serviços de Machine Learning do SQL Server 2017
+ SQL Server R Services 2016, com a atualização dos componentes do R para 9.1.0 ou posterior

No SQL Server, você deve habilitar o recurso de pontuação em tempo real com antecedência adicionar as bibliotecas com base em CLR para o SQL Server.

Para obter informações sobre a pontuação em tempo real em um ambiente distribuído com base no Microsoft R Server, consulte o [publishService](https://docs.microsoft.com/machine-learning-server/r-reference/mrsdeploy/publishservice) função disponível na [pacote mrsDeploy](https://docs.microsoft.com/machine-learning-server/r-reference/mrsdeploy/mrsdeploy-package), que dá suporte a Publicando modelos de pontuação em tempo real como um novo um serviço web em execução no servidor de R.

### <a name="restrictions"></a>Restrictions

+ O modelo deve ser treinado com antecedência usando um com suporte **rx** algoritmos. Para obter detalhes, consulte [suporte para algoritmos](#bkmk_rt_supported_algos). Pontuação em tempo real com `sp_rxPredict` dá suporte a algoritmos RevoScaleR e MicrosoftML.

+ O modelo deve ser salvo usando as novas funções de serialização: [rxSerialize](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxserializemodel) para R, e [rx_serialize_model](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-serialize-model) para Python. Essas funções de serialização foram otimizadas para dar suporte a pontuação rápida.

+ Pontuação em tempo real não usa um interpretador; Portanto, qualquer funcionalidade que pode exigir um interpretador não é suportada durante a etapa de pontuação.  Elas podem incluir:

  + Os modelos usando o `rxGlm` ou `rxNaiveBayes` algoritmos não têm suporte no momento

  + Modelos de RevoScaleR que usam uma função de transformação de R, ou uma fórmula que contém uma transformação, como <code>A ~ log(B)</code> não têm suporte no sistema de pontuação em tempo real. Para usar um modelo desse tipo, é recomendável que você realize a transformação a para dados de entrada antes de passar os dados para a pontuação em tempo real.

+ Pontuação em tempo real no momento é otimizado para previsões rápidas em conjuntos de dados menores, variando de algumas linhas a centenas de milhares de linhas. Em grandes conjuntos de dados, usando [rxPredict](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxpredict) pode ser mais rápida.

### <a name="a-namebkmkrtsupportedalgosalgorithms-that-support-real-time-scoring"></a><a name="bkmk_rt_supported_algos">Algoritmos que dão suporte a pontuação em tempo real

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

Não há suporte para a pontuação em tempo real para transformações de R diferente dos listados explicitamente na seção anterior. 

Para os desenvolvedores acostumados a trabalhar com o RevoScaleR e outras bibliotecas específicas da Microsoft R, funções sem suporte incluem `rxGlm` ou `rxNaiveBayes` algoritmos do RevoScaleR, modelos PMML e outros modelos criados usando outras bibliotecas de R do CRAN ou outros repositórios.

### <a name="known-issues"></a>Problemas conhecidos

+ `sp_rxPredict` Retorna uma mensagem de imprecisa quando um valor NULL é passado como o modelo: "System.Data.SqlTypes.SqlNullValueException:Data em Null".

## <a name="next-steps"></a>Próximas etapas

[Como fazer a pontuação em tempo real](r/how-to-do-realtime-scoring.md)
