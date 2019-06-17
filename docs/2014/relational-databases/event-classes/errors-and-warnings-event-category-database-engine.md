---
title: Categoria de eventos de erros e de avisos (Mecanismo de Banco de Dados) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
topic_type:
- apiref
helpviewer_keywords:
- Errors and Warnings event category [SQL Server]
- SQL Server event classes, Errors and Warnings event category
- event classes [SQL Server], Errors and Warnings event category
ms.assetid: 249c19b5-af68-4433-80f6-337395176641
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: b86b68b0e7273a275c8dd1bd00fe99a7c462a27d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62662622"
---
# <a name="errors-and-warnings-event-category-database-engine"></a>Categoria de eventos de erros e de avisos (Mecanismo de Banco de Dados)
  A categoria de evento **Errors and Warnings** contém eventos de erros gerais e advertências.  
  
## <a name="in-this-section"></a>Nesta seção  
  
|Tópico|Descrição|  
|-----------|-----------------|  
|[Classe de evento Attention](attention-event-class.md)|Indica que ocorreu um evento **Atenção** .|  
|[Classe de evento Background Job Error](background-job-error-event-class.md)|Indica que uma tarefa em segundo plano terminou de forma anormal.|  
|[Classe de evento Bitmap Warning](bitmap-warning-event-class.md)|Indica que a filtragem de bitmap foi desabilitada em uma consulta.|  
|[Classe de evento Blocked Process Report](blocked-process-report-event-class.md)|Indica que uma tarefa foi bloqueada para mais do que um período de tempo especificado.|  
|[Classe de evento CPU Threshold Exceeded](cpu-threshold-exceeded-event-class.md)|Indica que o gerenciador de recursos detecta uma consulta que excede o limite de CPU especificado.|  
|[Classe de evento ErrorLog](errorlog-event-class.md)|Indica que eventos de erro foram registrados no log de erros do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .|  
|[Classe de evento EventLog](eventlog-event-class.md)|Indica que eventos foram registrados no log de eventos do Windows.|  
|[Classe de evento Exception](exception-event-class.md)|Indica que uma exceção ocorreu no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|[Classe de evento Exchange Spill](exchange-spill-event-class.md)|Indica que os buffers de comunicação em um plano de consulta paralelo foram gravados no banco de dados tempdb.|  
|[Classe de evento Execution Warnings](execution-warnings-event-class.md)|Indica que ocorreram advertências de concessão de memória durante a execução de uma instrução ou um procedimento armazenado do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .|  
|[Classe de evento Hash Warning](hash-warning-event-class.md)|Indica que ocorreu uma recursão de hash ou abandono de hash durante uma operação de hash.|  
|[Classe de evento Missing Column Statistics](missing-column-statistics-event-class.md)|Indica que estatísticas de coluna que podem ter sido úteis para o otimizador não estão disponíveis.|  
|[Classe de evento Missing Join Predicate](missing-join-predicate-event-class.md)|Indica que uma consulta que está sendo executada não tem nenhum predicado de junção.|  
|[Classe de evento Sort Warnings](sort-warnings-event-class.md)|Indica que operações de classificação não cabem na memória.|  
|[Classe de evento User Error Message](user-error-message-event-class.md)|Exibe mensagens de erro que são vistas pelo usuário.|  
  
## <a name="see-also"></a>Consulte também  
 [sp_trace_setevent &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql)  
  
  
