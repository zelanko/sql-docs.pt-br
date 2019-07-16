---
title: Criar nova tabela do SQL Server usando rxDataStep RevoScaleR - aprendizagem de máquina do SQL Server
description: Tutorial passo a passo sobre como criar uma tabela do SQL Server usando a linguagem R no SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/27/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.openlocfilehash: 484f238e53db21030b04cdf46b86271236509989
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67962262"
---
# <a name="create-new-sql-server-table-using-rxdatastep-sql-server-and-revoscaler-tutorial"></a>Criar nova tabela do SQL Server usando rxDataStep (tutorial do SQL Server e o RevoScaleR)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Esta lição é parte do [tutorial de RevoScaleR](deepdive-data-science-deep-dive-using-the-revoscaler-packages.md) sobre como usar [funções RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) com o SQL Server.

Nesta lição, você aprenderá a mover dados entre os quadros de dados na memória, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] contexto e os arquivos locais.

> [!NOTE]
> Esta lição usa um conjunto de dados diferente. O conjunto de dados de atrasos de companhias aéreas é um conjunto de dados público que é amplamente usado para experimentos de aprendizado de máquina. Os arquivos de dados usados neste exemplo estão disponíveis no mesmo diretório que outras amostras de produto.

## <a name="load-data-from-a-local-xdf-file"></a>Carregar dados de um arquivo XDF local

Na primeira metade deste tutorial, você usou o **RxTextData** funcionar para importar dados no R de um arquivo de texto e, em seguida, é usado o **RxDataStep** função para mover os dados para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].

Nesta lição adota uma abordagem diferente, e usa dados de um arquivo salvo na [formato XDF](https://en.wikipedia.org/wiki/Extensible_Data_Format). Depois de fazer algumas transformações simples nos dados usando o arquivo XDF, você deve salvar os dados transformados em um novo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tabela.

**O que é XDF?**

O formato XDF é um padrão XML desenvolvido para dados altamente dimensionais e é o formato de arquivo nativo usado pelo [Machine Learning Server](https://docs.microsoft.com/machine-learning-server/r/concept-what-is-xdf). Trata-se de um formato de arquivo binário com uma interface de R que otimiza a análise e o processamento de linhas e colunas.  Você pode usá-lo para mover dados e armazenar subconjuntos de dados que são úteis para análise.

1. Defina o contexto de computação como a estação de trabalho local. **São necessárias permissões de DDL para esta etapa.**

    ```R
    rxSetComputeContext("local")
    ```
  
2. Defina um novo objeto de fonte de dados usando a função **RxXdfData** . Para definir uma fonte de dados XDF, especifique o caminho para o arquivo de dados.  

    Você pode especificar o caminho para o arquivo usando uma variável de texto. No entanto, nesse caso, há um atalho útil, que é usar o **rxGetOption** de função e obter o arquivo (Airlinedemosmall) do diretório de dados de exemplo.
  
    ```R
    xdfAirDemo <- RxXdfData(file.path(rxGetOption("sampleDataDir"),  "AirlineDemoSmall.xdf"))
    ```

3. Chame [rxGetVarInfo](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxgetvarinfoxdf) nos dados na memória para exibir um resumo do conjunto de dados.
  
    ```R
    rxGetVarInfo(xdfAirDemo)
    ```

**Resultados**

```R
Var 1: ArrDelay, Type: integer, Low/High: (-86, 1490)
Var 2: CRSDepTime, Type: numeric, Storage: float32, Low/High: (0.0167, 23.9833)
Var 3: DayOfWeek 7 factor levels: Monday Tuesday Wednesday Thursday Friday Saturday Sunday
```

> [!NOTE]
> 
> Você notou que não precisava chamar nenhuma outra função para carregar os dados no arquivo XDF e poderia chamar **rxGetVarInfo** nos dados imediatamente? Isso ocorre porque XDF é o método de armazenamento provisório padrão para **RevoScaleR**. Além dos arquivos XDF, o **rxGetVarInfo** função agora dá suporte a vários tipos de origem.

## <a name="move-contents-to-sql-server"></a>Mover conteúdo para o SQL Server

Com a fonte de dados do XDF criada na sessão local do R, agora você pode passar esses dados em uma tabela de banco de dados, armazenando *DayOfWeek* como um inteiro com valores de 1 a 7.

1. Defina um objeto de fonte de dados do SQL Server, especificando uma tabela para conter os dados e a conexão ao servidor remoto.
  
    ```R
    sqlServerAirDemo <- RxSqlServerData(table = "AirDemoSmallTest", connectionString = sqlConnString)
    ```
  
2. Como precaução, incluem uma etapa que verifica se uma tabela com o mesmo nome já existe e exclua a tabela se ela existir. Uma tabela existente de mesmo nome impede que um novo do que está sendo criado.
  
    ```R
    if (rxSqlServerTableExists("AirDemoSmallTest",  connectionString = sqlConnString))  rxSqlServerDropTable("AirDemoSmallTest",  connectionString = sqlConnString)
    ```
  
3. Carregar os dados na tabela usando **rxDataStep**. Essa função move dados entre dois já definir fontes de dados e, opcionalmente, podem transformar os dados de caminho.
  
    ```R
    rxDataStep(inData = xdfAirDemo, outFile = sqlServerAirDemo,
        transforms = list( DayOfWeek = as.integer(DayOfWeek),
        rowNum = .rxStartRow : (.rxStartRow + .rxNumRows - 1) ),
        overwrite = TRUE )
    ```
  
    Essa é uma tabela bastante grande, portanto, aguarde até que você verá uma mensagem de status final como este: *Linhas lidas: 200000, total de linhas processadas: 600000*.
     
## <a name="load-data-from-a-sql-table"></a>Carregar dados de uma tabela SQL

Depois que os dados existem na tabela, você pode carregá-lo usando uma consulta SQL simples. 

1. Crie uma nova fonte de dados do SQL Server. A entrada é uma consulta à nova tabela que você acabou de criar e carregado com dados. Essa definição adiciona níveis de fator para a *DayOfWeek* coluna, usando o *colInfo* argumento **RxSqlServerData**.
  
    ```R
    sqlServerAirDemo2 <- RxSqlServerData(
        sqlQuery = "SELECT * FROM AirDemoSmallTest",
        connectionString = sqlConnString,
        rowsPerRead = 50000,
        colInfo = list(DayOfWeek = list(type = "factor",  levels = as.character(1:7))))
    ```
  
2. Chame **rxSummary** mais uma vez para examinar um resumo dos dados em sua consulta.
  
    ```R
    rxSummary(~., data = sqlServerAirDemo2)
    ```

## <a name="next-steps"></a>Próximas etapas

> [!div class="nextstepaction"]
> [Executar análise de agrupamento usando rxDataStep](../../advanced-analytics/tutorials/deepdive-perform-chunking-analysis-using-rxdatastep.md)