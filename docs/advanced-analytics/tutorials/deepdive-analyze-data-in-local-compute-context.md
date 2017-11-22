---
title: "Analisar dados no contexto de computação Local | Microsoft Docs"
ms.custom: 
ms.date: 05/18/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
applies_to: SQL Server 2016
dev_langs: R
ms.assetid: 787bb526-4a13-40fa-9343-75d3bf5ba6a2
caps.latest.revision: "13"
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 514cc855af010347006054ad30fc5e5c36b16322
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2017
---
# <a name="analyze-data-in-local-compute-context-data-science-deep-dive"></a>Analisar dados no contexto de computação Local (mergulho profundo ciência de dados)

Embora possa ser mais rápido executar o código de R complexo usando o contexto do servidor, às vezes é apenas mais conveniente obter os dados de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e analisá-los em sua estação de trabalho particular.

Nesta seção, você aprenderá a voltar para um contexto de computação local e mover dados entre contextos para otimizar o desempenho.

## <a name="create-a-local-summary"></a>Criar um resumo local

1. Altere o contexto de computação para fazer todo o seu trabalho localmente.
  
    ```R
    rxSetComputeContext ("local")
    ```
  
2. Ao extrair dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], muitas vezes, é possível obter um desempenho melhor aumentando o número de linhas extraídas para cada leitura.  Para fazer isso, aumente o valor do parâmetro *rowsPerRead* na fonte de dados.
  
    ```R
    sqlServerDS1 <- RxSqlServerData(
       connectionString = sqlConnString,
       table = sqlFraudTable,
       colInfo = ccColInfo,
       rowsPerRead = 10000)
    ```
  
    Anteriormente, o valor de *rowsPerRead* estava definido como 5000.
  
3. Agora, chame **rxSummary** na nova fonte de dados.
  
    ```R
    rxSummary(formula = ~gender + balance + numTrans + numIntlTrans + creditLine, data = sqlServerDS1)
    ```
  
    Os resultados reais devem ser o mesmo ao executar no contexto de rxSummary a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] computador.  No entanto, a operação pode ser mais rápida ou mais lenta. Depende muito da conexão com seu banco de dados, pois os dados estão sendo transferidos para o computador local para análise.


## <a name="next--step"></a>Próxima etapa

[Mover dados entre o SQL Server e o arquivo XDF](../../advanced-analytics/tutorials/deepdive-move-data-between-sql-server-and-xdf-file.md)

## <a name="previous-step"></a>Etapa anterior

[Executar análise de agrupamento usando rxDataStep](../../advanced-analytics/tutorials/deepdive-perform-chunking-analysis-using-rxdatastep.md)


