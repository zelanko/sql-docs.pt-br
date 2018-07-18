---
title: Dados de exemplo de Download de lição 1 e scripts para embedded R (aprendizado de máquina do SQL Server) | Microsoft Docs
description: Tutorial que mostra como incorporar o R no SQL Server procedimentos armazenados e funções T-SQL
ms.prod: sql
ms.technology: machine-learning
ms.date: 06/07/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 74a60a95da4fb701f3862c36e35a4bada6ef933b
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2018
ms.locfileid: "38030374"
---
# <a name="lesson-1-download-data-and-scripts"></a>Lição 1: Baixar os dados e scripts
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Este artigo faz parte de um tutorial para desenvolvedores SQL sobre como usar o R no SQL Server.

Nesta etapa, você baixará o conjunto de dados de exemplo e o [!INCLUDE[tsql](../../includes/tsql-md.md)] arquivos de script que são usados neste tutorial. Os dados e os arquivos de script são compartilhados no GitHub, mas o script do PowerShell baixará os arquivos de dados e de script para um diretório local de sua escolha.

## <a name="download-tutorial-files-from-github"></a>Baixe os arquivos do tutorial do Github

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

[Análise de R incorporado para desenvolvedores do SQL](../tutorials/sqldev-in-database-r-for-sql-developers.md)
