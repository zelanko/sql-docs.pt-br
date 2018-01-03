---
title: "Lição 1: Baixar os dados de exemplo | Microsoft Docs"
ms.custom: 
ms.date: 07/26/2016
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: 
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: tutorial
applies_to: SQL Server 2016
dev_langs:
- R
- TSQL
ms.assetid: 32a5d5ad-c58a-4669-a90d-ef296b48fcd8
caps.latest.revision: "10"
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 9a5c5a5ab4bfe841ec7e06ffd44fef9ca9c15e85
ms.sourcegitcommit: 23433249be7ee3502c5b4d442179ea47305ceeea
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/20/2017
---
# <a name="lesson-1-download-the-sample-data"></a>Lição 1: Baixar os dados de exemplo

Este artigo faz parte de um tutorial para desenvolvedores em SQL sobre como usar o R no SQL Server.

Nesta etapa, você baixará o conjunto de dados de exemplo e o [!INCLUDE[tsql](../../includes/tsql-md.md)] script arquivos que são usados neste tutorial. Os dados e os arquivos de script são compartilhados no GitHub, mas o script do PowerShell baixará os arquivos de dados e o script para um diretório local de sua escolha.

## <a name="download-the-data-and-scripts"></a>Baixar os dados e scripts

1.  Abra um console de comando do Windows PowerShell.
  
    Use a opção **Executar como Administrador**se os privilégios administrativos forem necessários para criar o diretório de destino ou para gravar arquivos no destino especificado.
  
2.  Execute os comandos do PowerShell a seguir, alterando o valor do parâmetro *DestDir* para um diretório local.  O padrão que usamos aqui é **TempRSQL**.
  
    ```ps
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
  
3.  Quando todos os arquivos forem baixados, o script do PowerShell será aberto na pasta especificada por  *DestDir*. No prompt de comando do PowerShell, execute o comando a seguir e examine os arquivos baixados.
  
    ```
    ls
    ```
  
    **Resultados:**
  
    ![lista de arquivos baixados pelo script do PowerShell](media/rsql-devtut-filelist.png "lista de arquivos baixados pelo script do PowerShell")
  
## <a name="next-lesson"></a>Próxima lição

[Lição 2: Importar dados para o SQL Server usando o PowerShell](../r/sqldev-import-data-to-sql-server-using-powershell.md)

## <a name="previous-lesson"></a>Lição anterior

[Análise de R no banco de dados para desenvolvedores em SQL](../tutorials/sqldev-in-database-r-for-sql-developers.md)
