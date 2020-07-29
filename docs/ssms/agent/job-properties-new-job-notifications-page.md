---
title: Propriedades do trabalho – Novo trabalho (página Notificações)
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql13.ag.job.notifications.f1
ms.assetid: ed393cbd-4496-4399-a177-e5baa92fb689
author: markingmyname
ms.author: maghan
ms.reviewer: ''
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 2d1bc2ec3aef699e491fdac2036352fd986fec85
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85690605"
---
# <a name="job-properties---new-job-notifications-page"></a>Propriedades do trabalho – Novo trabalho (página Notificações)
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

> [!IMPORTANT]  
> No momento, na [Instância Gerenciada do Banco de Dados SQL do Azure](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance), a maioria dos recursos do SQL Server Agent é compatível, mas não todos. Consulte [Azure SQL Database Managed Instance T-SQL differences from SQL Server](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent) (Diferenças entre o T-SQL da Instância Gerenciada do Banco de Dados SQL do Azure e o SQL Server) para obter detalhes.

Use esta página com o objetivo de definir as ações que o [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent executará quando o trabalho for concluído.  
  
## <a name="options"></a>Opções  
**Email**  
Selecione esta opção para enviar email quando o trabalho terminar. Depois de selecionar essa opção, escolha o operador a ser notificado e a condição que vai disparar a notificação: **Quando o trabalho é bem-sucedido**; **Quando o trabalho falha**; ou **Quando o trabalho é concluído**.  
  
**Página**  
Selecione esta opção para enviar email ao pager de um operador quando o trabalho terminar. Depois de selecionar essa opção, especifique o operador a ser notificado e a condição que vai disparar a notificação: **Quando o trabalho é bem-sucedido**; **Quando o trabalho falha**; ou **Quando o trabalho é concluído**.  
  
**Net send**  
Selecione esta opção para usar o net send para notificar um operador quando o trabalho terminar. Depois de selecionar essa opção, especifique o operador a ser notificado e a condição que vai disparar a notificação: **Quando o trabalho é bem-sucedido**; **Quando o trabalho falha**; ou **Quando o trabalho é concluído**.  
  
**Gravar no log de eventos de Aplicativo do Windows**  
Selecione esta opção para gravar uma entrada no log de eventos de aplicativo quando o trabalho terminar. Depois de selecionar essa opção, especifique a condição que fará com que a entrada seja gravada: **Quando o trabalho é bem-sucedido**; **Quando o trabalho falha**; ou **Quando o trabalho é concluído**.  
  
**Excluir trabalho automaticamente**  
Selecione essa opção para excluir o trabalho quando ele terminar. Depois de selecionar essa opção, especifique a condição que disparará a exclusão do trabalho: **Quando o trabalho é bem-sucedido**; **Quando o trabalho falha**; ou **Quando o trabalho é concluído**.  
  
## <a name="see-also"></a>Consulte Também  
[Implementar trabalhos](../../ssms/agent/implement-jobs.md)  
[Como: configurar o SQL Server Agent Mail para usar o Database Mail](https://msdn.microsoft.com/4b8b61bd-4bd1-43cd-b6e5-c6ed2e101dce)  
  
