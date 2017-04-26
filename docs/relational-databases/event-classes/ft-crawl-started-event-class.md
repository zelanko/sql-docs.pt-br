---
title: Classe de evento FT:Crawl Started | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Crawl Started event class
ms.assetid: 2535b856-97e8-4fb2-8ba0-5d5446355fa6
caps.latest.revision: 28
author: BYHAM
ms.author: rickbyh
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 309fa5de7dd158c0b013d305623bc4a409776912
ms.lasthandoff: 04/11/2017

---
# <a name="ftcrawl-started-event-class"></a>Classe de evento FT:Crawl Started
  A classe de evento **FT:Crawl Started** indica que um rastreamento de texto completo (população) foi iniciado. Use essa classe de evento para verificar se uma solicitação de rastreamento está sendo atualmente acolhida por tarefas de trabalho.  
  
## <a name="ft-crawl-started-event-class-data-columns"></a>Colunas de dados da classe de evento FT:Crawl Started  
  
|Nome da coluna de dados|Tipo de dados|Descrição|ID da coluna|Filtrável|  
|----------------------|---------------|-----------------|---------------|----------------|  
|**DatabaseID**|**int**|ID do banco de dados no qual o rastreamento de texto completo foi iniciado. Determine o valor para um banco de dados usando a função DB_ID.|3|Sim|  
|**EventClass**|**int**|Tipo de evento = 155.|27|Não|  
|**EventSequence**|**int**|Sequência de um determinado evento na solicitação.|51|Não|  
|**IsSystem**|**int**|Indica se o evento ocorreu em um processo do sistema ou do usuário. 1 = sistema, 0 = usuário.|60|Sim|  
|**ObjectID**|**int**|ID de objeto atribuída pelo sistema. O rastreamento de texto completo foi iniciado no índice de texto completo neste objeto.|22|Sim|  
|**SessionLoginName**|**nvarchar**|Nome de logon do usuário que originou a sessão. Por exemplo, para se conectar ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando o Logon1 e executar uma instrução como Logon2, o **SessionLoginName** mostrará o Logon1 e o **LoginName** mostrará o Logon2. Esta coluna exibe os logons do Windows [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e [!INCLUDE[msCoName](../../includes/msconame-md.md)] .|64|Sim|  
|**SPID**|**int**|Identificação da sessão em que ocorreu o evento.|12|Sim|  
|**StartTime**|**datetime**|Hora de início do evento, se disponível.|14|Sim|  
|**TextData**|**ntext**|Tipo de rastreamento de texto completo. O valor pode ser Full (Completo), Incremental, Manual ou Auto (Automático).|1|Sim|  
|**TransactionID**|**bigint**|ID da transação atribuída pelo sistema.|4|Sim|  
  
## <a name="see-also"></a>Consulte também  
 [sp_trace_setevent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql.md)  
  
  
