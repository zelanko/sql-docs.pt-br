---
title: Criar tabela usando rxDataStep
description: 'Tutorial 11 do RevoScaleR: Como criar uma tabela do SQL Server usando a linguagem R no SQL Server.'
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/27/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 99f693210b567523b74f851d1db68470cae2891d
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2020
ms.locfileid: "74947236"
---
# <a name="create-new-sql-server-table-using-rxdatastep-sql-server-and-revoscaler-tutorial"></a>Criar tabela do SQL Server usando rxDataStep (tutorial do SQL Server e do RevoScaleR)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Este é o tutorial 11 da [série de tutoriais do RevoScaleR](deepdive-data-science-deep-dive-using-the-revoscaler-packages.md) sobre como usar as [funções do RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) com o SQL Server.

Neste tutorial, você aprenderá a mover dados entre os quadros de dados na memória, o contexto do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e os arquivos locais.

> [!NOTE]
> Este tutorial usa um conjunto de dados diferente. O conjunto de dados de Atrasos em Companhias Aéreas é um conjunto de dados público que é amplamente usado para experiências de aprendizado de máquina. Os arquivos de dados usados neste exemplo estão disponíveis no mesmo diretório que outros exemplos de produto.

## <a name="load-data-from-a-local-xdf-file"></a>Carregar dados de um arquivo XDF local

Na primeira metade desta série de tutoriais, você usou a função **RxTextData** para importar dados no R de um arquivo de texto e usou a função **RxDataStep** para mover os dados para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].

Este tutorial usa uma abordagem diferente e os dados de um arquivo salvo no [formato XDF](https://en.wikipedia.org/wiki/Extensible_Data_Format). Depois de fazer algumas transformações simples nos dados usando o arquivo XDF, salve os dados transformados em uma nova tabela [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].

**O que é XDF?**

O formato XDF é um padrão de XML desenvolvido para dados de grande dimensão e é o formato de arquivo nativo usado pelo [Machine Learning Server](https://docs.microsoft.com/machine-learning-server/r/concept-what-is-xdf). Trata-se de um formato de arquivo binário com uma interface de R que otimiza a análise e o processamento de linhas e colunas.  Você pode usá-lo para mover dados e armazenar subconjuntos de dados que são úteis para análise.

1. Defina o contexto de computação como a estação de trabalho local. **Permissões de DDL necessárias para esta etapa.**

    ```R
    rxSetComputeContext("local")
    ```
  
2. Defina um novo objeto de fonte de dados usando a função **RxXdfData** . Para definir uma fonte de dados XDF, especifique o caminho para o arquivo de dados.  

    Você poderia especificar o caminho para o arquivo usando uma variável de texto. No entanto, nesse caso, há um atalho útil que deve usar a função **rxGetOption** e obter o arquivo (AirlineDemoSmall.xdf) do diretório de dados de exemplo.
  
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

## <a name="move-contents-to-sql-server"></a>Mover conteúdo para o SQL Server

Com a fonte de dados XDF criada na sessão do R local, agora você pode mover esses dados para uma tabela de banco de dados, armazenando *DayOfWeek* como um inteiro com valores de 1 a 7.

1. Defina um objeto de fonte de dados do SQL Server especificando uma tabela para conter os dados e a conexão com o servidor remoto.
  
    ```R
    sqlServerAirDemo <- RxSqlServerData(table = "AirDemoSmallTest", connectionString = sqlConnString)
    ```
  
2. Como precaução, inclua uma etapa que verifique se uma tabela com o mesmo nome já existe e a exclua se ela existir. Uma tabela existente com os mesmos nomes impede que um seja criado.
  
    ```R
    if (rxSqlServerTableExists("AirDemoSmallTest",  connectionString = sqlConnString))  rxSqlServerDropTable("AirDemoSmallTest",  connectionString = sqlConnString)
    ```
  
3. Carregue os dados na tabela usando **rxDataStep**. Essa função move os dados entre duas fontes de dados já definidas e pode opcionalmente transformar os dados em rota.
  
    ```R
    rxDataStep(inData = xdfAirDemo, outFile = sqlServerAirDemo,
        transforms = list( DayOfWeek = as.integer(DayOfWeek),
        rowNum = .rxStartRow : (.rxStartRow + .rxNumRows - 1) ),
        overwrite = TRUE )
    ```
  
    Essa é uma tabela muito grande; portanto, aguarde até ver uma mensagem de status final como esta: *Linhas lidas: 200000, Total de linhas processadas: 600000*.
     
## <a name="load-data-from-a-sql-table"></a>Carregar dados de uma tabela SQL

Depois que os dados existirem na tabela, você poderá carregá-los usando uma consulta SQL simples. 

1. Crie uma fonte de dados do SQL Server. A entrada é uma consulta na tabela recém-criada e carregada com os dados. Essa definição adiciona níveis de fator para a coluna *DayOfWeek*, usando o argumento *colInfo* para **RxSqlServerData**.
  
    ```R
    sqlServerAirDemo2 <- RxSqlServerData(
        sqlQuery = "SELECT * FROM AirDemoSmallTest",
        connectionString = sqlConnString,
        rowsPerRead = 50000,
        colInfo = list(DayOfWeek = list(type = "factor",  levels = as.character(1:7))))
    ```
  
2. Chame **rxSummary** mais uma vez para examinar um resumo dos dados na consulta.
  
    ```R
    rxSummary(~., data = sqlServerAirDemo2)
    ```

## <a name="next-steps"></a>Próximas etapas

> [!div class="nextstepaction"]
> [Executar análise de agrupamento usando rxDataStep](../../advanced-analytics/tutorials/deepdive-perform-chunking-analysis-using-rxdatastep.md)