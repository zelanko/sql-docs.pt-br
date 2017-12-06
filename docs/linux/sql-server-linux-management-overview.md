---
title: Gerenciar o SQL Server no Linux | Microsoft Docs
description: "Este tópico fornece links para tarefas comuns de gerenciamento e ferramentas do SQL Server em execução no Linux."
author: rothja
ms.author: jroth
manager: jhubbard
ms.date: 03/17/2017
ms.topic: article
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: sql-linux
ms.suite: sql
ms.technology: database-engine
ms.assetid: 6bd8eb0b-593d-467e-87ea-ab1c4dbcd1ea
ms.custom: 
ms.workload: On Demand
ms.openlocfilehash: b9a28793d63f20a983f5eec92641f33978f6888b
ms.sourcegitcommit: 531d0245f4b2730fad623a7aa61df1422c255edc
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/01/2017
---
# <a name="choose-the-right-tool-to-manage-sql-server-on-linux"></a>Escolha a ferramenta certa para gerenciar o SQL Server no Linux

[!INCLUDE[tsql-appliesto-sslinux-only](../includes/tsql-appliesto-sslinux-only.md)]

Há várias maneiras de gerenciar 2017 do SQL Server no Linux. A seção a seguir fornecem uma visão geral das técnicas com ponteiros mais recursos e ferramentas de gerenciamento diferentes.

## <a name="mssql-conf"></a>MSSQL conf 
O **mssql conf** ferramenta configura o SQL Server no Linux. Para obter mais informações, consulte [configurar o SQL Server no Linux com mssql conf](sql-server-linux-configure-mssql-conf.md).

## <a name="transact-sql"></a>Transact-SQL

Quase tudo o que você pode fazer em uma ferramenta de cliente também pode ser feito com instruções Transact-SQL. O SQL Server fornece [exibições de gerenciamento dinâmico (DMVs)](../relational-databases/system-dynamic-management-views/system-dynamic-management-views.md) que consulta o status e a configuração do SQL Server. Também há [comandos Transact-SQL](https://msdn.microsoft.com/library/bb510741.aspx) para tarefas de gerenciamento de banco de dados. Você pode executar esses comandos em qualquer ferramenta de cliente que dá suporte ao se conectar ao SQL Server e executar consultas Transact-SQL. Os exemplos incluem [sqlcmd](sql-server-linux-setup-tools.md), [código do Visual Studio](sql-server-linux-develop-use-vscode.md), e [SQL Server Management Studio](sql-server-linux-manage-ssms.md).

## <a name="sql-server-management-studio-on-windows"></a>SQL Server Management Studio no Windows

SQL Server Management Studio (SSMS) é um aplicativo do Windows que fornece uma interface gráfica do usuário para o gerenciamento do SQL Server. Embora atualmente é executado somente no Windows, você pode usá-lo para se conectar remotamente a suas instâncias do SQL Server do Linux. Para obter mais informações sobre como usar o SSMS para gerenciar o SQL Server, consulte [Use SSMS para gerenciar o SQL Server no Linux](sql-server-linux-manage-ssms.md).

## <a name="powershell"></a>PowerShell

PowerShell fornece um ambiente rico de linha de comando para gerenciar o SQL Server no Linux. Para obter mais informações, consulte [usar o PowerShell para gerenciar o SQL Server no Linux](sql-server-linux-manage-powershell.md).

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre o SQL Server no Linux, consulte [SQL Server no Linux](sql-server-linux-overview.md).
