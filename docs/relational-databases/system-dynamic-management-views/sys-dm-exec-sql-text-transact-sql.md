---
title: sys.dm_exec_sql_text (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 10/20/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- dm_exec_sql_text
- sys.dm_exec_sql_text
- sys.dm_exec_sql_text_TSQL
- dm_exec_sql_text_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_exec_sql_text dynamic management function
ms.assetid: 61b8ad6a-bf80-490c-92db-58dfdff22a24
caps.latest.revision: 36
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 21b22b837cc4e46bdd5169b0c669e7dde74c029c
ms.sourcegitcommit: 7019ac41524bdf783ea2c129c17b54581951b515
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/23/2018
---
# <a name="sysdmexecsqltext-transact-sql"></a>sys.dm_exec_sql_text (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Retorna o texto do SQL em lote que é identificado pelo especificado *sql_handle*. Essa função com valor de tabela substitui a função de sistema **fn_get_sql**.  
  
 
## <a name="syntax"></a>Sintaxe  
  
```  
sys.dm_exec_sql_text(sql_handle | plan_handle)  
```  
  
## <a name="arguments"></a>Argumentos  
*sql_handle*  
É o identificador SQL do lote a ser pesquisado. *sql_handle* é **varbinary(64)**. *sql_handle* pode ser obtido dos seguintes objetos de gerenciamento dinâmico:  
  
-   [sys.dm_exec_query_stats](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-stats-transact-sql.md)  
  
-   [sys.dm_exec_requests](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)  
  
-   [sys.dm_exec_cursors](../../relational-databases/system-dynamic-management-views/sys-dm-exec-cursors-transact-sql.md)  
  
-   [sys.dm_exec_xml_handles](../../relational-databases/system-dynamic-management-views/sys-dm-exec-xml-handles-transact-sql.md)  
  
-   [sys.dm_exec_query_memory_grants](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-memory-grants-transact-sql.md)  
  
-   [sys.dm_exec_connections](../../relational-databases/system-dynamic-management-views/sys-dm-exec-connections-transact-sql.md)  
  
*plan_handle*  
Identifica exclusivamente um plano de consulta para um lote em cache ou sendo executado atualmente. *plan_handle* é **varbinary(64)**. *plan_handle* pode ser obtido dos seguintes objetos de gerenciamento dinâmico:  
  
-   [sys.dm_exec_cached_plans](../../relational-databases/system-dynamic-management-views/sys-dm-exec-cached-plans-transact-sql.md)  
  
-   [sys.dm_exec_query_stats](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-stats-transact-sql.md)  
  
-   [sys.dm_exec_requests](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)   
  
## <a name="table-returned"></a>Tabela retornada  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**dbid**|**smallint**|ID do banco de dados.<br /><br /> Para instruções SQL preparadas e ad hoc, a ID do banco de dados no qual as instruções foram compiladas.|  
|**objectid**|**Int**|ID do objeto.<br /><br /> É NULL para instruções SQL ad hoc e preparadas.|  
|**number**|**smallint**|Para um procedimento armazenado numerado, esta coluna retorna o número do procedimento armazenado. Para obter mais informações, consulte [numbered_procedures &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-numbered-procedures-transact-sql.md).<br /><br /> É NULL para instruções SQL ad hoc e preparadas.|  
|**Criptografado**|**bit**|1 = O texto SQL é criptografado.<br /><br /> 0 = O texto SQL não é criptografado.|  
|**text**|**nvarchar(max** **)**|Texto da consulta SQL.<br /><br /> É NULL para objetos criptografados.|  
  
## <a name="permissions"></a>Permissões  
 Requer a permissão `VIEW SERVER STATE` no servidor.  
  
## <a name="remarks"></a>Remarks  
Para consultas ad hoc, os identificadores SQL são valores de hash com base no texto SQL que está sendo enviado ao servidor e podem se originar de qualquer banco de dados. 

Para objetos de banco de dados como procedimentos armazenados, gatilhos ou funções, os identificadores SQL são derivados da ID de banco de dados, da ID de objeto e do número de objeto. 

Identificador de plano é um valor de hash derivado do plano compilado do lote inteiro. 

> [!NOTE]
> **DBID** não pode ser determinada *sql_handle* para consultas ad hoc. Para determinar **dbid** para consultas ad hoc, use *plan_handle* em vez disso.
  
## <a name="examples"></a>Exemplos 

### <a name="a-conceptual-example"></a>A. Exemplo conceitual
A seguir está um exemplo básico para ilustrar passando um **sql_handle** diretamente ou com **CROSS APPLY**.
  1.  Crie uma atividade.  
Execute o T-SQL a seguir em uma nova janela de consulta em [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].   
      ```sql
      -- Identify current spid (session_id)
      SELECT @@SPID;
      GO
  
      -- Create activity
        WAITFOR DELAY '00:02:00';
      ```
      
    2.  Usando **CROSS APPLY**.  
    O sql_handle do **exec_requests** será passado para **dm_exec_sql_text** usando **CROSS APPLY**. Abra uma nova janela de consulta e passar o spid identificado na etapa 1. Neste exemplo, o spid é `59`.

        ```sql
        SELECT t.*
        FROM sys.dm_exec_requests AS r
        CROSS APPLY sys.dm_exec_sql_text(r.sql_handle) AS t
        WHERE session_id = 59 -- modify this value with your actual spid
         ```      
 
    2.  Passando **sql_handle** diretamente.  
Adquirir o **sql_handle** de **exec_requests**. Em seguida, passe o **sql_handle** diretamente para **dm_exec_sql_text**. Abra uma nova janela de consulta e passar o spid identificado na etapa 1 para **exec_requests**. Neste exemplo, o spid é `59`. Em seguida, passe retornado **sql_handle** como um argumento para **dm_exec_sql_text**.

        ```sql
        -- acquire sql_handle
        SELECT sql_handle FROM sys.dm_exec_requests WHERE session_id = 59  -- modify this value with your actual spid
        
        -- pass sql_handle to sys.dm_exec_sql_text
        SELECT * FROM sys.dm_exec_sql_text(0x01000600B74C2A1300D2582A2100000000000000000000000000000000000000000000000000000000000000) -- modify this value with your actual sql_handle
         ```      
    
  
### <a name="b-obtain-information-about-the-top-five-queries-by-average-cpu-time"></a>B. Obter informações sobre as cinco principais consultas por tempo médio de CPU  
 O exemplo a seguir retorna o texto da instrução SQL e o tempo médio de CPU das cinco primeiras consultas.  
  
```sql  
SELECT TOP 5 total_worker_time/execution_count AS [Avg CPU Time],  
    SUBSTRING(st.text, (qs.statement_start_offset/2)+1,   
        ((CASE qs.statement_end_offset  
          WHEN -1 THEN DATALENGTH(st.text)  
         ELSE qs.statement_end_offset  
         END - qs.statement_start_offset)/2) + 1) AS statement_text  
FROM sys.dm_exec_query_stats AS qs  
CROSS APPLY sys.dm_exec_sql_text(qs.sql_handle) AS st  
ORDER BY total_worker_time/execution_count DESC;  
```  
  
### <a name="c-provide-batch-execution-statistics"></a>C. Fornecem estatísticas de execução em lotes  
 O exemplo a seguir retorna o texto de consultas SQL que estão sendo executadas em lotes e fornece informações estatísticas sobre elas.  
  
```sql  
SELECT s2.dbid,   
    s1.sql_handle,    
    (SELECT TOP 1 SUBSTRING(s2.text,statement_start_offset / 2+1 ,   
      ( (CASE WHEN statement_end_offset = -1   
         THEN (LEN(CONVERT(nvarchar(max),s2.text)) * 2)   
         ELSE statement_end_offset END)  - statement_start_offset) / 2+1))  AS sql_statement,  
    execution_count,   
    plan_generation_num,   
    last_execution_time,     
    total_worker_time,   
    last_worker_time,   
    min_worker_time,   
    max_worker_time,  
    total_physical_reads,   
    last_physical_reads,   
    min_physical_reads,    
    max_physical_reads,    
    total_logical_writes,   
    last_logical_writes,   
    min_logical_writes,   
    max_logical_writes    
FROM sys.dm_exec_query_stats AS s1   
CROSS APPLY sys.dm_exec_sql_text(sql_handle) AS s2    
WHERE s2.objectid is null   
ORDER BY s1.sql_handle, s1.statement_start_offset, s1.statement_end_offset;  
```  
  
## <a name="see-also"></a>Consulte também  
 [Exibições e funções de gerenciamento dinâmico &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Funções e exibições de gerenciamento dinâmico relacionadas à execução &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/execution-related-dynamic-management-views-and-functions-transact-sql.md)   
 [sys.dm_exec_query_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-stats-transact-sql.md)   
 [sys.dm_exec_requests &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)   
 [sys.dm_exec_cursors &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-cursors-transact-sql.md)   
 [sys.dm_exec_xml_handles &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-xml-handles-transact-sql.md)   
 [sys.dm_exec_query_memory_grants &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-memory-grants-transact-sql.md)   
 [Usando APPLY](../../t-sql/queries/from-transact-sql.md#using-apply)   
 [sys.dm_exec_text_query_plan &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-text-query-plan-transact-sql.md)  

