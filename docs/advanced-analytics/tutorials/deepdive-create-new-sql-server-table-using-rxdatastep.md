---
title: Criar nova tabela do SQL Server usando rxDataStep (SQL e R mergulho profundo) | Microsoft Docs
ms.custom: 
ms.date: 12/14/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: 
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: tutorial
applies_to:
- SQL Server 2016
- SQL Server 2017
dev_langs:
- R
ms.assetid: 98cead96-6de7-4edf-98b9-a1efb09297b9
caps.latest.revision: 
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: Inactive
ms.openlocfilehash: b64a62a9bc5e9b7c105bae1f6a8dda4a60e641c4
ms.sourcegitcommit: 99102cdc867a7bdc0ff45e8b9ee72d0daade1fd3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/11/2018
---
# <a name="create-new-sql-server-table-using-rxdatastep-sql-and-r-deep-dive"></a>Criar nova tabela do SQL Server usando rxDataStep (SQL e R mergulho profundo)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Este artigo faz parte do tutorial mergulho profundo de ciência de dados, como usar [RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) com o SQL Server.

Nesta lição, você aprenderá a mover dados entre os quadros de dados na memória, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] contexto e arquivos locais.

> [!NOTE]
> Esta lição usa um conjunto de dados diferente. O conjunto de dados aérea atrasos é um conjunto de dados público que é amplamente usado para experiências de aprendizado de máquina. Os arquivos de dados usados neste exemplo estão disponíveis no mesmo diretório que outros exemplos de produto.

## <a name="create-sql-server-table-from-local-data"></a>Criar a tabela do SQL Server de dados locais

Na primeira metade deste tutorial, você usou o **RxTextData** de função para importar dados para R de um arquivo de texto e, em seguida, é usado o **RxDataStep** função mover os dados em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].

Nesta lição adota uma abordagem diferente e usa dados de um arquivo salvo no [formato XDF](https://en.wikipedia.org/wiki/Extensible_Data_Format). Depois de fazer algumas transformações leves nos dados usando o arquivo XDF, você deve salvar os dados transformados em um novo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tabela.

**O que é XDF?**

O formato XDF é um padrão XML desenvolvido para dados altamente dimensional e é o formato de arquivo nativo usado pelo [Server de aprendizado de máquina](https://docs.microsoft.com/machine-learning-server/r/concept-what-is-xdf). Trata-se de um formato de arquivo binário com uma interface de R que otimiza a análise e o processamento de linhas e colunas.  Você pode usá-lo para mover dados e armazenar subconjuntos de dados que são úteis para análise.

1. Defina o contexto de computação como a estação de trabalho local. **São necessárias permissões de DDL para esta etapa.**

  
    ```R
    rxSetComputeContext("local")
    ```
  
2. Defina um novo objeto de fonte de dados usando a função **RxXdfData** . Para definir uma fonte de dados XDF, especifique o caminho para o arquivo de dados.  

    Você pode especificar o caminho para o arquivo usando uma variável de texto. No entanto, nesse caso, há um atalho prático, é usar o **rxGetOption** de função e obter o arquivo (AirlineDemoSmall.xdf) do diretório de dados de exemplo.
  
    ```R
    xdfAirDemo <- RxXdfData(file.path(rxGetOption("sampleDataDir"),  "AirlineDemoSmall.xdf"))
    ```

3. Chame [rxGetVarInfo](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxgetvarinfoxdf) nos dados na memória para exibir um resumo do conjunto de dados.
  
    ```R
    rxGetVarInfo(xdfAirDemo)
    ```

**Resultados**

*Var 1: ArrDelay, Type: integer, Low/High: (-86, 1490)*

*Var 2: CRSDepTime, Type: numeric, Storage: float32, Low/High: (0.0167, 23.9833)*

*Var 3: DayOfWeek 7 factor levels: Monday Tuesday Wednesday Thursday Friday Saturday Sunday*

> [!NOTE]
> 
> Você notou que não precisava chamar nenhuma outra função para carregar os dados no arquivo XDF e poderia chamar **rxGetVarInfo** nos dados imediatamente? Isso ocorre porque XDF é o método de armazenamento provisório padrão para RevoScaleR. Além dos arquivos XDF o **à função rxGetVarInfo** função agora dá suporte a vários tipos de origem.
  
4. Colocar dados em um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de tabela, armazenando _DayOfWeek_ como um inteiro com valores de 1 a 7.
  
    Para fazer isso, primeiro defina uma fonte de dados do SQL Server.
  
    ```R
    sqlServerAirDemo <- RxSqlServerData(table = "AirDemoSmallTest", connectionString = sqlConnString)
    ```
  
5. Verifique se uma tabela com o mesmo nome já existe e exclua-a se existir.
  
    ```R
    if (rxSqlServerTableExists("AirDemoSmallTest",  connectionString = sqlConnString))  rxSqlServerDropTable("AirDemoSmallTest",  connectionString = sqlConnString)
    ```
  
6. Crie a tabela e carregue os dados usando **rxDataStep**. Essa função move dados entre duas já definir fontes de dados e, opcionalmente, podem transformar os dados de caminho.
  
    ```R
    rxDataStep(inData = xdfAirDemo, outFile = sqlServerAirDemo,
            transforms = list( DayOfWeek = as.integer(DayOfWeek),
            rowNum = .rxStartRow : (.rxStartRow + .rxNumRows - 1) ),
            overwrite = TRUE )
    ```
  
    Essa é uma tabela muito grande, portanto Aguarde até que você verá uma mensagem de status final como este: *linhas lidas: 200000, linhas de Total processadas: 600000*.
     
7. Defina o contexto de computação de volta para o computador do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .

    ```R
    rxSetComputeContext(sqlCompute)
    ```
  
8. Crie uma nova fonte de dados do SQL Server, usando uma consulta SQL simples na nova tabela. Esta definição adiciona níveis fator para o *DayOfWeek* coluna, usando o *colInfo* argumento **RxSqlServerData**.
  
    ```R
    SqlServerAirDemo <- RxSqlServerData(
        sqlQuery = "SELECT * FROM AirDemoSmallTest",
        connectionString = sqlConnString,
        rowsPerRead = 50000,
        colInfo = list(DayOfWeek = list(type = "factor",  levels = as.character(1:7))))
    ```
  
9. Chamar **rxSummary** mais uma vez para exibir um resumo dos dados em sua consulta.
  
    ```R
    rxSummary(~., data = sqlServerAirDemo)
    ```

## <a name="next-step"></a>Próxima etapa

[Executar análise de agrupamento usando rxDataStep](../../advanced-analytics/tutorials/deepdive-perform-chunking-analysis-using-rxdatastep.md)

## <a name="previous-step"></a>Etapa anterior

[Carregar dados na memória usando rxImport](../../advanced-analytics/tutorials/deepdive-load-data-into-memory-using-rximport.md)
