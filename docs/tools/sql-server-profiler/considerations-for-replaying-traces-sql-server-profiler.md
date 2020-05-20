---
title: Considerações sobre repetição de rastreamentos
titleSuffix: SQL Server Profiler
description: Descubra quais operações, procedimentos armazenados, modelos e atividades de log evitam que o SQL Server Profiler reproduza rastreamentos.
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: profiler
ms.topic: conceptual
ms.assetid: 73fa339f-b71a-4be4-97ca-d4ae84c8b90b
author: markingmyname
ms.author: maghan
ms.custom: seo-lt-2019
ms.date: 03/06/2017
ms.openlocfilehash: a12b6101cde482d38ef9573cb236cc7eba002aab
ms.sourcegitcommit: b8933ce09d0e631d1183a84d2c2ad3dfd0602180
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/13/2020
ms.locfileid: "83151913"
---
# <a name="considerations-for-replaying-traces-sql-server-profiler"></a>Considerações para reproduzir rastreamentos (SQL Server Profiler)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] não pode reproduzir os seguintes tipos de rastreamento:  
  
-   Rastreamentos que contêm replicação transacional e outra atividade de log de transações. Esses eventos são ignorados. Outros tipos de replicação não marcam o log de transações e, logo, não são afetados.  
  
-   Rastreamentos que contêm operações que envolvem identificadores globalmente exclusivos (GUID). Esses eventos serão ignorados.  
  
-   Rastreamentos que contêm operações em colunas **text**, **ntext**e **image** envolvendo o utilitário **bcp** , as instruções BULK INSERT, READTEXT, WRITETEXT e UPDATETEXT e operações de texto completo. Esses eventos são ignorados.  
  
-   Rastreamentos que contêm associação de sessões: os procedimentos armazenados do sistema **sp_getbindtoken** e **sp_bindsession** . Esses eventos são ignorados.  
  
> [!NOTE]  
>  Se você não usar o modelo de reprodução pré-configurado (**TSQL_Replay**) e não capturar todos os dados necessários, o [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] não reproduzirá o rastreamento. Para obter mais informações, consulte [Replay Requirements](../../tools/sql-server-profiler/replay-requirements.md).  
  
 Para obter informações sobre quais permissões são necessárias para reproduzir um rastreamento, veja [Permissões necessárias para executar o SQL Server Profiler](../../tools/sql-server-profiler/permissions-required-to-run-sql-server-profiler.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Utilitário bcp](../../tools/bcp-utility.md)   
 [Referência de classe de evento do SQL Server](../../relational-databases/event-classes/sql-server-event-class-reference.md)   
 [sp_getbindtoken &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-getbindtoken-transact-sql.md)   
 [sp_bindsession &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-bindsession-transact-sql.md)   
 [BULK INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/bulk-insert-transact-sql.md)   
 [READTEXT &#40;Transact-SQL&#41;](../../t-sql/queries/readtext-transact-sql.md)   
 [WRITETEXT &#40;Transact-SQL&#41;](../../t-sql/queries/writetext-transact-sql.md)   
 [UPDATETEXT &#40;Transact-SQL&#41;](../../t-sql/queries/updatetext-transact-sql.md)  
  
  
