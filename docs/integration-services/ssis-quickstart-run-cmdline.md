---
description: Executar um pacote do SSIS no prompt de comando com DTExec.exe
title: Executar um pacote do SSIS por meio do prompt de comando | Microsoft Docs
ms.date: 05/21/2018
ms.topic: quickstart
ms.prod: sql
ms.prod_service: integration-services
ms.custom: ''
ms.technology: integration-services
author: chugugrace
ms.author: chugu
ms.openlocfilehash: bc97eb4c3c8d554a86a773910508c2d1ba936459
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88495401"
---
# <a name="run-an-ssis-package-from-the-command-prompt-with-dtexecexe"></a>Executar um pacote do SSIS no prompt de comando com DTExec.exe

[!INCLUDE[sqlserver-ssis](../includes/applies-to-version/sqlserver-ssis.md)]


Este guia de início rápido demonstra como executar um pacote do SSIS por meio do prompt de comando executando `DTExec.exe` com os parâmetros apropriados.

> [!NOTE]
> O método descrito neste artigo não foi testado com os pacotes implantados em um servidor de Banco de Dados SQL do Azure.

Para obter mais informações sobre o `DTExec.exe`, consulte [Utilitário dtexec](https://docs.microsoft.com/sql/integration-services/packages/dtexec-utility).

## <a name="supported-platforms"></a>Plataformas com suporte

Você pode usar as informações neste guia de início rápido para executar um pacote do SSIS nas seguintes plataformas:

-   SQL Server no Windows.

O método descrito neste artigo não foi testado com os pacotes implantados em um servidor de Banco de Dados SQL do Azure. Para obter mais informações sobre como implantar e executar pacotes no Azure, veja [Remover e deslocar cargas de trabalho do SQL Server Integration Services para a nuvem](lift-shift/ssis-azure-lift-shift-ssis-packages-overview.md).

Você não pode usar as informações neste guia de início rápido para executar um pacote do SSIS no Linux. Para obter mais informações sobre como executar pacotes no Linux, veja [Extrair, transformar e carregar dados no Linux com o SSIS](../linux/sql-server-linux-migrate-ssis.md).

## <a name="run-a-package-with-dtexec"></a>Executar um pacote com dtexec

Se a pasta que contém `DTExec.exe` não está na variável de ambiente `path`, talvez você precise usar o comando `cd` para mudar para o diretório dela. Para SQL Server 2017, essa pasta normalmente é `C:\Program Files (x86)\Microsoft SQL Server\140\DTS\Binn`.

Com os valores de parâmetro usados no exemplo a seguir, o programa executa o pacote no caminho da pasta especificada no servidor do SSIS – ou seja, o servidor que hospeda o SSISDB (banco de dados do Catálogo do SSIS). O parâmetro `/Server` fornece o nome do servidor. O programa se conecta como o usuário atual com a Autenticação Integrada do Windows. Para usar a autenticação do SQL, especifique os parâmetros `/User` e `Password` com valores apropriados.

1. Abra uma janela de Prompt de Comando.

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
