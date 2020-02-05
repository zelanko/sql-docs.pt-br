---
title: DMVs – estatísticas de uso e desempenho de exibições
description: Usar DMVs para determinar estatísticas de uso e o desempenho das exibições
ms.custom: seo-dt-2019
author: julieMSFT
ms.author: jrasnick
ms.date: 09/27/2018
ms.prod: sql
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
ms.openlocfilehash: e80ba0a8252881b7447dda721f02fc9c3e545917
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/01/2020
ms.locfileid: "74165889"
---
# <a name="use-dmvs-to-determine-usage-statistics-and-performance-of-views"></a>Usar DMVs para determinar estatísticas de uso e o desempenho das exibições
Este artigo aborda a metodologia e os scripts usados para obter informações sobre o **desempenho de consultas que usam exibições**. A finalidade desses scripts é fornecer indicadores de uso e desempenho das diferentes exibições encontradas em um banco de dados. 

## <a name="sysdm_exec_query_optimizer_info"></a>sys.dm_exec_query_optimizer_info
O DMV [sys.dm_exec_query_optimizer_info](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-optimizer-info-transact-sql.md) expõe estatísticas sobre as otimizações realizadas pelo otimizador de consulta do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Esses valores são cumulativos e começam a gravar quando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é iniciado. Para obter mais informações sobre o otimizador de consulta, confira o [Guia da arquitetura de processamento de consultas](../../relational-databases/query-processing-architecture-guide.md).   

A CTE (common_table_expression) a seguir usa esse DMV para fornecer informações sobre a carga de trabalho, como o percentual de consultas que fazem referência a uma exibição. Os resultados retornados pela consulta não indicam um problema de desempenho por si só, mas podem expor problemas subjacentes quando combinados com reclamações de usuários sobre o desempenho lento de consultas. 

```sql
WITH CTE_QO AS
(
  SELECT
    occurrence
  FROM
    sys.dm_exec_query_optimizer_info
  WHERE
    ([counter] = 'optimizations')
),
QOInfo AS
(
  SELECT
    [counter]
    ,[%] = CAST((occurrence * 100.00)/(SELECT occurrence FROM CTE_QO) AS DECIMAL(5, 2))
  FROM
    sys.dm_exec_query_optimizer_info
  WHERE
    [counter] IN ('optimizations'
                  ,'trivial plan'
                  ,'no plan'
                  ,'search 0'
                  ,'search 1'
                  ,'search 2'
                  ,'timeout'
                  ,'memory limit exceeded'
                  ,'insert stmt'
                  ,'delete stmt'
                  ,'update stmt'
                  ,'merge stmt'
                  ,'contains subquery'
                  ,'view reference'
                  ,'remote query'
                  ,'dynamic cursor request'
                  ,'fast forward cursor request'
             )
)
SELECT
  [optimizations] AS [optimizations %]
  ,[trivial plan] AS [trivial plan %]
  ,[no plan] AS [no plan %]
  ,[search 0] AS [search 0 %]
  ,[search 1] AS [search 1 %]
  ,[search 2] AS [search 2 %]
  ,[timeout] AS [timeout %]
  ,[memory limit exceeded] AS [memory limit exceeded %]
  ,[insert stmt] AS [insert stmt %]
  ,[delete stmt] AS [delete stmt]
  ,[update stmt] AS [update stmt]
  ,[merge stmt] AS [merge stmt]
  ,[contains subquery] AS [contains subquery %]
  ,[view reference] AS [view reference %]
  ,[remote query] AS [remote query %]
  ,[dynamic cursor request] AS [dynamic cursor request %]
  ,[fast forward cursor request] AS [fast forward cursor request %]
FROM
  QOInfo
PIVOT (MAX([%]) FOR [counter] 
  IN ([optimizations]
      ,[trivial plan]
      ,[no plan]
      ,[search 0]
      ,[search 1]
      ,[search 2]
      ,[timeout]
      ,[memory limit exceeded]
      ,[insert stmt]
      ,[delete stmt]
      ,[update stmt]
      ,[merge stmt]
      ,[contains subquery]
      ,[view reference]
      ,[remote query]
      ,[dynamic cursor request]
      ,[fast forward cursor request])) AS p;
GO
```

Combine os resultados dessa consulta com os resultados da exibição do sistema [sys.views](../../relational-databases/system-catalog-views/sys-views-transact-sql.md) para identificar estatísticas de consulta, o texto da consulta e o plano de execução armazenado em cache. 

## <a name="sysviews"></a>sys.views
A CTE a seguir fornece informações sobre o número de execuções, o tempo total de execução e as páginas lidas da memória. Os resultados podem ser usados para identificar consultas que podem ser candidatos para otimização. 
  
> [!NOTE]
> Os resultados dessa consulta podem variar dependendo da versão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  


```sql
WITH CTE_VW_STATS AS
(
  SELECT
    SCHEMA_NAME(vw.schema_id) AS schemaname
    ,vw.name AS viewname
    ,vw.object_id AS viewid
  FROM
    sys.views AS vw
  WHERE
    (vw.is_ms_shipped = 0)
  INTERSECT
  SELECT
    SCHEMA_NAME(o.schema_id) AS schemaname
    ,o.Name AS name
    ,st.objectid AS viewid
  FROM
    sys.dm_exec_cached_plans cp
  CROSS APPLY
    sys.dm_exec_sql_text(cp.plan_handle) st
  INNER JOIN
    sys.objects o ON st.[objectid] = o.[object_id]
  WHERE
    st.dbid = DB_ID()
)
SELECT
  vw.schemaname
  ,vw.viewname
  ,vw.viewid
  ,DB_NAME(t.databaseid) AS databasename
  ,t.databaseid
  ,t.*
FROM
  CTE_VW_STATS AS vw
CROSS APPLY
  (
    SELECT
      st.dbid AS databaseid
      ,st.text
      ,qp.query_plan
      ,qs.*
    FROM
      sys.dm_exec_query_stats AS qs
    CROSS APPLY
      sys.dm_exec_sql_text(qs.plan_handle) AS st
    CROSS APPLY
      sys.dm_exec_query_plan(qs.plan_handle) AS qp
    WHERE
      (CHARINDEX(vw.schemaname, st.text, 1) > 0)
      AND (st.dbid = DB_ID())
  ) AS t;
GO
```

## <a name="sysdmv_exec_cached_plans"></a>sys.dmv_exec_cached_plans
A consulta final fornece informações sobre as exibições não utilizadas, usando o DMV [sys.dmv_exec_cached_plans](../../relational-databases/system-dynamic-management-views/sys-dm-exec-cached-plans-transact-sql.md). No entanto, o cache do plano de execução é dinâmico e os resultados podem variar. Sendo assim, use esta consulta ao longo do tempo para determinar se uma exibição está de fato sendo usada ou não. 

```sql
SELECT
  SCHEMA_NAME(vw.schema_id) AS schemaname
  ,vw.name AS name
  ,vw.object_id AS viewid
FROM
  sys.views AS vw
WHERE
  (vw.is_ms_shipped = 0)
EXCEPT
SELECT
  SCHEMA_NAME(o.schema_id) AS schemaname
  ,o.name AS name
  ,st.objectid AS viewid
FROM
  sys.dm_exec_cached_plans cp
CROSS APPLY
  sys.dm_exec_sql_text(cp.plan_handle) st
INNER JOIN
  sys.objects o ON st.[objectid] = o.[object_id]
WHERE
  st.dbid = DB_ID();
GO
```

## <a name="see-also"></a>Confira também
[Exibições e funções de gerenciamento dinâmico](../../relational-databases/system-dynamic-management-views/system-dynamic-management-views.md) 
