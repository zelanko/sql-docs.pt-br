---
title: Criar nova tabela do SQL Server usando rxDataStep | Microsoft Docs
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
ms.assetid: 98cead96-6de7-4edf-98b9-a1efb09297b9
caps.latest.revision: "19"
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: c37cb44bdf2cc30e826ced8e06d47ec64c80f1b1
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2017
---
# <a name="create-new-sql-server-table-using-rxdatastep"></a>Criar nova tabela do SQL Server usando rxDataStep

Nesta lição, você aprenderá a mover dados entre os quadros de dados na memória, o contexto do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e os arquivos locais.

> [!NOTE]
> Nesta lição, você usará um conjunto de dados diferente. O conjunto de dados aérea atrasos é um conjunto de dados público que é amplamente usado para experiências de aprendizado de máquina. Se você estiver apenas começando a usar o R, será útil ter esse conjunto de dados para testes, pois ele será usado em vários exemplos de produtos para [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] que foram publicados com [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Os arquivos de dados de que você precisará para este exemplo estão disponíveis no mesmo diretório que outras amostras de produto.

## <a name="create-sql-server-table-from-local-data"></a>Criar tabela do SQL Server com base em dados locais

A primeira parte deste tutorial, você usou o **RxTextData** de função para importar dados para R de um arquivo de texto e, em seguida, é usado o **RxDataStep** função mover os dados em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].

Nesta lição, você usará uma abordagem diferente e obterá dados de um arquivo salvo no [formato XDF](https://en.wikipedia.org/wiki/Extensible_Data_Format). O formato XDF é um padrão de XML desenvolvido para dados de grande dimensão. Trata-se de um formato de arquivo binário com uma interface de R que otimiza a análise e o processamento de linhas e colunas.  Você pode usá-lo para mover dados e armazenar subconjuntos de dados que são úteis para análise.

Depois de fazer algumas transformações simples nos dados usando o arquivo XDF, você salvará os dados transformados em uma nova tabela [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .

> [!NOTE]
> Você precisará de permissões de DDL para esta etapa.

1. Defina o contexto de computação como a estação de trabalho local.
  
    ```R
    rxSetComputeContext("local")
    ```
  
2. Defina um novo objeto de fonte de dados usando a função **RxXdfData** . Para uma fonte de dados XDF, você apenas especifica o caminho para o arquivo de dados.  Você pode especificar o caminho para o arquivo usando uma variável de texto, mas nesse caso, há um atalho prático, porque o arquivo de dados de exemplo (AirlineDemoSmall.xdf) está no diretório retornado pela função rxGetOption.
  
    ```R
    xdfAirDemo <- RxXdfData(file.path(rxGetOption("sampleDataDir"),  "AirlineDemoSmall.xdf"))
    ```

3. Chamada à função rxGetVarInfo nos dados na memória para exibir um resumo do conjunto de dados.
  
    ```R
    rxGetVarInfo(xdfAirDemo)
    ```

**Resultados**

*Var 1: ArrDelay, Type: integer, Low/High: (-86, 1490)*

*Var 2: CRSDepTime, Type: numeric, Storage: float32, Low/High: (0.0167, 23.9833)*

*Var 3: DayOfWeek 7 factor levels: Monday Tuesday Wednesday Thursday Friday Saturday Sunday*

> [!NOTE]
> 
> Você notou que você não precisa chamar outras funções para carregar os dados no arquivo XDF e poderia chamar à função rxGetVarInfo nos dados imediatamente? Isso ocorre porque XDF é o método de armazenamento provisório padrão para RevoScaleR. Para obter mais informações sobre arquivos XDF, consulte [criar um XDF](https://msdn.microsoft.com/microsoft-r/scaler-data-xdf).
  
4. Agora, você colocará esses dados em uma tabela [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , armazenando _DayOfWeek_ como um inteiro com valores de 1 a 7.
  
    Para fazer isso, primeiro defina uma fonte de dados do SQL Server.
  
    ```R
    sqlServerAirDemo <- RxSqlServerData(table = "AirDemoSmallTest", connectionString = sqlConnString)
    ```
  
5. Verifique se uma tabela com o mesmo nome já existe e exclua-a se existir.
  
    ```R
    if (rxSqlServerTableExists("AirDemoSmallTest",  connectionString = sqlConnString))  rxSqlServerDropTable("AirDemoSmallTest",  connectionString = sqlConnString)
    ```
  
6. Crie a tabela e carregue os dados usando **rxDataStep**. Essa função move dados entre duas já definir fontes de dados e podem transformar os caminho de dados.
  
    ```R
    rxDataStep(inData = xdfAirDemo, outFile = sqlServerAirDemo,
            transforms = list( DayOfWeek = as.integer(DayOfWeek),
            rowNum = .rxStartRow : (.rxStartRow + .rxNumRows - 1) ),
            overwrite = TRUE )
    ```
  
    Essa é uma tabela bastante grande, então espere até ver a mensagem de status final: *Linhas lidas: 200.000. Total de linhas processadas: 600.000*.
     
7. Defina o contexto de computação de volta para o computador do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .

    ```R
    rxSetComputeContext(sqlCompute)
    ```
  
8. Crie uma nova fonte de dados do SQL Server, usando uma consulta SQL simples na nova tabela. Essa definição adiciona níveis de fator para a coluna *DayOfWeek*, usando o argumento *colInfo* para RxSqlServerData.
  
    ```R
    SqlServerAirDemo <- RxSqlServerData(
        sqlQuery = "SELECT * FROM AirDemoSmallTest",
        connectionString = sqlConnString,
        rowsPerRead = 50000,
        colInfo = list(DayOfWeek = list(type = "factor",  levels = as.character(1:7))))
    ```
  
9. Chame rxSummary mais uma vez para exibir um resumo dos dados em sua consulta.
  
    ```R
    rxSummary(~., data = sqlServerAirDemo)
    ```

## <a name="next-step"></a>Próxima etapa

[Executar análise de agrupamento usando rxDataStep](../../advanced-analytics/tutorials/deepdive-perform-chunking-analysis-using-rxdatastep.md)

## <a name="previous-step"></a>Etapa anterior

[Carregar dados em memória usando rxImport](../../advanced-analytics/tutorials/deepdive-load-data-into-memory-using-rximport.md)


