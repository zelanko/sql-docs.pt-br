---
title: "Executar análise de agrupamento usando rxDataStep | Microsoft Docs"
ms.custom: 
ms.date: 05/03/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
applies_to: SQL Server 2016
dev_langs: R
ms.assetid: 4290ee5f-be90-446a-91e8-3095d694bd82
caps.latest.revision: "17"
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 7fb2f00e3506514c7d4870763052df2558f47aa4
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2017
---
# <a name="perform-chunking-analysis-using-rxdatastep"></a>Executar análise de agrupamento usando rxDataStep

A função **rxDataStep** pode ser usada para processar dados em partes, em vez de exigir que o conjunto de dados inteiro seja carregado na memória e processado de uma vez, como ocorre no R tradicional. Ele funciona da seguinte forma: você lê os dados em partes e usa funções de R para processar cada parte por vez e, em seguida, grava os resultados resumidos para cada bloco em uma fonte de dados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] comum.

Nesta lição, você aprenderá a essa técnica, usando o `table` função em R, para calcular uma tabela de contingência.

> [!TIP]
> Este exemplo destina-se apenas a fins de instrução. Se você precisar tabular conjuntos de dados do mundo real, é recomendável que você use o **rxCrossTabs** ou **rxCube** funções em **RevoScaleR**, que são otimizados para este tipo de operação.

## <a name="partition-data-by-values"></a>Particionar os dados por valores

1. Primeiro, crie uma função R personalizada que chama o *tabela* funciona em cada bloco de dados e o nome de `ProcessChunk`.
  
    ```R
    ProcessChunk <- function( dataList) {
    # Convert the input list to a data frame and compute contingency table
    chunkTable <- table(as.data.frame(dataList))
  
    # Convert table output to a data frame with a single row
    varNames <- names(chunkTable)
    varValues <- as.vector(chunkTable)
    dim(varValues) <- c(1, length(varNames))
    chunkDF <- as.data.frame(varValues)
    names(chunkDF) <- varNames
  
    # Return the data frame, which has a single row
    return( chunkDF )
    }
    ```

2. Defina o contexto de computação como o servidor.
  
    ```R
    rxSetComputeContext( sqlCompute )
    ```
  
3. Você definirá uma fonte de dados do SQL Server para armazenar os dados que está processando. Comece atribuindo uma consulta SQL a uma variável.
  
    ```R
    dayQuery <-  "SELECT DayOfWeek FROM AirDemoSmallTest"
    ```

4. Conecte essa variável ao argumento *sqlQuery* de uma nova fonte de dados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .
  
    ```R
    inDataSource <- RxSqlServerData(sqlQuery = dayQuery,
        connectionString = sqlConnString,
        rowsPerRead = 50000,
        colInfo = list(DayOfWeek = list(type = "factor",
            levels = as.character(1:7))))
    ```
     Se tiver executado *rxGetVarInfo* nessa fonte de dados, você verá que ela contém apenas a única coluna: *Var 1: DayOfWeek, Type: factor, no factor levels available*
     
5. Antes de aplicar essa variável de fator aos dados de origem, crie uma tabela separada para manter os resultados intermediários. Novamente, você simplesmente usa a função RxSqlServerData para definir os dados e excluir todas as tabelas existentes de mesmo nome.
  
    ```R
    iroDataSource = RxSqlServerData(table = "iroResults",   connectionString = sqlConnString)
    # Check whether the table already exists.
    if (rxSqlServerTableExists(table = "iroResults",  connectionString = sqlConnString))  { rxSqlServerDropTable( table = "iroResults", connectionString = sqlConnString) }
    ```
  
7.  Agora você chamará a função personalizada `ProcessChunk` para transformar os dados conforme é lida, usando-o como o *transformFunc* argumento para a função rxDataStep.
  
    ```R
    rxDataStep( inData = inDataSource, outFile = iroDataSource, transformFunc = ProcessChunk, overwrite = TRUE)
    ```
  
8.  Para exibir os resultados intermediários de `ProcessChunk`, atribua os resultados do rxImport a uma variável e, em seguida, os resultados para o console de saída.
  
    ```R
    iroResults <- rxImport(iroDataSource)
    iroResults
    ```

**Resultados parciais**

|      |    1  |   2   |  3   |  4   |  5  |   6   |  7 |
| --- | ---  | --- | ---  |  ---  | ---  | ---  | --- |
| 1 | 8228 | 8924 | 6916 | 6932 | 6944 | 5602 | 6454 |
| 2  | 8321  | 5351 | 7329 | 7411 | 7409 | 6487 | 7692 |

9. Para calcular os resultados finais em todas as partes, some as colunas e exiba os resultados no console.

    ```R
    finalResults <- colSums(iroResults)
    finalResults
    ```

 **Resultados**
  1  |   2  |   3  |   4  |   5  |   6  |   7
---  |   ---  |   ---  |   ---  |   ---  |   ---  |   ---
97975 | 77725 | 78875 | 81304 | 82987 | 86159 | 94975 

10. Para remover a tabela de resultados intermediários, fazer outra chamada para rxSqlServerDropTable.
  
    ```R
    rxSqlServerDropTable( table = "iroResults",     connectionString = sqlConnString)
    ```

## <a name="next-step"></a>Próxima etapa

[Analisar dados no contexto de computação Local;](../../advanced-analytics/tutorials/deepdive-analyze-data-in-local-compute-context.md)

## <a name="previous-step"></a>Etapa anterior

[Criar nova tabela do SQL Server usando rxDataStep](../../advanced-analytics/tutorials/deepdive-create-new-sql-server-table-using-rxdatastep.md)


