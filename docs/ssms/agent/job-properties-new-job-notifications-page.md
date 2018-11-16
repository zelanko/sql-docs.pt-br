---
title: Propriedades do trabalho – Novo trabalho (página Notificações) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql13.ag.job.notifications.f1
ms.assetid: ed393cbd-4496-4399-a177-e5baa92fb689
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: de4bfe6cb6208e332b5c89ecabd4fc15caab94a7
ms.sourcegitcommit: 50b60ea99551b688caf0aa2d897029b95e5c01f3
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/15/2018
ms.locfileid: "51696277"
---
# <a name="job-properties---new-job-notifications-page"></a>Propriedades do trabalho – Novo trabalho (página Notificações)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> No momento, na [Instância Gerenciada do Banco de Dados SQL do Azure](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance), a maioria dos recursos do SQL Server Agent é compatível, mas não todos. Consulte [Azure SQL Database Managed Instance T-SQL differences from SQL Server](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent) (Diferenças entre o T-SQL da Instância Gerenciada do Banco de Dados SQL do Azure e o SQL Server) para obter detalhes.

Use esta página para definir ações para que o [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent seja executado quando o trabalho terminar.  
  
## <a name="options"></a>Opções  
**Email**  
Selecione esta opção para enviar email quando o trabalho terminar. Após selecionar essa opção, escolha o operador a ser notificado, além das condições que dispararão a notificação: **Quando o trabalho for bem-sucedido**; **Quando ocorrer falha no trabalho**; ou **Quando o trabalho for concluído**.  
  
**Página**  
Selecione esta opção para enviar email ao pager de um operador quando o trabalho terminar. Após selecionar essa opção, especifique o operador a ser notificado, além das condições que dispararão a notificação: **Quando o trabalho for bem-sucedido**; **Quando ocorrer falha no trabalho**; ou **Quando o trabalho for concluído**.  
  
**Net send**  
Selecione esta opção para usar o net send para notificar um operador quando o trabalho terminar. Após selecionar essa opção, especifique o operador a ser notificado, além das condições que dispararão a notificação: **Quando o trabalho for bem-sucedido**; **Quando ocorrer falha no trabalho**; ou **Quando o trabalho for concluído**.  
  
**Gravar no log de eventos de Aplicativo do Windows**  
Selecione esta opção para gravar uma entrada no log de eventos de aplicativo quando o trabalho terminar. Após selecionar essa opção, especifique a condição que fará com que a entrada seja gravada: **Quando o trabalho for bem-sucedido**; **Quando ocorrer falha no trabalho**; ou **Quando o trabalho for concluído**.  
  
**Excluir trabalho automaticamente**  
Selecione essa opção para excluir o trabalho quando ele terminar. Após selecionar essa opção, especifique a condição que disparará a exclusão do trabalho: **Quando o trabalho for bem-sucedido**; **Quando ocorrer falha no trabalho**; ou **Quando o trabalho for concluído**.  
  
## <a name="see-also"></a>Consulte Também  
[Implementar trabalhos](../../ssms/agent/implement-jobs.md)  
[Como configurar o SQL Server Agent Mail para usar o Database Mail (SQL Server Management Studio)](https://msdn.microsoft.com/4b8b61bd-4bd1-43cd-b6e5-c6ed2e101dce)  
  
