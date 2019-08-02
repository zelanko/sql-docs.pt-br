---
title: Executar análise de agrupamento usando RevoScaleR rxDataStep
description: Tutorial explicativo sobre como dividir dados para análise distribuída usando a linguagem R no SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/27/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: ed22020b162bfac9f35eb8328ea6409903191a4c
ms.sourcegitcommit: 321497065ecd7ecde9bff378464db8da426e9e14
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/01/2019
ms.locfileid: "68714889"
---
# <a name="perform-chunking-analysis-using-rxdatastep-sql-server-and-revoscaler-tutorial"></a>Executar análise de agrupamento usando rxDataStep (tutorial de SQL Server e RevoScaleR)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Esta lição faz parte do [tutorial do RevoScaleR](deepdive-data-science-deep-dive-using-the-revoscaler-packages.md) sobre como usar as [funções do RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) com SQL Server.

Nesta lição, você usará a função **rxDataStep** para processar dados em partes, em vez de exigir que todo o conjunto seja carregado na memória e processado de uma só vez, como no R tradicional. As funções **rxDataStep** lêem os dados no bloco, aplicam funções de R a cada bloco de dados por vez e, em seguida, salva os resultados de resumo para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] cada parte em uma fonte de dados comum. Quando todos os dados tiverem sido lidos, os resultados serão combinados.

> [!TIP]
> Nesta lição, você computa uma tabela de contingência usando a função de **tabela** no R. Este exemplo destina-se apenas a fins de instrução. 
> 
> Se você precisar tabular conjuntos de dados do mundo real, recomendamos que use as funções **rxCrossTabs** ou **rxCube** no **RevoScaleR**, que são otimizadas para esse tipo de operação.

## <a name="partition-data-by-values"></a>Particionar dados por valores

1. Crie uma função de R personalizada que chama a função de **tabela** r em cada parte dos dados e nomeie a nova função **ProcessChunk**.
  
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
  
3. Defina uma SQL Server fonte de dados para manter os dados que você está processando. Comece atribuindo uma consulta SQL a uma variável. Em seguida, use essa variável no argumento SQLQuery de uma nova fonte de dados SQL Server.
  
    ```R
    dayQuery <-  "SELECT DayOfWeek FROM AirDemoSmallTest"
    inDataSource <- RxSqlServerData(sqlQuery = dayQuery,
        connectionString = sqlConnString,
        rowsPerRead = 50000,
        colInfo = list(DayOfWeek = list(type = "factor",
            levels = as.character(1:7))))
    ```

4. Opcionalmente, você pode executar **rxGetVarInfo** nessa fonte de dados. Neste ponto, ele contém uma única coluna: *Var 1: DayOfWeek, tipo: fator, nenhum nível de fator disponível*
     
5. Antes de aplicar essa variável de fator aos dados de origem, crie uma tabela separada para manter os resultados intermediários. Novamente, basta usar a função **RxSqlServerData** para definir os dados, certificando-se de excluir todas as tabelas existentes de mesmo nome.
  
    ```R
    iroDataSource = RxSqlServerData(table = "iroResults",   connectionString = sqlConnString)
    # Check whether the table already exists.
    if (rxSqlServerTableExists(table = "iroResults",  connectionString = sqlConnString))  { rxSqlServerDropTable( table = "iroResults", connectionString = sqlConnString) }
    ```
  
7.  Chame a função personalizada **ProcessChunk** para transformar os dados conforme eles são lidos, usando-os como o argumento *transformFunc* para a função **rxDataStep** .
  
    ```R
    rxDataStep( inData = inDataSource, outFile = iroDataSource, transformFunc = ProcessChunk, overwrite = TRUE)
    ```
  
8.  Para exibir os resultados intermediários de **ProcessChunk**, atribua os resultados de **rxImport** a uma variável e, em seguida, gere os resultados para o console.
  
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