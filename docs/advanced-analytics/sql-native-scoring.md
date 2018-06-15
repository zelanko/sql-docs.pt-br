---
title: Pontuação nativo | Microsoft Docs
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: e08cb48335f956298c387e2a621a8e8de7a91a98
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
ms.locfileid: "31202738"
---
# <a name="native-scoring"></a>Nativo de pontuação
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Este tópico descreve os recursos do SQL Server 2017 que fornecem a pontuação em modelos de aprendizado de máquina em tempo quase real.

+ O que é nativo pontuação versus em tempo real de pontuação
+ Como ele funciona
+ Requisitos e plataformas com suporte

## <a name="what-is-native-scoring-and-how-is-it-different-from-realtime-scoring"></a>Qual é a pontuação nativo e como ele é diferente de pontuação em tempo real?

No SQL Server 2016, a Microsoft criou uma estrutura de extensibilidade que permite que os scripts de R a partir do T-SQL. Essa estrutura oferece suporte a qualquer operação que você pode executar em R, variando de funções simples para modelos de aprendizado de máquina complexa de treinamento. No entanto, a arquitetura dual-processo requer invocar um processo externo do R para todas as chamadas, independentemente da complexidade da operação. Se você estiver carregando um modelo previamente treinado de uma tabela e pontuação em relação a ela em dados já existentes no SQL Server, a sobrecarga de chamar o processo de R externo representa um custo de desempenho desnecessários.

_Pontuação_ é um processo de duas etapas. Primeiro, você pode especificar um modelo previamente treinado para carregar de uma tabela. Em segundo lugar, passagem de novos dados de entrada para a função, para gerar valores de previsão (ou _pontuações_). A entrada pode ser linhas de tabela ou único. Você pode optar por um valor de coluna única que representa a probabilidade de saída, ou pode gerar vários valores, como um intervalo de confiança, erro ou outro complemento útil para a previsão.

Quando a entrada inclui muitas linhas de dados, é normalmente mais rápido inserir os valores de previsão em uma tabela como parte do processo de classificação.  Gerar uma pontuação único é mais comum em um cenário onde você obter valores de entrada de uma solicitação de usuário ou do formulário e retorna a pontuação a um aplicativo cliente. Para melhorar o desempenho ao gerar pontuações sucessivas, SQL Server pode armazenar em cache o modelo para que ele possa ser recarregado na memória.

Para dar suporte a pontuação rápido, serviços de aprendizado de máquina do SQL Server (e Microsoft Server de aprendizado de máquina) fornecem bibliotecas internas de pontuação que funcionam em R ou no T-SQL. Há diferentes opções dependendo de qual versão você tem.

**Pontuação nativa**

+ A função de previsão no Transact-SQL dá suporte a _pontuação nativo_ em qualquer instância do SQL Server 2017. Requer apenas que você tenha um modelo já está treinado, que pode ser chamado usando o T-SQL. Pontuação nativo usando o T-SQL tem estas vantagens:

    + Nenhuma configuração adicional é necessária.
    + O tempo de execução de R não é chamado. Não é necessário para instalar o R.

**Em tempo real de pontuação**

+ **sp_rxPredict** é um procedimento armazenado para em tempo real de pontuação que pode ser usado para gerar pontuações de qualquer tipo de modelo com suporte, sem chamar o tempo de execução de R.

  Esse procedimento armazenado também está disponível no SQL Server 2016, se você atualizar os componentes de R usando o instalador autônomo do Microsoft R Server. Também há suporte para sp_rxPredict 2017 do SQL Server. Portanto, você pode usar essa função quando a geração de pontuações com um tipo de modelo não é suportado pela função de previsão.

+ A função rxPredict pode ser usada para pontuação rápida no código de R.

Para todos esses métodos de pontuação, você deve usar um modelo que foi treinado usando um dos algoritmos de RevoScaleR ou MicrosoftML com suporte.

Para obter um exemplo em tempo real de pontuação em ação, consulte [final final empréstimo ChargeOff previsão criados usando o Azure HDInsight Spark Clusters e o serviço do SQL Server 2016 R](https://blogs.msdn.microsoft.com/rserver/2017/06/29/end-to-end-loan-chargeoff-prediction-built-using-azure-hdinsight-spark-clusters-and-sql-server-2016-r-service/)

## <a name="how-native-scoring-works"></a>Funciona como nativa de pontuação

Pontuação nativo usa bibliotecas nativas C++ da Microsoft que podem ler o modelo de um formato binário especial e gerar pontuações. Como um modelo pode ser publicado e usado para pontuação sem a necessidade de chamar o interpretador de R, a sobrecarga de várias interações do processo é reduzida. Portanto, pontuação nativo oferece suporte a desempenho muito mais rápido de previsão em cenários de produção da empresa.

Para gerar pontuações usando essa biblioteca, chame a função de pontuação e passar as seguintes entradas necessárias:

+ Um modelo compatível. Consulte o [requisitos](#Requirements) seção para obter detalhes.
+ Dados de entrada, costumam ser definidos como uma consulta SQL

A função retorna previsões para os dados de entrada, junto com as colunas de dados de origem que você deseja passar.

Para obter exemplos de código, juntamente com instruções sobre como preparar os modelos no formato binário exigido, consulte este artigo:

+ [Como realizar em tempo real de pontuação](r/how-to-do-realtime-scoring.md)

Para uma solução completa que inclui uma pontuação nativo, consulte estes exemplos da equipe de desenvolvimento do SQL Server:

+ Implantar seu script ML: [usando um modelo de Python](https://microsoft.github.io/sql-ml-tutorials/python/rentalprediction/step/3.html)
+ Implantar seu script ML: [usando um modelo de R](https://microsoft.github.io/sql-ml-tutorials/R/rentalprediction/step/3.html)

## <a name="requirements"></a>Requisitos

Plataformas com suporte são os seguintes:

+ Serviços de aprendizado de máquina do SQL Server de 2017 (inclui o Microsoft R Server 9.1.0)
    
    Pontuação nativo usando PREVER requer 2017 do SQL Server.
    Ele funciona em qualquer versão do SQL Server de 2017, inclusive Linux.

    Você também pode realizar em tempo real de pontuação usando sp_rxPredict. Para usar este procedimento armazenado requer que você habilite [integração CLR do SQL Server](https://docs.microsoft.com/dotnet/framework/data/adonet/sql/introduction-to-sql-server-clr-integration).

+ SQL Server 2016

   Em tempo real usando sp_rxPredict de pontuação é possível com o SQL Server 2016 e também pode ser executado no Microsoft R Server. Essa opção requer SQLCLR esteja habilitado e que você instale a atualização do Microsoft R Server.
   Para obter mais informações, consulte [em tempo real de pontuação](Real-time-scoring.md)

### <a name="model-preparation"></a>Preparação de modelo

+ O modelo deve ser treinado com antecedência usando um com suporte **rx** algoritmos. Para obter detalhes, consulte [suporte para algoritmos](#bkmk_native_supported_algos).
+ O modelo deve ser salvo usando a nova função de serialização fornecida no Microsoft R Server 9.1.0. A função de serialização é otimizada para oferecer suporte a pontuação rápida.

### <a name="bkmk_native_supported_algos"></a> Algoritmos que oferecem suporte nativo de pontuação

+ Modelos de RevoScaleR

  + [rxLinMod](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxlinmod)
  + [rxLogit](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxlogit)
  + [rxBTrees](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxbtrees)
  + [rxDtree](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxdtree)
  + [rxDForest](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxdforest)

Se você precisar usar modelos de MicrosoftML, use em tempo real com sp_rxPredict de pontuação.

### <a name="restrictions"></a>Restrições

Não há suporte para os seguintes tipos de modelo:

+ Modelos que contém outros tipos de transformações de R sem suporte
+ Modelos usando o `rxGlm` ou `rxNaiveBayes` algoritmos em RevoScaleR
+ Modelos PMML
+ Modelos criados usando outras bibliotecas de R de CRAN ou outros repositórios
+ Modelos que contêm qualquer outra transformação de R
