---
title: "Considerações para reproduzir rastreamentos (SQL Server Profiler) | Microsoft Docs"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- traces [SQL Server], replaying
- replaying traces
ms.assetid: 73fa339f-b71a-4be4-97ca-d4ae84c8b90b
caps.latest.revision: 21
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 77934826a2ba364c4ec8b4e6a5295699d8469257
ms.contentlocale: pt-br
ms.lasthandoff: 08/02/2017

---
# <a name="considerations-for-replaying-traces-sql-server-profiler"></a>Considerações para reproduzir rastreamentos (SQL Server Profiler)
  [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]não é possível reproduzir os seguintes tipos de rastreamentos:  
  
-   Rastreamentos que contêm replicação transacional e outra atividade de log de transações. Esses eventos são ignorados. Outros tipos de replicação não marcam o log de transações e, logo, não são afetados.  
  
-   Rastreamentos que contêm operações que envolvem identificadores globalmente exclusivos (GUID). Esses eventos serão ignorados.  
  
-   Rastreamentos que contêm operações em colunas **text**, **ntext**e **image** envolvendo o utilitário **bcp** , as instruções BULK INSERT, READTEXT, WRITETEXT e UPDATETEXT e operações de texto completo. Esses eventos são ignorados.  
  
-   Rastreamentos que contêm associação de sessões: os procedimentos armazenados do sistema **sp_getbindtoken** e **sp_bindsession** . Esses eventos são ignorados.  
  
> [!NOTE]  
>  Se você não usar o modelo de reprodução pré-configurado (**TSQL_Replay**) e não capturar todos os dados necessários, o [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] não reproduzirá o rastreamento. Para obter mais informações, consulte [Replay Requirements](../../tools/sql-server-profiler/replay-requirements.md).  
  
 Para obter informações sobre quais permissões são necessárias para reproduzir um rastreamento, veja [Permissões necessárias para executar o SQL Server Profiler](../../tools/sql-server-profiler/permissions-required-to-run-sql-server-profiler.md).  
  
## <a name="see-also"></a>Consulte também  
 [Utilitário bcp](../../tools/bcp-utility.md)   
 [Referência de classe de evento do SQL Server](../../relational-databases/event-classes/sql-server-event-class-reference.md)   
 [sp_getbindtoken &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-getbindtoken-transact-sql.md)   
 [sp_bindsession &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-bindsession-transact-sql.md)   
 [INSERÇÃO em MASSA &#40;O Transact-SQL&#41;](../../t-sql/statements/bulk-insert-transact-sql.md)   
 [READTEXT &#40; Transact-SQL &#41;](../../t-sql/queries/readtext-transact-sql.md)   
 [WRITETEXT &#40; Transact-SQL &#41;](../../t-sql/queries/writetext-transact-sql.md)   
 [UPDATETEXT &#40; Transact-SQL &#41;](../../t-sql/queries/updatetext-transact-sql.md)  
  
  

