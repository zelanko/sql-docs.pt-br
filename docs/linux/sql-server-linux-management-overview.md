---
title: Gerenciar o SQL Server no Linux | Microsoft Docs
description: Este artigo fornece links para tarefas comuns de gerenciamento e ferramentas do SQL Server em execução no Linux.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 03/17/2017
ms.topic: article
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: ''
ms.suite: sql
ms.technology: database-engine
ms.assetid: 6bd8eb0b-593d-467e-87ea-ab1c4dbcd1ea
ms.custom: sql-linux
ms.openlocfilehash: e8867df2cc3102b398aaf5a600ab82b0ed152d78
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="choose-the-right-tool-to-manage-sql-server-on-linux"></a>Escolha a ferramenta certa para gerenciar o SQL Server no Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Há várias maneiras de gerenciar 2017 do SQL Server no Linux. A seção a seguir fornece uma visão geral das técnicas com ponteiros mais recursos e ferramentas de gerenciamento diferentes.

## <a name="mssql-conf"></a>mssql-conf 
O **mssql conf** ferramenta configura o SQL Server no Linux. Para obter mais informações, consulte [configurar o SQL Server no Linux com mssql conf](sql-server-linux-configure-mssql-conf.md).

## <a name="transact-sql"></a>Transact-SQL

Quase tudo o que você pode fazer em uma ferramenta de cliente também pode ser feito com instruções Transact-SQL. O SQL Server fornece [exibições de gerenciamento dinâmico (DMVs)](../relational-databases/system-dynamic-management-views/system-dynamic-management-views.md) que consulta o status e a configuração do SQL Server. Também há [comandos Transact-SQL](https://msdn.microsoft.com/library/bb510741.aspx) para tarefas de gerenciamento de banco de dados. Você pode executar esses comandos em qualquer ferramenta de cliente que dá suporte ao se conectar ao SQL Server e executar consultas Transact-SQL, por exemplo [sqlcmd](sql-server-linux-setup-tools.md) ou [código do Visual Studio](sql-server-linux-develop-use-vscode.md).

## <a name="sql-server-operations-studio-preview"></a>Operações do SQL Server Studio (visualização)

O novo Microsoft SQL Operations Studio (preview) é uma ferramenta de plataforma cruzada para o gerenciamento do SQL Server. Para obter mais informações, consulte [Microsoft SQL Operations Studio (preview)](../sql-operations-studio/what-is.md).

## <a name="sql-server-management-studio-on-windows"></a>SQL Server Management Studio no Windows

SQL Server Management Studio (SSMS) é um aplicativo do Windows que fornece uma interface gráfica do usuário para o gerenciamento do SQL Server. Embora atualmente é executado somente no Windows, você pode usá-lo para se conectar remotamente a suas instâncias do SQL Server do Linux. Para obter mais informações sobre como usar o SSMS para gerenciar o SQL Server, consulte [Use SSMS para gerenciar o SQL Server no Linux](sql-server-linux-manage-ssms.md).

## <a name="mssql-cli-preview"></a>MSSQL-cli (visualização)

A Microsoft lançou uma nova ferramenta de script de plataforma cruzada para o SQL Server, [mssql cli](https://blogs.technet.microsoft.com/dataplatforminsider/2017/12/12/try-mssql-cli-a-new-interactive-command-line-tool-for-sql-server/). Essa ferramenta está atualmente em visualização.

## <a name="powershell"></a>PowerShell

PowerShell fornece um ambiente rico de linha de comando para gerenciar o SQL Server no Linux. Para obter mais informações, consulte [usar o PowerShell para gerenciar o SQL Server no Linux](sql-server-linux-manage-powershell.md).

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre o SQL Server no Linux, consulte [SQL Server no Linux](sql-server-linux-overview.md).
