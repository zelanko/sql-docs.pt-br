---
title: 'Etapa 1: Baixar os dados de exemplo | Microsoft Docs'
ms.custom: 
ms.date: 10/17/2017
ms.prod: sql-server-2017
ms.reviewer: 
ms.suite: 
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
applies_to: SQL Server 2017
dev_langs:
- Python
- TSQL
ms.assetid: 
caps.latest.revision: "2"
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.openlocfilehash: b2ac1eeb53ba9f9a0dcbf86ee772db9c8b2d3553
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2017
---
# <a name="step-1-download-the-sample-data"></a>Etapa 1: Baixar os dados de exemplo

Este artigo faz parte de um tutorial, [análise Python no banco de dados para desenvolvedores em SQL](sqldev-in-database-python-for-sql-developers.md). 

Os dados e os scripts para este tutorial são compartilhados no Github. Nesta etapa, você pode usar um script do PowerShell para baixar os arquivos de dados e o script para um diretório local de sua escolha.

## <a name="run-the-script"></a>Execute o script

1. Abra um console de comando do Windows PowerShell.

    Use a opção **executar como administrador**, se os privilégios administrativos são necessários para criar o diretório de destino ou para gravar arquivos de destino especificado.

2. Execute os comandos do PowerShell a seguir, alterando o valor do parâmetro *DestDir* para um diretório local.  O padrão que usamos aqui é `C:\temp\pysql`.

    ```ps
    $source = 'https://raw.githubusercontent.com/Azure/Azure-MachineLearning-DataScience/master/Misc/PythonSQL/Download_Scripts_SQL_Walkthrough.ps1'
    $ps1_dest = "$pwd\Download_Scripts_SQL_Walkthrough.ps1"
    $wc = New-Object System.Net.WebClient
    $wc.DownloadFile($source, $ps1_dest)
    .\Download_Scripts_SQL_Walkthrough.ps1 –DestDir 'C:\temp\pysql'
    ```
    
    Se a pasta especificada em *DestDir* não existir, ela será criada pelo script do PowerShell.
    
    Se você receber um erro, a política de execução de scripts do PowerShell para definir temporariamente **irrestrito** para este passo a passo, usando o **Bypass** argumento e o escopo de alterações para a sessão atual. A execução desse comando não resulta em uma alteração de configuração.
    
    ```ps
    Set-ExecutionPolicy Bypass -Scope Process
    ```

3. Dependendo de sua conexão de internet, o download pode levar algum tempo. 

## <a name="view-the-results"></a>Exibir os resultados

Quando todos os arquivos forem baixados, o script do PowerShell será aberto na pasta especificada por  *DestDir*. 

+ No prompt de comando do PowerShell, execute o seguinte comando para listar os arquivos que foram baixados.

    ```ps
    ls
    ```

![lista de arquivos baixados pelo script do PowerShell](media/sqldev-python-filelist.png "lista de arquivos baixados pelo script do PowerShell")

## <a name="next-step"></a>Próxima etapa

[Etapa 2: Importar dados para o SQL Server usando o PowerShell](sqldev-py2-import-data-to-sql-server-using-powershell.md)

## <a name="previous-step"></a>Etapa anterior

[No banco de dados análise do Python para o desenvolvedor do SQL](sqldev-in-database-python-for-sql-developers.md)

## <a name="see-also"></a>Consulte também

[Serviços de aprendizado de máquina com Python](../python/sql-server-python-services.md)


