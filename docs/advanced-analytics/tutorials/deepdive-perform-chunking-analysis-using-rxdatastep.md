---
title: Executar a análise das partes usando rxDataStep (SQL e R mergulho profundo) | Microsoft Docs
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 5db0acfb90c200442489cd7c3ec464223195eec6
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="perform-chunking-analysis-using-rxdatastep-sql-and-r-deep-dive"></a>Executar a análise das partes usando rxDataStep (SQL e R mergulho profundo)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Este artigo faz parte do tutorial mergulho profundo de ciência de dados, como usar [RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) com o SQL Server.

Nesta lição, você deve usar o **rxDataStep** de função para processar dados em partes, em vez de exigir que o conjunto de dados ser carregado na memória e processado ao mesmo tempo, como r tradicional. O **rxDataStep** funções lê os dados no bloco, aplica funções de R para cada bloco de dados, por sua vez e, em seguida, salva os resultados de resumos para cada bloco em um comum [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] fonte de dados. Quando todos os dados são lidos, os resultados são combinados.

> [!TIP]
> Nesta lição, você deve calcular uma tabela de contingência usando o `table` função em R. Este exemplo destina-se apenas para fins de instrução. 
> 
> Se você precisar tabular conjuntos de dados do mundo real, é recomendável que você use o **rxCrossTabs** ou **rxCube** funções em **RevoScaleR**, que são otimizados para este tipo de operação.

## <a name="partition-data-by-values"></a>Particionar dados por valores

1. Criar uma função de R personalizada que chama o R `table` de função em cada bloco de dados e nomear a nova função `ProcessChunk`.
  
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
  
3. Defina uma fonte de dados do SQL Server para manter os dados que você está processando. Comece atribuindo uma consulta SQL a uma variável. Em seguida, usar essa variável no *sqlQuery* argumento de um novo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] fonte de dados.
  
  
    ```R
    dayQuery <-  "SELECT DayOfWeek FROM AirDemoSmallTest"
    inDataSource <- RxSqlServerData(sqlQuery = dayQuery,
        connectionString = sqlConnString,
        rowsPerRead = 50000,
        colInfo = list(DayOfWeek = list(type = "factor",
            levels = as.character(1:7))))
    ```
4. Opcionalmente, você pode executar **à função rxGetVarInfo** nessa fonte de dados. Neste ponto, ele contém uma única coluna: *Var 1: DayOfWeek, digite: fator, não há níveis de fator disponíveis*
     
5. Antes de aplicar essa variável de fator aos dados de origem, crie uma tabela separada para manter os resultados intermediários. Novamente, você simplesmente usar a função RxSqlServerData para definir os dados, makign certeza que deseja excluir todas as tabelas existentes de mesmo nome.
  
    ```R
    iroDataSource = RxSqlServerData(table = "iroResults",   connectionString = sqlConnString)
    # Check whether the table already exists.
    if (rxSqlServerTableExists(table = "iroResults",  connectionString = sqlConnString))  { rxSqlServerDropTable( table = "iroResults", connectionString = sqlConnString) }
    ```
  
7.  Chame a função personalizada `ProcessChunk` para transformar os dados conforme é lida, usando-o como o *transformFunc* argumento para o **rxDataStep** função.
  
    ```R
    rxDataStep( inData = inDataSource, outFile = iroDataSource, transformFunc = ProcessChunk, overwrite = TRUE)
    ```
  
8.  Para exibir os resultados intermediários de `ProcessChunk`, atribua os resultados do **rxImport** a uma variável e, em seguida, os resultados para o console de saída.
  
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

10. Para remover a tabela de resultados intermediários, fazer uma chamada para **rxSqlServerDropTable**.
  
    ```R
    rxSqlServerDropTable( table = "iroResults", connectionString = sqlConnString)
    ```

## <a name="next-step"></a>Próxima etapa

[Analisar dados no contexto de computação local](../../advanced-analytics/tutorials/deepdive-analyze-data-in-local-compute-context.md)

## <a name="previous-step"></a>Etapa anterior

[Criar nova tabela do SQL Server usando rxDataStep](../../advanced-analytics/tutorials/deepdive-create-new-sql-server-table-using-rxdatastep.md)
