---
title: Classe de evento Background Job Error | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- Background Job Error event class
ms.assetid: 9e6d2a0e-919d-4fe2-a306-b20b8d41c197
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 5689c86e530fd7bf7f78cb58f3e1e53f9b731bc3
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62686829"
---
# <a name="background-job-error-event-class"></a>classe de evento Background Job Error
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  A classe de evento **Background Job Error** ocorre quando um trabalho em segundo plano é encerrado de maneira anormal. Essa condição pode exigir a atenção de um administrador do sistema.  
  
## <a name="background-job-error-event-class-data-columns"></a>Colunas de dados da classe de evento Background Job Error  
  
|Nome da coluna de dados|Tipo de dados|Descrição|ID da coluna|Filtrável|  
|----------------------|---------------|-----------------|---------------|----------------|  
|**DatabaseID**|**int**|ID do banco de dados especificado pelo trabalho. Determine o valor para um banco de dados usando a função DB_ID.|3|Sim|  
|**DatabaseName**|**nvarchar**|Nome do banco de dados no qual a instrução do usuário está sendo executada.|35|Sim|  
|**Erro**|**int**|Número de erro da última tentativa (**EventSubClass** 1, apenas).|31|Sim|  
|**EventClass**|**int**|Tipo de evento = 193.|27|Não|  
|**EventSequence**|**int**|A sequência de determinado evento dentro da solicitação.|51|Não|  
|**EventSubClass**|**int**|Tipo de subclasse de evento.<br /><br /> 1 = Trabalho em segundo plano encerrado após falha.<br /><br /> 2 = Trabalho em segundo plano descartado — a fila está cheia.<br /><br /> 3 = Trabalho em segundo plano retornou erro.|21|Sim|  
|**IndexID**|**int**|ID do índice no objeto afetado pelo evento. Para determinar a ID do índice de um objeto, use a coluna **indid** da tabela do sistema **sysindexes** .|24|Sim|  
|**IntegerData**|**int**|Número de tentativas feitas pelo trabalho (**EventSubClass** 1, apenas).|25|Sim|  
|**IntegerData2**|**int**|Número de sequência do trabalho.|55|Sim|  
|**ObjectID**|**int**|ID de objeto atribuída pelo sistema.|22|Sim|  
|**SessionLoginName**|**nvarchar**|Nome de logon do usuário que originou a sessão. Por exemplo, para se conectar ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando o Logon1 e executar uma instrução como Logon2, o **SessionLoginName** mostrará o Logon1 e o **LoginName** mostrará o Logon2. Esta coluna exibe os logons do Windows [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e [!INCLUDE[msCoName](../../includes/msconame-md.md)] .|64|Sim|  
|**Severity**|**int**|Nível de severidade do erro na última tentativa (**EventSubClass** 1, apenas).|20|Sim|  
|**StartTime**|**datetime**|Hora em que o trabalho foi criado.|14|Sim|  
|**Estado**|**int**|Estado do erro na última tentativa (**EventSubClass** 1, apenas).|30|Sim|  
|**TextData**|**ntext**|Texto descritivo do valor de subclasse do evento.|1|Sim|  
|**Tipo**|**int**|Tipo de trabalho.|57|Sim|  
  
## <a name="see-also"></a>Consulte Também  
 [Eventos estendidos](../../relational-databases/extended-events/extended-events.md)   
 [sp_trace_setevent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql.md)   
 [Classe de evento Auto Stats](../../relational-databases/event-classes/auto-stats-event-class.md)  
  
  
