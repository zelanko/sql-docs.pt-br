---
title: Análise de agrupamento no RevoScaleR
description: 'Tutorial 12 do RevoScaleR: como agrupar dados para análise distribuída usando a linguagem R no SQL Server.'
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 11/27/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 094354c0e5039d70bac0cb4463aa5323b294a3e3
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85680023"
---
# <a name="perform-chunking-analysis-using-rxdatastep-sql-server-and-revoscaler-tutorial"></a>Executar análise de agrupamento usando rxDataStep (tutorial do SQL Server e do RevoScaleR)
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

Este é o tutorial 12 da [série de tutoriais do RevoScaleR](deepdive-data-science-deep-dive-using-the-revoscaler-packages.md) sobre como usar as [funções do RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) com o SQL Server.

Neste tutorial, você usará a função **rxDataStep** para processar dados em partes, em vez de exigir que todo o conjunto de dados seja carregado na memória e processado de uma vez, como no R tradicional. As funções **rxDataStep** leem os dados em partes, aplicam as funções do R a cada parte de dados por vez e salvam os resultados resumidos para cada parte em uma fonte de dados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] comum. Quando todos os dados tiverem sido lidos, os resultados serão combinados.

> [!TIP]
> Neste tutorial, calcule uma tabela de contingência usando a função **table** no R. Esse exemplo serve apenas para fins de instrução. 
> 
> Se você precisar tabular conjuntos de dados do mundo real, será recomendável usar as funções **rxCrossTabs** ou **rxCube** no **RevoScaleR**, que são otimizadas para esse tipo de operação.

## <a name="partition-data-by-values"></a>Particionar os dados por valores

1. Crie uma função do R personalizada que chame a função **table** do R em cada parte de dados e dê à nova função o nome **ProcessChunk**.
  
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
    rxSetComputeContext(sqlCompute)
    ```
  
3. Defina uma fonte de dados do SQL Server para armazenar os dados que você está processando. Comece atribuindo uma consulta SQL a uma variável. Em seguida, use essa variável no argumento *sqlQuery* de uma nova fonte de dados do SQL Server.
  
    ```R
    dayQuery <-  "SELECT DayOfWeek FROM AirDemoSmallTest"
    inDataSource <- RxSqlServerData(sqlQuery = dayQuery,
        connectionString = sqlConnString,
        rowsPerRead = 50000,
        colInfo = list(DayOfWeek = list(type = "factor",
            levels = as.character(1:7))))
    ```

4. Ou você pode executar **rxGetVarInfo** nessa fonte de dados. Neste ponto, ela contém uma única coluna: *Var 1: DayOfWeek, Type: factor, no factor levels available*
     
5. Antes de aplicar essa variável de fator aos dados de origem, crie uma tabela separada para manter os resultados intermediários. Novamente, use apenas a função **RxSqlServerData** para definir os dados, lembrando-se de excluir as tabelas existentes de mesmo nome.
  
    ```R
    iroDataSource = RxSqlServerData(table = "iroResults",   connectionString = sqlConnString)
    # Check whether the table already exists.
    if (rxSqlServerTableExists(table = "iroResults",  connectionString = sqlConnString))  { rxSqlServerDropTable( table = "iroResults", connectionString = sqlConnString) }
    ```
  
7.  Chame a função personalizada **ProcessChunk** para transformar os dados conforme eles são lidos, usando-a como o argumento *transformFunc* para a função **rxDataStep**.
  
    ```R
    rxDataStep( inData = inDataSource, outFile = iroDataSource, transformFunc = ProcessChunk, overwrite = TRUE)
    ```
  
8.  Para exibir resultados intermediários de **ProcessChunk**, atribua os resultados de **rxImport** a uma variável e, em seguida, transfira os resultados para o console.
  
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

10. Para remover a tabela de resultados intermediários, faça uma chamada para **rxSqlServerDropTable**.
  
    ```R
    rxSqlServerDropTable( table = "iroResults", connectionString = sqlConnString)
    ```

## <a name="next-steps"></a>Próximas etapas

> [!div class="nextstepaction"]
> [Tutoriais de R para SQL Server](sql-server-r-tutorials.md)