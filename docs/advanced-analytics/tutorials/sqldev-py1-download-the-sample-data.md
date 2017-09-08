---
title: 'Etapa 1: Baixar os dados de exemplo | Microsoft Docs'
ms.custom: 
ms.date: 05/25/2017
ms.prod: sql-server-2017
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server 2017
dev_langs:
- Python
- TSQL
ms.assetid: 
caps.latest.revision: 2
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 147860e9af8cce86d1a7ccbd3e53f20d240fcd49
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="step-1-download-the-sample-data"></a>Etapa 1: Baixar os dados de exemplo

Nesta etapa, você baixará o conjunto de dados de exemplo e os scripts. Os dados e os arquivos de script são compartilhados no GitHub, mas o script do PowerShell baixará os arquivos de dados e de script em um diretório local de sua escolha.

## <a name="download-the-data-and-scripts"></a>Baixar os dados e os scripts

1. Abra um console de comando do Windows PowerShell.

    Use a opção **executar como administrador**, se os privilégios administrativos são necessários para criar o diretório de destino ou para gravar arquivos de destino especificado.

2. Execute os comandos do PowerShell a seguir, alterando o valor do parâmetro *DestDir* para um diretório local.  O padrão que usamos aqui é **TempPythonSQL**.

    ```
    $source = 'https://raw.githubusercontent.com/Azure/Azure-MachineLearning-DataScience/master/Misc/PythonSQL/Download_Scripts_SQL_Walkthrough.ps1'
    $ps1_dest = "$pwd\Download_Scripts_SQL_Walkthrough.ps1"
    $wc = New-Object System.Net.WebClient
    $wc.DownloadFile($source, $ps1_dest)
    .\Download_Scripts_SQL_Walkthrough.ps1 –DestDir 'C:\tempPythonSQL'
    ```
    
    Se a pasta especificada em *DestDir* não existir, ela será criada pelo script do PowerShell.
    
    Se você receber um erro, você pode definir temporariamente a política de execução de scripts do PowerShell para **irrestrito** somente para este passo a passo, usando o **Bypass** argumento e as alterações atuais de escopo sessão. A execução desse comando não resulta em uma alteração de configuração.
    
    `Set\-ExecutionPolicy Bypass \-Scope Process`

3. Dependendo da conexão com a Internet, o download poderá demorar um pouco. Quando todos os arquivos forem baixados, o script do PowerShell será aberto na pasta especificada por  *DestDir*. No prompt de comando do PowerShell, execute o comando a seguir e examine os arquivos baixados.

    ```
    ls
    ```
**Resultados:**

![lista de arquivos baixados pelo script do PowerShell](media/sqldev-python-filelist.png "lista de arquivos baixados pelo script do PowerShell")

## <a name="next-step"></a>Próxima etapa

[Etapa 2: Importar dados para o SQL Server usando o PowerShell](sqldev-py2-import-data-to-sql-server-using-powershell.md)

## <a name="previous-step"></a>Etapa anterior

[No banco de dados análise do Python para o desenvolvedor do SQL](sqldev-in-database-python-for-sql-developers.md)

## <a name="see-also"></a>Consulte também

[Serviços de aprendizado de máquina com Python](../python/sql-server-python-services.md)



