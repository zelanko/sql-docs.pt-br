---
title: "Etapa 1: Baixar os dados de exemplo (Tutorial de an&#225;lise avan&#231;ada no banco de dados) | Microsoft Docs"
ms.custom: ""
ms.date: "04/19/2016"
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
  - "TSQL"
ms.assetid: 32a5d5ad-c58a-4669-a90d-ef296b48fcd8
caps.latest.revision: 10
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 10
---
# Etapa 1: Baixar os dados de exemplo (Tutorial de an&#225;lise avan&#231;ada no banco de dados)
Nesta etapa, você baixará o conjunto de dados de exemplo e os arquivos de script do [!INCLUDE[tsql](../../includes/tsql-md.md)] que são usados neste passo a passo. Os dados e os arquivos de script são compartilhados no GitHub, mas o script do PowerShell baixará os arquivos de dados e de script em um diretório local de sua escolha.  
  
## Baixar os dados e os scripts  
  
1.  Abra um console de comando do Windows PowerShell.  
  
    Use a opção **Executar como Administrador** se os privilégios administrativos forem necessários para criar o diretório de destino ou para gravar arquivos no destino especificado.  
  
2.  Execute os comandos do PowerShell a seguir, alterando o valor do parâmetro *DestDir* para um diretório local.  O padrão que usamos aqui é **TempRSQL**.  
  
    ```  
    $source = ‘https://raw.githubusercontent.com/Azure/Azure-MachineLearning-DataScience/master/Misc/RSQL/Download_Scripts_SQL_Walkthrough.ps1’  
    $ps1_dest = “$pwd\Download_Scripts_SQL_Walkthrough.ps1”  
    $wc = New-Object System.Net.WebClient  
    $wc.DownloadFile($source, $ps1_dest)  
    .\Download_Scripts_SQL_Walkthrough.ps1 –DestDir ‘C:\tempRSQL’  
  
    ```  
  
    Se a pasta especificada em *DestDir* não existir, ela será criada pelo script do PowerShell.  
  
    > [!TIP]  
    > Se você receber um erro, poderá definir temporariamente a política de execução de scripts do PowerShell como **irrestrito** apenas para este passo a passo, usando o argumento Bypass e incluindo as alterações no escopo da sessão atual.  
    >   
    >````  
    > Set\-ExecutionPolicy Bypass \-Scope Process  
    >````   
    > A execução desse comando não resulta em uma alteração de configuração.  
  
    Dependendo da conexão com a Internet, o download poderá demorar um pouco.  
  
3.  Quando todos os arquivos forem baixados, o script do PowerShell será aberto na pasta especificada por *DestDir*. No prompt de comando do PowerShell, execute o comando a seguir e examine os arquivos baixados.  
  
    ```  
    ls  
    ```  
  
    **Resultados:**  
  
    ![list of files downloaded by PowerShell script](../../advanced-analytics/r-services/media/rsql-devtut-filelist.PNG "list of files downloaded by PowerShell script")  
  
## Próxima etapa  
[Etapa 2: Importar dados para o SQL Server usando o PowerShell](../../advanced-analytics/r-services/step-2-import-data-to-sql-server-using-powershell.md)  
  
## Etapa anterior  
[Análise avançada no banco de dados para desenvolvedores do SQL &#40;Tutorial&#41;](../../advanced-analytics/r-services/in-database-advanced-analytics-for-sql-developers-tutorial.md)  
  
## Consulte também  
[Tutoriais do SQL Server R Services](../../advanced-analytics/r-services/sql-server-r-services-tutorials.md)  
  
  
  
