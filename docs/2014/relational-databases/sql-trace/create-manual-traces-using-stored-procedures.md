---
title: Criar rastreamentos manuais usando procedimentos armazenados | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
ms.assetid: f6f47fa2-7c17-41d4-9f69-9be144d56832
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 129d5c1104d2e2b05df6f484364b1fdfa12fcc9e
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48052006"
---
# <a name="create-manual-traces-using-stored-procedures"></a>Criar rastreamentos manuais usando procedimentos armazenados
  O Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] fornece procedimentos armazenados do sistema [!INCLUDE[tsql](../../includes/tsql-md.md)] para criar rastreamentos em uma instância do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]. Esses procedimentos armazenados do sistema podem ser usados nos seus próprios aplicativos para criar rastreamentos manualmente em vez de usar o [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]. Isso lhe permite escrever aplicativos personalizados específicos às necessidades de sua empresa.  
  
## <a name="in-this-section"></a>Nesta seção  
 A tabela a seguir lista os procedimentos armazenados do sistema para rastreamento de uma instância do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)].  
  
|Procedimento armazenado|Tarefa executada|  
|----------------------|--------------------|  
|[sys.fn_trace_geteventinfo &#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/sys-fn-trace-geteventinfo-transact-sql)|Retorna informações sobre eventos incluídos em um rastreamento.|  
|[sys.fn_trace_getinfo &#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/sys-fn-trace-getinfo-transact-sql)|Retorna informações sobre um rastreamento especificado ou todos os rastreamentos existentes.|  
|[sp_trace_create &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-trace-create-transact-sql)|Cria uma definição de rastreamento. O rastreamento novo estará em um estado interrompido.|  
|[sp_trace_generateevent &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-trace-generateevent-transact-sql)|Cria um evento definido pelo usuário.|  
|[sp_trace_setevent &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql)|Adiciona ou remove uma classe de evento ou coluna de dados de um rastreamento.|  
|[sp_trace_setstatus &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-trace-setstatus-transact-sql)|Inicia, interrompe ou encerra um rastreamento.|  
|[sys.fn_trace_getfilterinfo &#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/sys-fn-trace-getfilterinfo-transact-sql)|Retorna informações sobre filtros aplicados a um rastreamento.|  
|[sp_trace_setfilter &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-trace-setfilter-transact-sql)|Aplica um filtro novo ou modificado a um rastreamento.|  
  
 **Para definir seu próprio rastreamento usando procedimentos armazenados**  
  
1.  Especifique os eventos a serem capturados usando **sp_trace_setevent**.  
  
2.  Especifique qualquer filtro de evento. Para obter mais informações, veja [Definir um filtro de rastreamento #40;Transact-SQL&#41;](../../ssms/agent/set-sql-server-alias-for-sql-server-agent-service-ssms.md).  
  
3.  Especifique o destino para os dados do evento capturado usando **sp_trace_create**.  
  
 Para obter um exemplo de como usar procedimentos armazenados de rastreamento, veja [Criar um rastreamento &#40;Transact-SQL&#41;](../sql-trace/create-a-trace-transact-sql.md).  
  
 **Para definir padrões de definição de rastreamento**  
  
 [SQL Server Profiler](../../tools/sql-server-profiler/sql-server-profiler.md)  
  
 **Para definir padrões de exibição de rastreamento**  
  
 [SQL Server Profiler](../../tools/sql-server-profiler/set-trace-display-defaults-sql-server-profiler.md)  
  
 **Para criar um rastreamento**  
  
 [SQL Server Profiler](../../tools/sql-server-profiler/create-a-trace-sql-server-profiler.md)  
  
 [Transact-SQL](../sql-trace/create-a-trace-transact-sql.md)  
  
 **Para adicionar ou remover eventos de um modelo de rastreamento**  
  
 [SQL Server Profiler](../../tools/sql-server-profiler/specify-events-and-data-columns-for-a-trace-file-sql-server-profiler.md)  
  
 [Transact-SQL](/sql/relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql)  
  
  
