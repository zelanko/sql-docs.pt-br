---
title: "Pontuação nativo | Microsoft Docs"
ms.custom: 
ms.date: 07/16/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: e1cb06223e5274c1fa439eb9f7d82a005e93a47d
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---

# <a name="native-scoring"></a>Nativo de pontuação

Este tópico descreve os recursos do SQL Server 2017 que fornecem a pontuação em modelos de aprendizado de máquina em tempo quase real.

+ O que é nativo pontuação versus em tempo real de pontuação
+ Como ele funciona
+ Requisitos e plataformas com suporte

## <a name="what-is-native-scoring-and-how-is-it-different-from-realtime-scoring"></a>Qual é a pontuação nativo e como ele é diferente de pontuação em tempo real?

No SQL Server 2016, a Microsoft criou uma estrutura de extensibilidade que permite que os scripts de R a partir do T-SQL. Essa estrutura oferece suporte a qualquer operação que você pode executar em R, variando de funções simples para modelos de aprendizado de máquina complexa de treinamento. No entanto, a arquitetura dual-processo que pares R com o SQL Server significa que processos externos de R devem ser chamados para cada chamada, independentemente da complexidade da operação. Se você estiver carregando um modelo previamente treinado de uma tabela e pontuação em relação a ela em dados já existentes no SQL Server, a sobrecarga de chamar o processo de R externo representa um custo de desempenho desnecessários.

_Pontuação_ é um processo de duas etapas: um modelo previamente treinado é carregado de uma tabela, e novos dados de entrada, linhas de tabela ou único, são passados para o modelo, o que gera novos valores (ou _pontuações_). A saída pode ser um valor de coluna única que representa a probabilidade de uma ou vários valores, incluindo um intervalo de confiança, erro ou outro complemento útil para a previsão.

Quando muitas linhas de dados de pontuação, os novos valores geralmente são inseridos em uma tabela como parte do procedimento de pontuação.  No entanto, você também pode recuperar uma única pontuação em tempo real. Quando as entradas de pontuação, o modelo pode armazenados em cache para que ele pode ser recarregado no rápido de memória.

Para dar suporte a pontuação rápido, serviços de aprendizado de máquina do SQL Server (e Microsoft Server de aprendizado de máquina) fornecem bibliotecas internas de pontuação que funcionam em R ou no T-SQL. Há diferentes opções dependendo de qual versão você tem.

**Nativo de pontuação**

+ A função de previsão no Transact-SQL pode ser usada para _pontuação nativo_ de qualquer instância do SQL Server 2017. Requer apenas que você tenha um modelo já treinado e salvos em uma tabela ou pode ser chamado por meio do T-SQL. É um tipo de pontuação em tempo real que usa funções nativas do T-SQL; Nenhuma configuração adicional necessária.

   O tempo de execução de R não é chamado e não precisa ser instalado.

**Em tempo real de pontuação**

+ **sp_rxPredict** é um procedimento armazenado para em tempo real de pontuação que pode ser usado para gerar pontuações de qualquer tipo de modelo com suporte, sem chamar o tempo de execução de R.

  Esta opção para usar em tempo real de pontuação também está disponível no SQL Server 2016, se você atualizar os componentes de R usando o instalador autônomo do Microsoft R Server. sp_rxPredict também é suportado no SQL Server 2017 e pode ser uma boa opção se você está Pontuando em um tipo de modelo não tem suportado pela função de previsão.

+ A função rxPredict pode ser usada para pontuação rápida no código de R.

Para todos esses métodos de pontuação, você deve usar um modelo que foi treinado usando um dos algoritmos de RevoScaleR ou MicrosoftML com suporte.

Para obter um exemplo em tempo real de pontuação em ação, consulte [final final empréstimo ChargeOff previsão criados usando o Azure HDInsight Spark Clusters e o serviço do SQL Server 2016 R](https://blogs.msdn.microsoft.com/rserver/2017/06/29/end-to-end-loan-chargeoff-prediction-built-using-azure-hdinsight-spark-clusters-and-sql-server-2016-r-service/)

## <a name="how-native-scoring-works"></a>Funciona como nativa de pontuação

Pontuação nativo usa bibliotecas nativas C++ da Microsoft que podem ler o modelo de um formato binário especial e gerar pontuações. Como um modelo pode ser publicado e usado para pontuação sem a necessidade de chamar o interpretador de R, a sobrecarga de várias interações do processo é reduzida. Isso dá suporte a desempenho muito mais rápido de previsão em cenários de produção da empresa.

Para gerar pontuações usando essa biblioteca, chame a função de pontuação e passar as seguintes entradas necessárias:

+ Um modelo compatível. Consulte o [requisitos](#Requirements) seção para obter detalhes.
+ Dados de entrada, costumam ser definidos como uma consulta SQL

A função retorna previsões para os dados de entrada, junto com as colunas de dados de origem que você deseja passar.

Para obter exemplos de código, juntamente com instruções sobre como preparar os modelos no formato binário exigido, consulte este artigo:

+ [Como realizar em tempo real de pontuação](r/how-to-do-realtime-scoring.md)

## <a name="requirements"></a>Requisitos

Plataformas com suporte são os seguintes:

+ Serviços de aprendizado de máquina do SQL Server de 2017 (inclui o Microsoft R Server 9.1.0)
    
    Pontuação nativo usando PREVER requer 2017 do SQL Server.
    Ele funciona em qualquer versão do SQL Server de 2017, inclusive Linux.

    Você também pode realizar em tempo real de pontuação usando sp_rxPredict, que exige a ativação de SQL CLR.

+ SQL Server 2016

   Em tempo real de pontuação usando sp_rxPredict é possível com o SQL Server 2016 e também pode ser executado no Microsoft R Server. Essa opção requer SQLCLR esteja habilitado e que você instale a atualização do Microsoft R Server.
   Para obter mais informações, consulte [em tempo real de pontuação](Real-time-scoring.md)

### <a name="model-preparation"></a>Preparação de modelo

+ O modelo deve ser treinado com antecedência usando um com suporte **rx** algoritmos. Para obter detalhes, consulte [suporte para algoritmos](#bkmk_native_supported_algos).
+ O modelo deve ser salvo usando a nova função de serialização fornecida no Microsoft R Server 9.1.0. A função de serialização é otimizada para oferecer suporte a pontuação rápida.

### <a name="bkmk_native_supported_algos"></a>Algoritmos que oferecem suporte nativo de pontuação

+ Modelos de RevoScaleR

  + [rxLinMod](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxlinmod)
  + [rxLogit](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxlogit)
  + [rxBTrees](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxbtrees)
  + [rxDtree](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxdtree)
  + [rxdForest](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxdforest)

Se você precisar usar modelos de MicrosoftML, use em tempo real com sp_rxPredict de pontuação.

### <a name="restrictions"></a>Restrições

Não há suporte para os seguintes tipos de modelo:

+ Modelos que contém outros tipos de transformações de R sem suporte
+ Modelos usando o `rxGlm` ou `rxNaiveBayes` algoritmos em RevoScaleR
+ Modelos PMML
+ Modelos criados usando outras bibliotecas de R de CRAN ou outros repositórios
+ Modelos que contêm qualquer outro tipo de transformação de R

