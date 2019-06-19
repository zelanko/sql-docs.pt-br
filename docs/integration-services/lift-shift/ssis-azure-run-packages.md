---
title: Executar pacotes do SSIS no Azure | Microsoft Docs
description: Fornece uma visão geral dos métodos disponíveis para executar pacotes SSIS implantados para o Banco de Dados SQL do Azure.
ms.date: 05/29/2018
ms.topic: conceptual
ms.prod: sql
ms.prod_service: integration-services
ms.custom: ''
ms.technology: integration-services
author: swinarko
ms.author: sawinark
ms.reviewer: maghan
manager: craigg
ms.openlocfilehash: 8b91a1572e5c7cd477d8e112b68b8f9a46fb1153
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66012332"
---
# <a name="run-sql-server-integration-services-ssis-packages-deployed-in-azure"></a>Executar pacotes SSIS (SQL Server Integration Services) implantados no Azure

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]



É possível executar pacotes SSIS implantados no Catálogo do SSISDB em um servidor de Banco de Dados SQL do Azure escolhendo um dos métodos descritos neste artigo. É possível executar um pacote diretamente ou um pacote como parte de um pipeline do Azure Data Factory. Para obter uma visão geral sobre o SSIS no Azure, consulte [Implantar e executar pacotes SSIS no Azure](ssis-azure-lift-shift-ssis-packages-overview.md).

- Executar um pacote diretamente

  - [Executar com SSMS](#ssms)

  - [Executar com procedimentos armazenados](#sproc)

  - [Executar com script ou código](#script)

- Executar um pacote como parte de um pipeline do Azure Data Factory

  - [Executar com a atividade Executar pacote do SSIS](#exec_activity)

  - [Executar com a atividade Procedimento armazenado](#sproc_activity)

> [!NOTE]
> A execução de um pacote com `dtexec.exe` não foi testada com os pacotes implantados no Azure.

## <a name="ssms"></a> Executar um pacote com o SSMS

No SSMS (SQL Server Management Studio), é possível clicar com o botão direito do mouse em um pacote implantado no banco de dados do Catálogo do SSIS, SSISDB e selecionar **Executar** para abrir a caixa de diálogo **Executar pacote**. Para obter mais informações, consulte [Executar um pacote SSIS com o SSMS (SQL Server Management Studio)](../ssis-quickstart-run-ssms.md).

## <a name="sproc"></a> Executar um pacote com procedimentos armazenados

Em qualquer ambiente do qual for possível se conectar com o Banco de Dados SQL do Azure e executar o código do Transact-SQL, será possível executar um pacote chamando os seguintes procedimentos armazenados:

1. **[catalog].[create_execution]**. Para obter mais informações, consulte [catalog.create_execution](../system-stored-procedures/catalog-create-execution-ssisdb-database.md).

2. **[catalog].[set_execution_parameter_value]**. Para obter mais informações, consulte [catalog.set_execution_parameter_value](../system-stored-procedures/catalog-set-execution-parameter-value-ssisdb-database.md).

3. **[catalog].[start_execution]**. Para obter mais informações, consulte [catalog.start_execution](../system-stored-procedures/catalog-start-execution-ssisdb-database.md).

Para obter mais informações, veja os exemplos a seguir:

- [Executar um pacote do SSIS do SSMS com o Transact-SQL](../ssis-quickstart-run-tsql-ssms.md)

- [Executar um pacote do SSIS no Visual Studio Code com o Transact-SQL](../ssis-quickstart-run-tsql-vscode.md)

## <a name="script"></a> Executar um pacote com script ou código

Em qualquer ambiente de desenvolvimento do qual for possível chamar uma API gerenciada, será possível executar um pacote chamando o método `Execute` do objeto `Package` no namespace `Microsoft.SQLServer.Management.IntegrationServices`.

Para obter mais informações, veja os exemplos a seguir:

- [Executar um pacote do SSIS com o PowerShell](../ssis-quickstart-run-powershell.md)

- [Executar um pacote do SSIS com o código C# em um aplicativo .NET](../ssis-quickstart-run-dotnet.md)

## <a name="exec_activity"></a> Executar um pacote com a atividade Executar pacote do SSIS

Para obter mais informações, consulte [Executar um pacote do SSIS usando a atividade Executar pacote do SSIS no Azure Data Factory](https://docs.microsoft.com/azure/data-factory/how-to-invoke-ssis-package-ssis-activity).

## <a name="sproc_activity"></a> Executar um pacote com a atividade Procedimento armazenado

Para obter mais informações, consulte [Executar um pacote do SSIS usando a atividade Procedimento armazenado no Azure Data Factory](https://docs.microsoft.com/azure/data-factory/how-to-invoke-ssis-package-stored-procedure-activity).

## <a name="next-steps"></a>Próximas etapas

Conheça opções para agendar pacotes do SSIS implantados no Azure. Para obter mais informações, confira [Agendar pacotes SSIS no Azure](ssis-azure-schedule-packages.md).
