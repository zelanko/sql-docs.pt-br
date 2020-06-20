---
title: Classe de evento FT:Crawl Started | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
topic_type:
- apiref
helpviewer_keywords:
- Crawl Started event class
ms.assetid: 2535b856-97e8-4fb2-8ba0-5d5446355fa6
author: stevestein
ms.author: sstein
ms.openlocfilehash: 0a3dbaa76fcc54bf35b72d0a81efce479be51974
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85029645"
---
# <a name="ftcrawl-started-event-class"></a>Classe de evento FT:Crawl Started
  A classe de evento **FT:Crawl Started** indica que um rastreamento de texto completo (população) foi iniciado. Use essa classe de evento para verificar se uma solicitação de rastreamento está sendo atualmente acolhida por tarefas de trabalho.  
  
## <a name="ft-crawl-started-event-class-data-columns"></a>Colunas de dados da classe de evento FT:Crawl Started  
  
|Nome da coluna de dados|Tipo de dados|DESCRIÇÃO|ID da coluna|Filtrável|  
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
  
## <a name="see-also"></a>Consulte Também  
 [sp_trace_setevent &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql)  
  
  
