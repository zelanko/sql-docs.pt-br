---
title: Executar um pacote do SSIS no prompt de comando | Microsoft Docs
ms.date: 09/25/2017
ms.topic: article
ms.prod: sql-server-2017
ms.technology:
- integration-services
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.translationtype: MT
ms.sourcegitcommit: 656e62f36446db4ef5b232129130a0253d2aebdf
ms.openlocfilehash: a33b8518ec3284f5de73d38c87209057dc1c7487
ms.contentlocale: pt-br
ms.lasthandoff: 09/22/2017

---
# <a name="run-an-ssis-package-from-the-command-prompt-with-dtexecexe"></a>Executar um pacote do SSIS no prompt de comando com DTExec.exe
Este tutorial de início rápido demonstra como executar um pacote do SSIS no prompt de comando executando `DTExec.exe` com os parâmetros apropriados.

> [!NOTE]
> O método descrito neste artigo não foi testado com os pacotes implantados em um servidor de banco de dados SQL.

Para obter mais informações sobre `DTExec.exe`, consulte [utilitário dtexec](https://docs.microsoft.com/en-us/sql/integration-services/packages/dtexec-utility).

## <a name="run-a-package-with-dtexec"></a>Executar um pacote com dtexec

Se a pasta que contém `DTExec.exe` não está no seu `path` variável de ambiente, talvez você precise usar o `cd` comando para alterar para seu diretório. Para SQL Server 2017, essa pasta é normalmente `C:\Program Files (x86)\Microsoft SQL Server\140\DTS\Binn`.

Com os valores de parâmetro usados no exemplo a seguir, o programa é executado o pacote no caminho da pasta especificada no servidor do SSIS - ou seja, o servidor que hospeda o banco de dados do catálogo do SSIS (SSISDB). O `/Server` parâmetro fornece o nome do servidor. O programa se conectar como o usuário atual com a autenticação integrada do Windows. Para usar a autenticação do SQL, especifique o `/User` e `Password` parâmetros com valores apropriados.

1. Abra uma janela do prompt de comando.

2. Executar `DTExec.exe` e forneça valores pelo menos para o `ISServer` e `Server` parâmetros, conforme mostrado no exemplo a seguir:

    ```cmd
    dtexec /ISServer "\SSISDB\Project1Folder\Integration Services Project1\Package.dtsx" /Server "localhost"
    ```

## <a name="next-steps"></a>Próximas etapas
- Considere a possibilidade de outras maneiras de executar um pacote.
    - [Executar um pacote do SSIS com o SSMS](./ssis-quickstart-run-ssms.md)
    - [Executar um pacote do SSIS com Transact-SQL (SSMS)](./ssis-quickstart-run-tsql-ssms.md)
    - [Executar um pacote do SSIS com Transact-SQL (VS código)](ssis-quickstart-run-tsql-vscode.md)
    - [Executar um pacote do SSIS com o PowerShell](ssis-quickstart-run-powershell.md)
    - [Executar um pacote do SSIS com c#](./ssis-quickstart-run-dotnet.md) 

