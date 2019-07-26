---
title: Criar nova tabela de SQL Server usando RevoScaleR rxDataStep
description: Tutorial explicativo sobre como criar uma tabela de SQL Server usando a linguagem R em SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/27/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.openlocfilehash: b88de049cb73cf8539067e708963bd82ee7086ae
ms.sourcegitcommit: 9062c5e97c4e4af0bbe5be6637cc3872cd1b2320
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/24/2019
ms.locfileid: "68469825"
---
# <a name="create-new-sql-server-table-using-rxdatastep-sql-server-and-revoscaler-tutorial"></a>Criar nova tabela de SQL Server usando o rxDataStep (tutorial SQL Server e RevoScaleR)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Esta lição faz parte do [tutorial do RevoScaleR](deepdive-data-science-deep-dive-using-the-revoscaler-packages.md) sobre como usar as [funções do RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) com SQL Server.

Nesta lição, você aprenderá a mover dados entre quadros de dados na memória, o contexto [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e os arquivos locais.

> [!NOTE]
> Esta lição usa um conjunto de dados diferente. O conjunto de informações de atrasos de viagens é um conjunto de informações público que é amplamente usado para experimentos de aprendizado de máquina. Os arquivos de dados usados neste exemplo estão disponíveis no mesmo diretório que outros exemplos de produtos.

## <a name="load-data-from-a-local-xdf-file"></a>Carregar dados de um arquivo XDF local

Na primeira metade deste tutorial, você usou a função **RxTextData** para importar dados para o R de um arquivo de texto e, em seguida, usou a função **RxDataStep** para mover [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]os dados para o.

Esta lição usa uma abordagem diferente e usa dados de um arquivo salvo no [formato Xdf](https://en.wikipedia.org/wiki/Extensible_Data_Format). Depois de fazer algumas transformações leves nos dados usando o arquivo Xdf, você salva os dados transformados em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] uma nova tabela.

**O que é o XDF?**

O formato XDF é um padrão XML desenvolvido para dados altamente dimensionais e é o formato de arquivo nativo usado pelo [Machine Learning Server](https://docs.microsoft.com/machine-learning-server/r/concept-what-is-xdf). Trata-se de um formato de arquivo binário com uma interface de R que otimiza a análise e o processamento de linhas e colunas.  Você pode usá-lo para mover dados e armazenar subconjuntos de dados que são úteis para análise.

1. Defina o contexto de computação como a estação de trabalho local. **As permissões DDL são necessárias para esta etapa.**

    ```R
    rxSetComputeContext("local")
    ```
  
2. Defina um novo objeto de fonte de dados usando a função **RxXdfData** . Para definir uma fonte de dados XDF, especifique o caminho para o arquivo de dados.  

    Você pode especificar o caminho para o arquivo usando uma variável de texto. No entanto, nesse caso, há um atalho útil, que é usar a função **rxGetOption** e obter o arquivo (AirlineDemoSmall. Xdf) do diretório de dados de exemplo.
  
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
> Você notou que não precisava chamar nenhuma outra função para carregar os dados no arquivo XDF e poderia chamar **rxGetVarInfo** nos dados imediatamente? Isso ocorre porque XDF é o método de armazenamento provisório padrão para **RevoScaleR**. Além dos arquivos XDF, a função **rxGetVarInfo** agora dá suporte a vários tipos de origem.

## <a name="move-contents-to-sql-server"></a>Mover conteúdo para SQL Server

Com a fonte de dados XDF criada na sessão do R local, agora você pode mover esses dados para uma tabela de banco de dado, armazenando *DayOfWeek* como um inteiro com valores de 1 a 7.

1. Defina um objeto de fonte de dados SQL Server, especificando uma tabela para conter os dados e a conexão com o servidor remoto.
  
    ```R
    sqlServerAirDemo <- RxSqlServerData(table = "AirDemoSmallTest", connectionString = sqlConnString)
    ```
  
2. Como precaução, inclua uma etapa que verifique se já existe uma tabela com o mesmo nome e exclua a tabela, se ela existir. Uma tabela existente com os mesmos nomes impede que um novo seja criado.
  
    ```R
    if (rxSqlServerTableExists("AirDemoSmallTest",  connectionString = sqlConnString))  rxSqlServerDropTable("AirDemoSmallTest",  connectionString = sqlConnString)
    ```
  
3. Carregue os dados na tabela usando **rxDataStep**. Essa função move dados entre duas fontes de dados já definidas e, opcionalmente, pode transformar os dados em rota.
  
    ```R
    rxDataStep(inData = xdfAirDemo, outFile = sqlServerAirDemo,
        transforms = list( DayOfWeek = as.integer(DayOfWeek),
        rowNum = .rxStartRow : (.rxStartRow + .rxNumRows - 1) ),
        overwrite = TRUE )
    ```
  
    Essa é uma tabela bastante grande, portanto, aguarde até que você veja uma mensagem de status final como esta: *Linhas lidas: 200000, total de linhas processadas: 600000*.
     
## <a name="load-data-from-a-sql-table"></a>Carregar dados de uma tabela SQL

Depois que os dados existirem na tabela, você poderá carregá-los usando uma consulta SQL simples. 

1. Crie uma nova fonte de dados SQL Server. A entrada é uma consulta na nova tabela que você acabou de criar e carregar com os dados. Essa definição adiciona níveis de fator para a coluna *DayOfWeek* , usando o argumento *colInfo* para **RxSqlServerData**.
  
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