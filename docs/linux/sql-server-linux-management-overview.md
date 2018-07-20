---
title: Gerenciar o SQL Server no Linux | Microsoft Docs
description: Este artigo fornece links para tarefas comuns de gerenciamento e ferramentas para o SQL Server em execução no Linux.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 03/17/2017
ms.topic: conceptual
ms.prod: sql
ms.component: ''
ms.suite: sql
ms.technology: linux
ms.assetid: 6bd8eb0b-593d-467e-87ea-ab1c4dbcd1ea
ms.custom: sql-linux
ms.openlocfilehash: 26123d12c48c6c8abd51590d3f6d42c7476acd29
ms.sourcegitcommit: a431ca21eac82117492d7b84c398ddb3fced53cc
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/17/2018
ms.locfileid: "39102414"
---
# <a name="choose-the-right-tool-to-manage-sql-server-on-linux"></a>Escolha a ferramenta certa para gerenciar o SQL Server no Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Há várias maneiras para gerenciar o SQL Server 2017 no Linux. A seção a seguir fornece uma visão geral das ferramentas de gerenciamento diferentes e técnicas com ponteiros para obter mais recursos.

## <a name="mssql-conf"></a>mssql-conf 

O **mssql-conf** ferramenta configura o SQL Server no Linux. Para obter mais informações, consulte [configurar o SQL Server no Linux com o mssql-conf](sql-server-linux-configure-mssql-conf.md).

## <a name="transact-sql"></a>Transact-SQL

Quase tudo o que você pode fazer em uma ferramenta de cliente também pode ser feito com instruções Transact-SQL. O SQL Server fornece [exibições de gerenciamento dinâmico (DMVs)](../relational-databases/system-dynamic-management-views/system-dynamic-management-views.md) que consultar o status e a configuração do SQL Server. Também há [comandos Transact-SQL](https://msdn.microsoft.com/library/bb510741.aspx) para tarefas de gerenciamento de banco de dados. Você pode executar esses comandos em qualquer ferramenta de cliente que dá suporte à conexão ao SQL Server e executar consultas Transact-SQL, por exemplo [sqlcmd](sql-server-linux-setup-tools.md) ou [Visual Studio Code](sql-server-linux-develop-use-vscode.md).

## <a name="sql-server-operations-studio-preview"></a>SQL Server Operations Studio (versão prévia)

O novo Microsoft SQL Operations Studio (preview) é uma ferramenta de plataforma cruzada para o gerenciamento do SQL Server. Para obter mais informações, consulte [Microsoft SQL Operations Studio (preview)](../sql-operations-studio/what-is.md).

## <a name="sql-server-management-studio-on-windows"></a>SQL Server Management Studio no Windows

SQL Server Management Studio (SSMS) é um aplicativo do Windows que fornece uma interface gráfica do usuário para gerenciar o SQL Server. Embora atualmente seja executado somente no Windows, você pode usá-lo para se conectar remotamente para suas instâncias do SQL Server do Linux. Para obter mais informações sobre como usar o SSMS para gerenciar o SQL Server, consulte [usar o SSMS para gerenciar o SQL Server no Linux](sql-server-linux-manage-ssms.md).

## <a name="mssql-cli-preview"></a>MSSQL-cli (versão prévia)

A Microsoft lançou uma nova ferramenta de script de plataforma cruzada para o SQL Server [mssql-cli](https://blogs.technet.microsoft.com/dataplatforminsider/2017/12/12/try-mssql-cli-a-new-interactive-command-line-tool-for-sql-server/). Essa ferramenta está atualmente em visualização.

## <a name="powershell"></a>PowerShell

PowerShell fornece um rico ambiente de linha de comando para gerenciar o SQL Server no Linux. Para obter mais informações, consulte [usar o PowerShell para gerenciar o SQL Server no Linux](sql-server-linux-manage-powershell.md).

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre o SQL Server no Linux, consulte [SQL Server no Linux](sql-server-linux-overview.md).
