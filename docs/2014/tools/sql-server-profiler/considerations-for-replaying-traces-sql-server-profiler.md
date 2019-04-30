---
title: Considerações para reproduzir rastreamentos (SQL Server Profiler) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: profiler
ms.topic: conceptual
helpviewer_keywords:
- traces [SQL Server], replaying
- replaying traces
ms.assetid: 73fa339f-b71a-4be4-97ca-d4ae84c8b90b
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 2dd2fe9f5e4e2a5b41c9951b1a38dd819a15aa35
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63316037"
---
# <a name="considerations-for-replaying-traces-sql-server-profiler"></a>Considerações para reproduzir rastreamentos (SQL Server Profiler)
  [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] não pode reproduzir os seguintes tipos de rastreamento:  
  
-   Rastreamentos que contêm replicação transacional e outra atividade de log de transações. Esses eventos são ignorados. Outros tipos de replicação não marcam o log de transações e, logo, não são afetados.  
  
-   Rastreamentos que contêm operações que envolvem identificadores globalmente exclusivos (GUID). Esses eventos serão ignorados.  
  
-   Rastreamentos que contêm operações em colunas **text**, **ntext**e **image** envolvendo o utilitário **bcp** , as instruções BULK INSERT, READTEXT, WRITETEXT e UPDATETEXT e operações de texto completo. Esses eventos são ignorados.  
  
-   Rastreamentos que contêm associação de sessões: os procedimentos armazenados do sistema **sp_getbindtoken** e **sp_bindsession** . Esses eventos são ignorados.  
  
> [!NOTE]  
>  Se você não usar o modelo de reprodução pré-configurado (**TSQL_Replay**) e não capturar todos os dados necessários, o [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] não reproduzirá o rastreamento. Para obter mais informações, consulte [Replay Requirements](replay-requirements.md).  
  
 Para obter informações sobre quais permissões são necessárias para reproduzir um rastreamento, veja [Permissões necessárias para executar o SQL Server Profiler](sql-server-profiler.md).  
  
## <a name="see-also"></a>Consulte também  
 [Utilitário bcp](../bcp-utility.md)   
 [Referência de classe de evento do SQL Server](../../relational-databases/event-classes/sql-server-event-class-reference.md)   
 [sp_getbindtoken &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-getbindtoken-transact-sql)   
 [sp_bindsession &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-bindsession-transact-sql)   
 [BULK INSERT &#40;Transact-SQL&#41;](/sql/t-sql/statements/bulk-insert-transact-sql)   
 [READTEXT &#40;Transact-SQL&#41;](/sql/t-sql/queries/readtext-transact-sql)   
 [WRITETEXT &#40;Transact-SQL&#41;](/sql/t-sql/queries/writetext-transact-sql)   
 [UPDATETEXT &#40;Transact-SQL&#41;](/sql/t-sql/queries/updatetext-transact-sql)  
  
  
