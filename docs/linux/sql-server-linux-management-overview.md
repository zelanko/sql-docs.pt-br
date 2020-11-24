---
title: Gerenciar o SQL Server em Linux
description: Este artigo fornece links para tarefas de gerenciamento e ferramentas comuns para o SQL Server em execução no Linux.
author: VanMSFT
ms.author: vanto
ms.date: 03/17/2017
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: 6bd8eb0b-593d-467e-87ea-ab1c4dbcd1ea
moniker: '>= sql-server-linux-2017 || >= sql-server-2017 || =sqlallproducts-allversions'
ms.openlocfilehash: a1a2d38a9c42905d433a403952a7f96fd9e0245f
ms.sourcegitcommit: a49a66dbda0cb16049e092b49c8318ac3865af3c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/20/2020
ms.locfileid: "94983130"
---
# <a name="choose-the-right-tool-to-manage-sql-server-on-linux"></a>Escolher a ferramenta correta para gerenciar o SQL Server em Linux

[!INCLUDE [SQL Server - Linux](../includes/applies-to-version/sql-linux.md)]

Há várias maneiras de gerenciar o SQL Server em Linux. A seção a seguir fornece uma visão geral rápida de diferentes ferramentas de gerenciamento e técnicas com ponteiros para mais recursos.

## <a name="mssql-conf"></a>mssql-conf 

A ferramenta **mssql-conf** configura o SQL Server em Linux. Para obter mais informações, confira [Configurar o SQL Server em Linux com mssql-conf](sql-server-linux-configure-mssql-conf.md).

## <a name="transact-sql"></a>Transact-SQL

Quase tudo o que você pode fazer em uma ferramenta de cliente também pode ser feito com instruções Transact-SQL. O SQL Server fornece [DMVs (exibições de gerenciamento dinâmico)](../relational-databases/system-dynamic-management-views/system-dynamic-management-views.md) que consultam o status e a configuração do SQL Server. Também há [comandos Transact-SQL](../t-sql/language-reference.md) para tarefas de gerenciamento de banco de dados. Você pode executar esses comandos em qualquer ferramenta de cliente que dê suporte à conexão com o SQL Server e execução de consultas Transact-SQL, por exemplo, o [sqlcmd](sql-server-linux-setup-tools.md) ou o [Visual Studio Code](../tools/visual-studio-code/sql-server-develop-use-vscode.md).

## <a name="azure-data-studio"></a>Azure Data Studio

O novo Azure Data Studio é uma ferramenta multiplataforma para gerenciamento do SQL Server. Para obter mais informações, confira [Azure Data Studio](../azure-data-studio/what-is.md).

## <a name="sql-server-management-studio-on-windows"></a>SQL Server Management Studio no Windows

O SSMS (SQL Server Management Studio) é um aplicativo do Windows que fornece uma interface gráfica do usuário para gerenciamento do SQL Server. Embora ele seja atualmente executado apenas no Windows, você pode usá-lo para se conectar remotamente às instâncias do SQL Server em Linux. Para obter mais informações sobre como usar o SSMS para gerenciar o SQL Server, confira [Usar o SSMS para gerenciar o SQL Server em Linux](sql-server-linux-manage-ssms.md).

## <a name="mssql-cli-preview"></a>mssql-cli (versão prévia)

A Microsoft lançou uma nova ferramenta de script multiplataforma para o SQL Server, [mssql-cli](https://blogs.technet.microsoft.com/dataplatforminsider/2017/12/12/try-mssql-cli-a-new-interactive-command-line-tool-for-sql-server/). Atualmente, essa ferramenta está em versão prévia.

## <a name="powershell"></a>PowerShell

O PowerShell fornece um ambiente de linha de comando avançado para gerenciar o SQL Server em Linux. Para obter mais informações, confira [Usar o PowerShell para gerenciar o SQL Server em Linux](sql-server-linux-manage-powershell.md).

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre o SQL Server em Linux, confira [SQL Server em Linux](sql-server-linux-overview.md).