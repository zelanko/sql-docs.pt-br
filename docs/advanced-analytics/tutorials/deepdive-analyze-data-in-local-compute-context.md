---
title: Analisar dados no contexto de computação local (SQL e R mergulho profundo) | Microsoft Docs
ms.date: 12/18/2017
ms.reviewer: ''
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: ''
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: tutorial
applies_to:
- SQL Server 2016
- SQL Server 2017
dev_langs:
- R
ms.author: heidist
author: HeidiSteen
manager: cgronlun
ms.workload: Inactive
ms.openlocfilehash: e521ae9ab359ac210383cfb56ded80da4ed181ff
ms.sourcegitcommit: 059fc64ba858ea2adaad2db39f306a8bff9649c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/04/2018
---
# <a name="analyze-data-in-local-compute-context-sql-and-r-deep-dive"></a>Analisar dados no contexto de computação local (SQL e R mergulho profundo)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Este artigo faz parte do tutorial mergulho profundo de ciência de dados, como usar [RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) com o SQL Server.

Nesta seção, você aprenderá como alternar para um contexto de computação local e mover dados entre contextos para otimizar o desempenho.

Embora i pode ser mais rápido executar o código de R complexo usando o contexto do servidor, às vezes, é mais conveniente obter os dados de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e analisá-lo em uma estação de trabalho local.

## <a name="create-a-local-summary"></a>Criar um resumo de local

1. Altere o contexto de computação para fazer todo o seu trabalho localmente.
  
    ```R
    rxSetComputeContext ("local")
    ```
  
2. Ao extrair dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], muitas vezes, é possível obter um desempenho melhor aumentando o número de linhas extraídas para cada leitura.  Para fazer isso, aumente o valor do parâmetro *rowsPerRead* na fonte de dados. Anteriormente, o valor de *rowsPerRead* estava definido como 5000.
  
    ```R
    sqlServerDS1 <- RxSqlServerData(
       connectionString = sqlConnString,
       table = sqlFraudTable,
       colInfo = ccColInfo,
       rowsPerRead = 10000)
    ```

3. Chamar **rxSummary** na nova fonte de dados.
  
    ```R
    rxSummary(formula = ~gender + balance + numTrans + numIntlTrans + creditLine, data = sqlServerDS1)
    ```
  
    Os resultados reais devem ser iguais a quando você executa **rxSummary** no contexto do computador [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  No entanto, a operação pode ser mais rápida ou mais lenta. Depende muito da conexão com seu banco de dados, pois os dados estão sendo transferidos para o computador local para análise.

## <a name="next-step"></a>Próxima etapa

[Mover dados entre o SQL Server e o arquivo XDF](../../advanced-analytics/tutorials/deepdive-move-data-between-sql-server-and-xdf-file.md)

## <a name="previous-step"></a>Etapa anterior

[Executar análise de agrupamento usando rxDataStep](../../advanced-analytics/tutorials/deepdive-perform-chunking-analysis-using-rxdatastep.md)
