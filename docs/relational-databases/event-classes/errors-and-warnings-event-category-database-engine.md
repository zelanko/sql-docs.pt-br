---
title: Categoria de eventos de erros e de avisos (Mecanismo de Banco de Dados) | Microsoft Docs
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
- Errors and Warnings event category [SQL Server]
- SQL Server event classes, Errors and Warnings event category
- event classes [SQL Server], Errors and Warnings event category
ms.assetid: 249c19b5-af68-4433-80f6-337395176641
caps.latest.revision: 28
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: b0c7673b15dec984e81cc7dd8207006a0b278fe7
ms.contentlocale: pt-br
ms.lasthandoff: 04/11/2017

---
# <a name="errors-and-warnings-event-category-database-engine"></a>Categoria de eventos de erros e de avisos (Mecanismo de Banco de Dados)
  A categoria de evento **Errors and Warnings** contém eventos de erros gerais e advertências.  
  
## <a name="in-this-section"></a>Nesta seção  
  
|Tópico|Descrição|  
|-----------|-----------------|  
|[Classe de evento Attention](../../relational-databases/event-classes/attention-event-class.md)|Indica que ocorreu um evento **Atenção** .|  
|[Classe de evento Background Job Error](../../relational-databases/event-classes/background-job-error-event-class.md)|Indica que uma tarefa em segundo plano terminou de forma anormal.|  
|[Classe de evento Bitmap Warning](../../relational-databases/event-classes/bitmap-warning-event-class.md)|Indica que a filtragem de bitmap foi desabilitada em uma consulta.|  
|[Classe de evento Blocked Process Report](../../relational-databases/event-classes/blocked-process-report-event-class.md)|Indica que uma tarefa foi bloqueada para mais do que um período de tempo especificado.|  
|[Classe de evento CPU Threshold Exceeded](../../relational-databases/event-classes/cpu-threshold-exceeded-event-class.md)|Indica que o gerenciador de recursos detecta uma consulta que excede o limite de CPU especificado.|  
|[Classe de evento ErrorLog](../../relational-databases/event-classes/errorlog-event-class.md)|Indica que eventos de erro foram registrados no log de erros do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .|  
|[Classe de evento EventLog](../../relational-databases/event-classes/eventlog-event-class.md)|Indica que eventos foram registrados no log de eventos do Windows.|  
|[Classe de evento Exception](../../relational-databases/event-classes/exception-event-class.md)|Indica que uma exceção ocorreu no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|[Classe de evento Exchange Spill](../../relational-databases/event-classes/exchange-spill-event-class.md)|Indica que os buffers de comunicação em um plano de consulta paralelo foram gravados no banco de dados tempdb.|  
|[Classe de evento Execution Warnings](../../relational-databases/event-classes/execution-warnings-event-class.md)|Indica que ocorreram advertências de concessão de memória durante a execução de uma instrução ou um procedimento armazenado do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .|  
|[Classe de evento Hash Warning](../../relational-databases/event-classes/hash-warning-event-class.md)|Indica que ocorreu uma recursão de hash ou abandono de hash durante uma operação de hash.|  
|[Classe de evento Missing Column Statistics](../../relational-databases/event-classes/missing-column-statistics-event-class.md)|Indica que estatísticas de coluna que podem ter sido úteis para o otimizador não estão disponíveis.|  
|[Classe de evento Missing Join Predicate](../../relational-databases/event-classes/missing-join-predicate-event-class.md)|Indica que uma consulta que está sendo executada não tem nenhum predicado de junção.|  
|[Classe de evento Sort Warnings](../../relational-databases/event-classes/sort-warnings-event-class.md)|Indica que operações de classificação não cabem na memória.|  
|[Classe de evento User Error Message](../../relational-databases/event-classes/user-error-message-event-class.md)|Exibe mensagens de erro que são vistas pelo usuário.|  
  
## <a name="see-also"></a>Consulte também  
 [sp_trace_setevent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql.md)  
  
  
