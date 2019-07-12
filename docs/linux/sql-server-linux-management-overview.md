---
title: Gerenciar o SQL Server no Linux
description: Este artigo fornece links para tarefas comuns de gerenciamento e ferramentas para o SQL Server em execução no Linux.
author: VanMSFT
ms.author: vanto
manager: jroth
ms.date: 03/17/2017
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: 6bd8eb0b-593d-467e-87ea-ab1c4dbcd1ea
ms.openlocfilehash: 33489d1704d90d32b8b9362b1fa87f123ac17236
ms.sourcegitcommit: 93d1566b9fe0c092c9f0f8c84435b0eede07019f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2019
ms.locfileid: "67834925"
---
# <a name="choose-the-right-tool-to-manage-sql-server-on-linux"></a>Escolha a ferramenta certa para gerenciar o SQL Server no Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Há várias maneiras para gerenciar o SQL Server no Linux. A seção a seguir fornece uma visão geral das ferramentas de gerenciamento diferentes e técnicas com ponteiros para obter mais recursos.

## <a name="mssql-conf"></a>mssql-conf 

O **mssql-conf** ferramenta configura o SQL Server no Linux. Para obter mais informações, consulte [configurar o SQL Server no Linux com o mssql-conf](sql-server-linux-configure-mssql-conf.md).

## <a name="transact-sql"></a>Transact-SQL

Quase tudo o que você pode fazer em uma ferramenta de cliente também pode ser feito com instruções Transact-SQL. O SQL Server fornece [exibições de gerenciamento dinâmico (DMVs)](../relational-databases/system-dynamic-management-views/system-dynamic-management-views.md) que consultar o status e a configuração do SQL Server. Também há [comandos Transact-SQL](../t-sql/language-reference.md) para tarefas de gerenciamento de banco de dados. Você pode executar esses comandos em qualquer ferramenta de cliente que dá suporte à conexão ao SQL Server e executar consultas Transact-SQL, por exemplo [sqlcmd](sql-server-linux-setup-tools.md) ou [Visual Studio Code](sql-server-linux-develop-use-vscode.md).

## <a name="azure-data-studio"></a>Azure Data Studio

O novo Studio dados do Azure é uma ferramenta de plataforma cruzada para o gerenciamento do SQL Server. Para obter mais informações, consulte [Studio do Azure Data](../azure-data-studio/what-is.md).

## <a name="sql-server-management-studio-on-windows"></a>SQL Server Management Studio no Windows

SQL Server Management Studio (SSMS) é um aplicativo do Windows que fornece uma interface gráfica do usuário para gerenciar o SQL Server. Embora atualmente seja executado somente no Windows, você pode usá-lo para se conectar remotamente para suas instâncias do SQL Server do Linux. Para obter mais informações sobre como usar o SSMS para gerenciar o SQL Server, consulte [usar o SSMS para gerenciar o SQL Server no Linux](sql-server-linux-manage-ssms.md).

## <a name="mssql-cli-preview"></a>mssql-cli (preview)

A Microsoft lançou uma nova ferramenta de script de plataforma cruzada para o SQL Server [mssql-cli](https://blogs.technet.microsoft.com/dataplatforminsider/2017/12/12/try-mssql-cli-a-new-interactive-command-line-tool-for-sql-server/). Essa ferramenta está atualmente em visualização.

## <a name="powershell"></a>PowerShell

PowerShell fornece um rico ambiente de linha de comando para gerenciar o SQL Server no Linux. Para obter mais informações, consulte [usar o PowerShell para gerenciar o SQL Server no Linux](sql-server-linux-manage-powershell.md).

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre o SQL Server no Linux, consulte [SQL Server no Linux](sql-server-linux-overview.md).
