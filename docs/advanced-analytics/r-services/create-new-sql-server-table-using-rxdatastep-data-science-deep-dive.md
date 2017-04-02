---
title: "Criar nova tabela do SQL Server usando rxDataStep (Aprofundamento da ci&#234;ncia de dados) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
applies_to: 
  - "SQL Server 2016"
dev_langs: 
  - "R"
ms.assetid: 98cead96-6de7-4edf-98b9-a1efb09297b9
caps.latest.revision: 19
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
---
# Criar nova tabela do SQL Server usando rxDataStep (Aprofundamento da ci&#234;ncia de dados)
Nesta lição, você aprenderá a mover dados entre os quadros de dados na memória, o contexto do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e os arquivos locais.  
  
> [!NOTE]  
> Nesta lição, você usará um conjunto de dados diferente. O conjunto de dados de atraso de companhias aéreas é um conjunto de dados público que é amplamente usado para experiências de aprendizado de máquina. Se você estiver apenas começando a usar o R, será útil ter esse conjunto de dados para testes, pois ele será usado em vários exemplos de produtos para [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] que foram publicados com [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Os arquivos de dados de que você precisará para este exemplo estão disponíveis no mesmo diretório que outras amostras de produto.  
  
## Criar tabela do SQL Server com base em dados locais  
Na primeira lição deste tutorial, você usou a função *RxTextData* para importar dados no R de um arquivo de texto e usou a função *RxDataStep* para mover os dados para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
Nesta lição, você usará uma abordagem diferente e obterá dados de um arquivo salvo no [formato XDF](https://en.wikipedia.org/wiki/Extensible_Data_Format). O formato XDF é um padrão de XML desenvolvido para dados de grande dimensão. Trata-se de um formato de arquivo binário com uma interface de R que otimiza a análise e o processamento de linhas e colunas.  Você pode usá-lo para mover dados e armazenar subconjuntos de dados que são úteis para análise.
  
Depois de fazer algumas transformações simples nos dados usando o arquivo XDF, você salvará os dados transformados em uma nova tabela [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
> [!NOTE]  
> Você precisará de permissões de DDL para esta etapa.  
  
1.  Defina o contexto de computação como a estação de trabalho local.  
  
    ```R  
    rxSetComputeContext("local")   
    ```  
  
2.  Defina um novo objeto de fonte de dados usando a função *RxXdfData*. Para uma fonte de dados XDF, você apenas especifica o caminho para o arquivo de dados.  Você pode especificar o caminho para o arquivo usando uma variável de texto, mas nesse caso, há um atalho útil, pois o arquivo de dados de exemplo (AirlineDemoSmall.xdf) está no diretório retornado pela função *rxGetOption*.
  
    ```R  
    xdfAirDemo <- RxXdfData(file.path(rxGetOption("sampleDataDir"),  "AirlineDemoSmall.xdf"))   
    ```  
  
  
3.  Chame *rxGetVarInfo* nos dados na memória para exibir um resumo do conjunto de dados.  
  
    ```R  
    rxGetVarInfo(xdfAirDemo)    
    ```  
  
**Resultados**  
  
*Var 1: ArrDelay, Type: integer, Low/High: (-86, 1490)*   
*Var 2: CRSDepTime, Type: numeric, Storage: float32, Low/High: (0.0167, 23.9833)*   
*Var 3: DayOfWeek 7 factor levels: Monday Tuesday Wednesday Thursday Friday Saturday Sunday*  

> [!NOTE]
> 
> Você notou que não precisava chamar nenhuma outra função para carregar os dados no arquivo XDF e poderia chamar *rxGetVarInfo* nos dados imediatamente? Isso ocorre porque XDF é o método de armazenamento provisório padrão para RevoScaleR. Para obter mais informações sobre arquivos XDF, consulte o [Guia de Introdução ao ScaleR](https://msdn.microsoft.com/microsoft-r/scaler-user-guide-data-transform#using-the-data-step-to-create-an-xdf-file-from-a-data-frame) 
  
4.  Agora, você colocará esses dados em uma tabela [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], armazenando _DayOfWeek_ como um inteiro com valores de 1 a 7.  
  
    Para fazer isso, primeiro defina uma fonte de dados do SQL Server.  
  
    ```R  
    sqlServerAirDemo <- RxSqlServerData(table = "AirDemoSmallTest", connectionString = sqlConnString)   
    ```  
  
5.  Verifique se há uma tabela com o mesmo nome e exclua-a se ela existir.  
  
    ```R  
    if (rxSqlServerTableExists("AirDemoSmallTest",  connectionString = sqlConnString))  rxSqlServerDropTable("AirDemoSmallTest",  connectionString = sqlConnString)    
    ```  
  
6.  Crie a tabela e carregue os dados usando `rxDataStep`.  
  
    ```R  
    rxDataStep(inData = xdfAirDemo, outFile = sqlServerAirDemo,    
            transforms = list( DayOfWeek = as.integer(DayOfWeek),   
            rowNum = .rxStartRow : (.rxStartRow + .rxNumRows - 1) ),   
            overwrite = TRUE )    
    ```  
  
7.  Defina o contexto de computação de volta para o computador do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
    ```R  
    rxSetComputeContext(sqlCompute)  
    ```  
  
8.  Defina um subconjunto dos dados usando uma instrução SQL simples.  
  
    ```R    
    SqlServerAirDemo <- RxSqlServerData(  
        sqlQuery = "SELECT * FROM AirDemoSmallTest",      
        connectionString = sqlConnString,   
        rowsPerRead = 50000,      
        colInfo = list(DayOfWeek = list(type = "factor",  levels = as.character(1:7))))    
    ```  
  
9. Chame *rxSummary* para examinar um resumo dos dados na consulta.  
  
    ```R  
    rxSummary(~., data = sqlServerAirDemo)   
    ```  
  
## Próxima etapa  
[Executar análise de agrupamento usando rxDataStep &#40;Aprofundamento da ciência de dados&#41;](../../advanced-analytics/r-services/perform-chunking-analysis-using-rxdatastep-data-science-deep-dive.md)  
  
## Etapa anterior  
[Carregar dados na memória usando rxImport &#40;Aprofundamento da ciência de dados&#41;](../../advanced-analytics/r-services/load-data-into-memory-using-rximport-data-science-deep-dive.md)  
  
## Consulte também  
[Aprofundamento da ciência de dados: Usando os pacotes RevoScaleR](../../advanced-analytics/r-services/data-science-deep-dive-using-the-revoscaler-packages.md)  
  
  
  
