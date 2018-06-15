---
title: Monitorando o desempenho de procedimentos armazenados compilados nativamente | Microsoft Docs
ms.custom: ''
ms.date: 04/03/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: in-memory-oltp
ms.reviewer: ''
ms.suite: sql
ms.technology: in-memory-oltp
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 55548cb2-77a8-4953-8b5a-f2778a4f13cf
caps.latest.revision: 11
author: CarlRabeler
ms.author: carlrab
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: d62096acba1d44cfa15af8ae6028ec2b756a117c
ms.sourcegitcommit: ee661730fb695774b9c483c3dd0a6c314e17ddf8
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/19/2018
ms.locfileid: "34330557"
---
# <a name="monitoring-performance-of-natively-compiled-stored-procedures"></a>Monitorando o desempenho de procedimentos armazenados compilados nativamente
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  Este artigo discute como é possível monitorar o desempenho de procedimentos armazenados e de outros módulos T-SQL, ambos compilados nativamente.  
  
## <a name="using-extended-events"></a>Usando eventos estendidos  
 Use o evento estendido **sp_statement_completed** para rastrear a execução de uma consulta. Crie uma sessão de evento estendido com esse evento, opcionalmente com um filtro no object_id para um procedimento armazenado específico compilado nativamente. O evento estendido é ativado depois da execução de cada consulta. O tempo de CPU e a duração relatados pelo evento estendido indicam a quantidade de CPU usada pela consulta e o tempo de execução. Um procedimento armazenado compilado de modo nativo que usa muito tempo da CPU pode ter problemas de desempenho.  
  
 **line_number**junto com **object_id** no evento estendido pode ser usado para investigar a consulta. A consulta a seguir pode ser usada para recuperar a definição de procedimento. O número da linha pode ser usado para identificar a consulta na definição:  
  
```sql  
select [definition] from sys.sql_modules where object_id=object_id  
```  
  
 Para obter mais informações sobre o evento estendido **sp_statement_completed** , consulte [Como recuperar a instrução que gerou um evento](http://blogs.msdn.com/b/extended_events/archive/2010/05/07/making-a-statement-how-to-retrieve-the-t-sql-statement-that-caused-an-event.aspx).  
  
## <a name="using-data-management-views-and-query-store"></a>Usando exibições de gerenciamento de dados e Repositório de Consultas
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e [!INCLUDE[ssSDS](../../includes/sssds-md.md)] dão suporte à coleta de estatísticas de execução para procedimentos armazenados compilados nativamente, nos níveis de procedimento e de consulta. Coletar estatísticas de execução não está habilitado por padrão devido ao impacto sobre o desempenho.  

As estatísticas de execução são refletidas nas exibições do sistema [sys.dm_exec_procedure_stats](../../relational-databases/system-dynamic-management-views/sys-dm-exec-procedure-stats-transact-sql.md) e [sys.dm_exec_query_stats](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-stats-transact-sql.md), bem como no [Repositório de Consultas](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md).

### <a name="enabling-procedure-level-execution-statistics-collection"></a>Habilitando a coleta de estatísticas de execução de nível de procedimento

**[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]**: habilite ou desabilite a coleta de estatísticas em procedimentos armazenados compilados nativamente no nível de procedimento usando [sys.sp_xtp_control_proc_exec_stats &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-xtp-control-proc-exec-stats-transact-sql.md).  A instrução a seguir permite a coleta de estatísticas de execução de nível de procedimento para todos os módulos T-SQL compilados nativamente na instância atual:
```sql
EXEC sys.sp_xtp_control_proc_exec_stats 1
```

**[!INCLUDE[ssSDSFull](../../includes/sssdsfull-md.md)]**: habilite ou desabilite a coleta de estatísticas em procedimentos armazenados compilados nativamente no nível de procedimento usando a opção [configuração com a configuração de escopo do banco de dados](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md) `XTP_PROCEDURE_EXECUTION_STATISTICS`. A instrução a seguir permite a coleta de estatísticas de execução de nível de procedimento para todos os módulos T-SQL compilados nativamente no banco de dados atual:
```sql
ALTER DATABASE SCOPED CONFIGURATION SET XTP_PROCEDURE_EXECUTION_STATISTICS = ON
```

### <a name="enabling-query-level-execution-statistics-collection"></a>Habilitando a coleta de estatísticas de execução de nível de consulta

**[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]**: habilite ou desabilite a coleta de estatísticas em procedimentos armazenados compilados nativamente no nível de consulta usando [sys.sp_xtp_control_query_exec_stats &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-xtp-control-query-exec-stats-transact-sql.md).  A instrução a seguir permite a coleta de estatísticas de execução de nível de consulta para todos os módulos T-SQL compilados nativamente na instância atual:
```sql
EXEC sys.sp_xtp_control_query_exec_stats 1
```

**[!INCLUDE[ssSDSFull](../../includes/sssdsfull-md.md)]**: habilite ou desabilite a coleta de estatísticas em procedimentos armazenados compilados nativamente no nível de instrução usando a opção [configuração com a configuração de escopo do banco de dados](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md) `XTP_QUERY_EXECUTION_STATISTICS`. A instrução a seguir permite a coleta de estatísticas de execução de nível de consulta para todos os módulos T-SQL compilados nativamente no banco de dados atual:
```sql
ALTER DATABASE SCOPED CONFIGURATION SET XTP_QUERY_EXECUTION_STATISTICS = ON
```

## <a name="sample-queries"></a>Consultas de exemplo

 Depois que você coletar estatísticas, as estatísticas de execução de procedimentos armazenados compilados de modo nativo poderão ser consultadas para um procedimento com [sys.dm_exec_procedure_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-procedure-stats-transact-sql.md) e para consultas com [sys.dm_exec_query_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-stats-transact-sql.md).  
 
  
 A seguinte consulta retorna os nomes de procedimento e as estatísticas de execução para procedimentos armazenados compilados de modo nativo no banco de dados atual, após a coleta de estatísticas:  
  
```sql  
select object_id,  
       object_name(object_id) as 'object name',  
       cached_time,  
       last_execution_time,  
       execution_count,  
       total_worker_time,  
       last_worker_time,  
       min_worker_time,  
       max_worker_time,  
       total_elapsed_time,  
       last_elapsed_time,  
       min_elapsed_time,  
       max_elapsed_time   
from sys.dm_exec_procedure_stats  
where database_id=db_id() and object_id in (select object_id   
from sys.sql_modules where uses_native_compilation=1)  
order by total_worker_time desc  
```  
  
 A seguinte consulta retorna o texto da consulta, bem como as estatísticas de execução para todas as consultas em procedimentos armazenados compilados de modo nativo no banco de dados atual, para as quais as estatísticas foram coletadas, ordenadas pelo tempo de trabalho total, em ordem decrescente:  
  
```sql  
select st.objectid,   
       object_name(st.objectid) as 'object name',   
       SUBSTRING(st.text, (qs.statement_start_offset/2) + 1, ((qs.statement_end_offset-qs.statement_start_offset)/2) + 1) as 'query text',   
       qs.creation_time,  
       qs.last_execution_time,  
       qs.execution_count,  
       qs.total_worker_time,  
       qs.last_worker_time,  
       qs.min_worker_time,  
       qs.max_worker_time,  
       qs.total_elapsed_time,  
       qs.last_elapsed_time,  
       qs.min_elapsed_time,  
       qs.max_elapsed_time  
from sys.dm_exec_query_stats qs cross apply sys.dm_exec_sql_text(sql_handle) st  
where  st.dbid=db_id() and st.objectid in (select object_id   
from sys.sql_modules where uses_native_compilation=1)  
order by qs.total_worker_time desc  
```  

## <a name="query-execution-plans"></a>Planos de execução de consulta

 Os procedimentos armazenados compilados de modo nativo dão suporte ao SHOWPLAN_XML (plano de execução estimado). O plano de execução estimado pode ser usado para inspecionar o plano de consulta, para localizar quaisquer problemas de plano incorreto. As razões comuns de planos incorretos são:  
  
-   As estatísticas não foram atualizadas antes da criação do procedimento.  
  
-   Índices ausentes  
  
 O plano de execução XML é obtido executando o seguinte [!INCLUDE[tsql](../../includes/tsql-md.md)]:  
  
```sql  
SET SHOWPLAN_XML ON  
GO  
EXEC my_proc   
GO  
SET SHOWPLAN_XML OFF  
GO  
```  
  
 Como alternativa, no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], selecione o nome do procedimento e clique em **Exibir Plano de Execução Estimado**.  
  
 O plano de execução estimado para procedimentos armazenados compilados de modo nativo mostra os operadores e as expressões para as consultas no procedimento. [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] não dá suporte a todos os atributos SHOWPLAN_XML para procedimentos armazenados compilados de modo nativo. Por exemplo, os atributos relacionados ao cálculo de custos do otimizador de consulta não fazem parte do SHOWPLAN_XML para o procedimento.  
  
## <a name="see-also"></a>Consulte Também  
 [Procedimentos armazenados compilados nativamente](../../relational-databases/in-memory-oltp/natively-compiled-stored-procedures.md)  
  
  
