---
title: Log de erros do SQL Server Agent | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.component: ssms-agent
ms.reviewer: ''
ms.suite: sql
ms.technology: ssms
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- logs [SQL Server], SQL Server Agent
- messages [SQL Server], SQL Server Agent
- errors [SQL Server], logs
- SQL Server Agent, errors
ms.assetid: 0b2d6e6e-cd2d-4b8b-9fa2-2bbd2fc0da41
caps.latest.revision: 4
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 87b362a568a020f4882ebbed4b8e1e7558a6c3a3
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2018
ms.locfileid: "37971318"
---
# <a name="sql-server-agent-error-log"></a>Log de erros do SQL Server Agent
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> No momento, na [Instância Gerenciada do Banco de Dados SQL do Azure](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance), a maioria dos recursos do SQL Server Agent é compatível, mas não todos. Consulte [Azure SQL Database Managed Instance T-SQL differences from SQL Server](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent) (Diferenças entre o T-SQL da Instância Gerenciada do Banco de Dados SQL do Azure e o SQL Server) para obter detalhes.

[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] O Agent cria um log de erros que registra avisos e erros por padrão. Os seguintes avisos e erros são exibidos no log:  
  
-   Mensagens de aviso que fornecem informações sobre problemas potenciais, como "O trabalho \<*job_name*> foi excluído durante sua execução".  
  
-   Mensagens de erro que normalmente requerem intervenção de um administrador de sistema, como "Não é possível iniciar a sessão de email". As mensagens de erro podem ser enviadas a um usuário ou computador específico por meio de **net send**.  
  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] mantém até nove logs de erros do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent. Cada log arquivado tem uma extensão que indica sua idade relativa. Por exemplo, uma extensão .1 indica o log de erros arquivado mais recentemente e a extensão .9, o mais antigo.  
  
Por padrão, mensagens de rastreamento de execução não são gravadas no log de erros do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent, pois elas podem lotá-lo. Quando o log de erros fica cheio, sua capacidade de selecionar e analisar erros mais difíceis é reduzida. Como o log é somado à carga de processamento do servidor, é importante considerar com atenção o valor obtido ao capturar mensagens de rastreamento de execução para o log de erros. Geralmente, é melhor capturar todas as mensagens apenas quando você estiver depurando um problema específico.  
  
Quando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent é interrompido, você pode modificar o local do log de erros do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent. Quando o log de erros está vazio, não é possível abri-lo. É possível reciclar o log do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent a qualquer hora, sem ter que interromper o [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent.  
  
**Para exibir o log de erros do SQL Server Agent**  
  
-   [Exibir o log de erros do SQL Server Agent &#40;SQL Server Management Studio&#41;](../../ssms/agent/view-sql-server-agent-error-log-sql-server-management-studio.md)  
  
**Para renomear o log de erros do SQL Server Agent**  
  
-   [Renomear um log de erros do SQL Server Agent &#40;SQL Server Management Studio&#41;](../../ssms/agent/rename-a-sql-server-agent-error-log-sql-server-management-studio.md)  
  
**Para enviar mensagens de erro do SQL Server Agent**  
  
-   [Send SQL Server Agent Error Messages](../../ssms/agent/send-sql-server-agent-error-messages.md)  
  
**Para gravar mensagens de rastreamento de execução no log de erros do SQL Server Agent**  
  
-   [Gravar mensagens de rastreamento de execução no log de erros do SQL Server Agent &#40;SQL Server Management Studio&#41;](../../ssms/agent/write-execution-trace-messages-to-sql-server-agent-log-ssms.md)  
  
