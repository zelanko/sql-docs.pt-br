---
title: Executar análise de agrupamento usando rxDataStep RevoScaleR - aprendizagem de máquina do SQL Server
description: Tutorial passo a passo sobre como dividir dados para análise distribuída usando a linguagem R no SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/27/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.openlocfilehash: 6ccc64c98f0519b33b6ba9da180c01e4478492f6
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67962203"
---
# <a name="perform-chunking-analysis-using-rxdatastep-sql-server-and-revoscaler-tutorial"></a>Executar análise de agrupamento usando rxDataStep (tutorial do SQL Server e o RevoScaleR)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Esta lição é parte do [tutorial de RevoScaleR](deepdive-data-science-deep-dive-using-the-revoscaler-packages.md) sobre como usar [funções RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) com o SQL Server.

Nesta lição, você deve usar o **rxDataStep** de função para processar dados em partes, em vez de exigir que todo o conjunto de dados ser carregado na memória e processado ao mesmo tempo, como no r tradicional. O **rxDataStep** funções lê os dados no bloco, aplica funções de R para cada bloco de dados por sua vez e, em seguida, salva os resultados de resumidos para cada bloco em um comum [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] fonte de dados. Quando todos os dados foram lidos, os resultados são combinados.

> [!TIP]
> Nesta lição, você deve calcular uma tabela de contingência usando o **tabela** função em R. Este exemplo destina-se apenas para fins de ensino. 
> 
> Se você precisar tabular conjuntos de dados do mundo real, é recomendável que você use o **rxCrossTabs** ou **rxCube** funções na **RevoScaleR**, que são otimizados para este tipo de operação.

## <a name="partition-data-by-values"></a>Particionar os dados por valores

1. Criar uma função personalizada do R que chama o R **tabela** funcionarão em cada bloco de dados e nomeie a nova função **ProcessChunk**.
  
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
  
3. Defina uma fonte de dados do SQL Server para manter os dados que você está processando. Comece atribuindo uma consulta SQL a uma variável. Em seguida, use essa variável na *sqlQuery* argumento de uma nova fonte de dados do SQL Server.
  
    ```R
    dayQuery <-  "SELECT DayOfWeek FROM AirDemoSmallTest"
    inDataSource <- RxSqlServerData(sqlQuery = dayQuery,
        connectionString = sqlConnString,
        rowsPerRead = 50000,
        colInfo = list(DayOfWeek = list(type = "factor",
            levels = as.character(1:7))))
    ```

4. Opcionalmente, você pode executar **rxGetVarInfo** nessa fonte de dados. Neste ponto, ele contém uma única coluna: *Var 1: DayOfWeek, Type: factor, não há níveis de fator disponíveis*
     
5. Antes de aplicar essa variável de fator aos dados de origem, crie uma tabela separada para manter os resultados intermediários. Novamente, basta usar o **RxSqlServerData** função para definir os dados, certificando-se de excluir as tabelas existentes de mesmo nome.
  
    ```R
    iroDataSource = RxSqlServerData(table = "iroResults",   connectionString = sqlConnString)
    # Check whether the table already exists.
    if (rxSqlServerTableExists(table = "iroResults",  connectionString = sqlConnString))  { rxSqlServerDropTable( table = "iroResults", connectionString = sqlConnString) }
    ```
  
7.  Chame a função personalizada **ProcessChunk** para transformar os dados conforme eles são lidos, usando-o como o *transformFunc* argumento para o **rxDataStep** função.
  
    ```R
    rxDataStep( inData = inDataSource, outFile = iroDataSource, transformFunc = ProcessChunk, overwrite = TRUE)
    ```
  
8.  Para exibir os resultados intermediários de **ProcessChunk**, atribua os resultados do **rxImport** a uma variável e, em seguida, os resultados no console de saída.
  
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

## <a name="next-steps"></a>Próximas etapas

> [!div class="nextstepaction"]
> [Tutoriais de R para SQL Server](sql-server-r-tutorials.md)