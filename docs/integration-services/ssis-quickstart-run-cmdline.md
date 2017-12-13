---
title: Executar um pacote do SSIS por meio do prompt de comando | Microsoft Docs
ms.date: 09/25/2017
ms.topic: article
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: integration-services
ms.suite: sql
ms.custom: 
ms.technology: integration-services
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 33293b17caff5d5c71b58bff3f34ed130ab19ba3
ms.sourcegitcommit: 531d0245f4b2730fad623a7aa61df1422c255edc
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/01/2017
---
# <a name="run-an-ssis-package-from-the-command-prompt-with-dtexecexe"></a>Executar um pacote do SSIS no prompt de comando com DTExec.exe
Este tutorial de início rápido demonstra como executar um pacote do SSIS por meio do prompt de comando executando `DTExec.exe` com os parâmetros apropriados.

> [!NOTE]
> O método descrito neste artigo não foi testado com os pacotes implantados em um servidor de Banco de Dados SQL do Azure.

Para obter mais informações sobre o `DTExec.exe`, consulte [Utilitário dtexec](https://docs.microsoft.com/sql/integration-services/packages/dtexec-utility).

## <a name="run-a-package-with-dtexec"></a>Executar um pacote com dtexec

Se a pasta que contém `DTExec.exe` não está na variável de ambiente `path`, talvez você precise usar o comando `cd` para mudar para o diretório dela. Para SQL Server 2017, essa pasta normalmente é `C:\Program Files (x86)\Microsoft SQL Server\140\DTS\Binn`.

Com os valores de parâmetro usados no exemplo a seguir, o programa executa o pacote no caminho da pasta especificada no servidor do SSIS – ou seja, o servidor que hospeda o SSISDB (banco de dados do Catálogo do SSIS). O parâmetro `/Server` fornece o nome do servidor. O programa se conecta como o usuário atual com a Autenticação Integrada do Windows. Para usar a autenticação do SQL, especifique os parâmetros `/User` e `Password` com valores apropriados.

1. Abra uma janela do prompt de comando.

2. Execute `DTExec.exe` e forneça valores pelo menos para os parâmetros `ISServer` e `Server`, conforme mostrado no exemplo a seguir:

    ```cmd
    dtexec /ISServer "\SSISDB\Project1Folder\Integration Services Project1\Package.dtsx" /Server "localhost"
    ```

## <a name="next-steps"></a>Próximas etapas
- Considere outras maneiras de executar um pacote.
    - [Executar um pacote do SSIS com o SSMS](./ssis-quickstart-run-ssms.md)
    - [Executar um pacote do SSIS com o Transact-SQL (SSMS)](./ssis-quickstart-run-tsql-ssms.md)
    - [Executar um pacote do SSIS com o Transact-SQL (VS Code)](ssis-quickstart-run-tsql-vscode.md)
    - [Executar um pacote do SSIS com o PowerShell](ssis-quickstart-run-powershell.md)
    - [Executar um pacote do SSIS com o C#](./ssis-quickstart-run-dotnet.md) 
