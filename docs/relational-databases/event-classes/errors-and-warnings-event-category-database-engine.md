---
title: Categoria de eventos de erros e de avisos (Mecanismo de Banco de Dados) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: event-classes
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Errors and Warnings event category [SQL Server]
- SQL Server event classes, Errors and Warnings event category
- event classes [SQL Server], Errors and Warnings event category
ms.assetid: 249c19b5-af68-4433-80f6-337395176641
caps.latest.revision: "28"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: bdac2740a2db73a3cf548b37c288b8dd203ed46d
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="errors-and-warnings-event-category-database-engine"></a>Categoria de eventos de erros e de avisos (Mecanismo de Banco de Dados)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)] A categoria de evento **Errors and Warnings** contém eventos de erros gerais e advertências.  
  
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
  
  
