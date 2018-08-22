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
ms.openlocfilehash: bf8f9a6362b72efddccbf5c2b0e54096c6e86aa7
ms.sourcegitcommit: 9cd01df88a8ceff9f514c112342950e03892b12c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/20/2018
ms.locfileid: "40392474"
---
# <a name="native-scoring-using-the-predict-t-sql-function"></a>Pontuação nativa usando a função PREVER T-SQL
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

Quando você tiver um modelo previamente treinado, você pode passar os novos dados de entrada para a função para gerar valores de previsão ou *pontuações*. No SQL Server 2017 Windows ou Linux ou no banco de dados SQL, você pode usar a função PREDICT no Transact-SQL para dar suporte a pontuação nativa. Exige apenas que você tenha um modelo já está treinado, que pode ser chamado usando o T-SQL. 

+ O que é nativo versus pontuação em tempo real de pontuação
+ Como ele funciona
+ Requisitos e plataformas com suporte

## <a name="what-is-native-scoring-and-how-is-it-different-from-real-time-scoring"></a>Qual é a pontuação nativa e como ele é diferente da pontuação em tempo real?

No SQL Server 2016, a Microsoft criou uma estrutura de extensibilidade que permite que os scripts de R ser executado a partir do T-SQL. Essa estrutura oferece suporte a qualquer operação que você pode executar em R, variando de funções simples para modelos de aprendizado de máquina complexos de treinamento. No entanto, a arquitetura dual-processo requer invocar um processo externo do R para cada chamada, independentemente da complexidade da operação. Se você estiver carregando um modelo previamente treinado de uma tabela e de pontuação em relação a ele em dados já existentes no SQL Server, a sobrecarga de chamar o processo de R externo representa um custo de desempenho desnecessária.

_Pontuação_ é um processo em duas etapas. Primeiro, você pode especificar um modelo previamente treinado para carregar a partir de uma tabela. Em segundo lugar, passagem de novos dados de entrada para a função, para gerar valores de previsão (ou _pontuações_). A entrada pode ser linhas tabulares ou únicas. Você pode optar por um valor de coluna única que representa a probabilidade de saída, ou você pode saída vários valores, como um intervalo de confiança, erro ou outro complemento útil para a previsão.

Quando a entrada inclui muitas linhas de dados, é geralmente mais rápido inserir os valores de previsão em uma tabela como parte do processo de classificação.  Gerar uma pontuação única é mais comum em um cenário onde obter os valores de entrada de uma solicitação de forma ou de usuário e retornar a pontuação a um aplicativo cliente. Para melhorar o desempenho ao gerar as pontuações de sucessivas, SQL Server pode armazenar em cache o modelo para que ele pode ser recarregado na memória.

Para dar suporte a pontuação rápida, serviços de Machine Learning do SQL Server (e Microsoft Machine Learning Server) fornecem bibliotecas internas de pontuação que trabalham em R ou no T-SQL. Há diferentes opções dependendo de qual versão você tem.

**Pontuação nativa**

+ A função PREDICT no Transact-SQL dá suporte à _pontuação nativa_ em qualquer instância do SQL Server 2017. Exige apenas que você tenha um modelo já está treinado, que pode ser chamado usando o T-SQL. Pontuação nativa usando o T-SQL tem estas vantagens:

    + Nenhuma configuração adicional é necessária.
    + O tempo de execução de R não é chamado. Não é necessário instalar o R.

**Pontuação em tempo real**

+ **sp_rxPredict** é um procedimento armazenado para pontuação em tempo real que pode ser usado para gera as pontuações de qualquer tipo de modelo com suporte, sem chamar o tempo de execução de R.

  Esse procedimento armazenado também está disponível no SQL Server 2016, se você atualizar os componentes do R usando o instalador autônomo do Microsoft R Server. sp_rxPredict também é suportado no SQL Server 2017. Portanto, você pode usar essa função ao gerar pontuações com um tipo de modelo não tem suportado pela função PREDICT.

+ A função rxPredict pode ser usada para pontuação rápidas dentro do código R.

Para todos esses métodos de pontuação, você deve usar um modelo que foi treinado usando um dos algoritmos RevoScaleR ou MicrosoftML com suporte.

Para obter um exemplo de pontuação em tempo real em ação, consulte [End final empréstimo como Incobrável previsão criados usando Clusters do Azure HDInsight Spark e o serviço de R do SQL Server 2016](https://blogs.msdn.microsoft.com/rserver/2017/06/29/end-to-end-loan-chargeoff-prediction-built-using-azure-hdinsight-spark-clusters-and-sql-server-2016-r-service/)

## <a name="how-native-scoring-works"></a>Funciona como nativa de pontuação

Pontuação nativa usa as bibliotecas nativas de C++ da Microsoft que pode ler o modelo em um formato binário especial e gerar pontuações. Como um modelo pode ser publicado e podem ser usado para pontuação sem a necessidade de chamar o interpretador de R, a sobrecarga de várias interações de processo é reduzida. Portanto, pontuação nativa oferece suporte a desempenho de previsão muito mais rápido em cenários de produção corporativo.

Para gerar pontuações usando essa biblioteca, chame a função de pontuação e passar as entradas necessárias a seguir:

+ Um modelo compatível. Consulte a [requisitos](#Requirements) seção para obter detalhes.
+ Dados de entrada, geralmente definidos como uma consulta SQL

A função retorna previsões para os dados de entrada, junto com qualquer coluna de dados de origem que você deseja passar.

Para obter exemplos de código, juntamente com instruções sobre como preparar os modelos no formato binário necessário, consulte este artigo:

+ [Como executar pontuação em tempo real](r/how-to-do-realtime-scoring.md)

Para uma solução completa que inclui a pontuação nativa, consulte estes exemplos da equipe de desenvolvimento do SQL Server:

+ Implantar o seu script de ML: [usando um modelo de Python](https://microsoft.github.io/sql-ml-tutorials/python/rentalprediction/step/3.html)
+ Implantar o seu script de ML: [usando um modelo do R](https://microsoft.github.io/sql-ml-tutorials/R/rentalprediction/step/3.html)

## <a name="requirements"></a>Requisitos

Plataformas com suporte são da seguinte maneira:

+ Serviços de aprendizado de máquina do SQL Server 2017 (inclui o Microsoft R Server 9.1.0)
    
    Pontuação nativa usando PREDICT requer o SQL Server 2017.
    Ele funciona em qualquer versão do SQL Server 2017, incluindo Linux.

    Você também pode executar usando sp_rxPredict de pontuação em tempo real. Para usar este procedimento armazenado exige que você habilite [integração de CLR do SQL Server](https://docs.microsoft.com/dotnet/framework/data/adonet/sql/introduction-to-sql-server-clr-integration).

+ SQL Server 2016

   Em tempo real de pontuação usando sp_rxPredict é possível com o SQL Server 2016 e também pode ser executado no Microsoft R Server. Essa opção requer o SQLCLR esteja habilitado e que você instale a atualização do Microsoft R Server.
   Para obter mais informações, consulte [de pontuação em tempo real](Real-time-scoring.md)

### <a name="model-preparation"></a>Preparação de modelo

+ O modelo deve ser treinado com antecedência usando um com suporte **rx** algoritmos. Para obter detalhes, consulte [suporte para algoritmos](#bkmk_native_supported_algos).
+ O modelo deve ser salvo usando a nova função de serialização fornecida no Microsoft R Server 9.1.0. A função de serialização é otimizada para dar suporte a pontuação rápida.

### <a name="bkmk_native_supported_algos"></a> Algoritmos que dão suporte a pontuação nativa

+ Modelos de RevoScaleR

  + [rxLinMod](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxlinmod)
  + [rxLogit](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxlogit)
  + [rxBTrees](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxbtrees)
  + [rxDtree](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxdtree)
  + [rxDForest](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxdforest)

Se você precisar usar modelos do MicrosoftML, use a pontuação em tempo real com sp_rxPredict.

### <a name="restrictions"></a>Restrictions

Não há suporte para os seguintes tipos de modelo:

+ Modelos que contenham outros tipos de transformações de R sem suporte
+ Os modelos usando o `rxGlm` ou `rxNaiveBayes` algoritmos de RevoScaleR
+ Modelos PMML
+ Modelos criados usando outras bibliotecas de R do CRAN ou outros repositórios
+ Modelos que contenham qualquer outra transformação de R

## <a name="see-also"></a>Confira também

[Pontuação no aprendizado de máquina do SQL Server em tempo real ](real-time-scoring.md)