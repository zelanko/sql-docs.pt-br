---
title: Categoria de evento de erros e de avisos
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- Errors and Warnings event category [SQL Server]
- SQL Server event classes, Errors and Warnings event category
- event classes [SQL Server], Errors and Warnings event category
ms.assetid: 249c19b5-af68-4433-80f6-337395176641
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 4832910f00322875c334e16df77975a33106d214
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/01/2020
ms.locfileid: "74056420"
---
# <a name="errors-and-warnings-event-category-database-engine"></a>Categoria de eventos de erros e de avisos (Mecanismo de Banco de Dados)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  A categoria de evento **Errors and Warnings** contém eventos de erros gerais e advertências.  
  
## <a name="in-this-section"></a>Nesta seção  
  
|Tópico|DESCRIÇÃO|  
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
  
## <a name="see-also"></a>Consulte Também  
 [sp_trace_setevent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql.md)  
  
  
