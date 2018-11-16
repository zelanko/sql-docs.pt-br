---
title: Usar DMVs para determinar estatísticas de uso e o desempenho das exibições
description: Usar DMVs para determinar estatísticas de uso e o desempenho das exibições
manager: craigg
author: MashaMSFT
ms.author: mathoma
ms.date: 09/27/2018
ms.prod: sql
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
ms.openlocfilehash: 05a02bae41ff2d39d9415154fd1aeabeee065c82
ms.sourcegitcommit: 9c6a37175296144464ffea815f371c024fce7032
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/15/2018
ms.locfileid: "51668545"
---
# <a name="use-dmvs-to-determine-usage-statistics-and-performance-of-views"></a>Usar DMVs para determinar estatísticas de uso e o desempenho das exibições

Este artigo aborda a metodologia e os scripts usados para obter informações sobre o **desempenho de consultas que usam exibições** em um objeto de banco de dados. A finalidade desses scripts é fornecer indicadores de uso e desempenho das diferentes exibições encontradas dentro de um banco de dados. 

## <a name="sysdmexecqueryoptimizerinfo"></a>Sys.dm_exec_query_optimizer_info

O DMV [exec_query_optimizer_info](https://docs.microsoft.com/sql/relational-databases/system-dynamic-management-views/sys-dm-exec-query-optimizer-info-transact-sql) expõe estatísticas sobre as otimizações realizadas pelo otimizador de consulta do SQL Server. Esses valores são cumulativos e começam a gravar quando o SQL Server é iniciado.  

A CTE (common_table_expression) a seguir usa esse DMV para fornecer informações sobre a carga de trabalho, como o percentual de consultas que fazem referência a uma exibição. Os resultados retornados pela consulta não indicam um problema de desempenho por si só, mas podem expor problemas subjacentes quando combinados com reclamações de usuários sobre o desempenho lento de consultas. 


```SQL
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
Combine os resultados dessa consulta com os resultados da exibição do sistema [sys.views](https://docs.microsoft.com/sql/relational-databases/system-catalog-views/sys-views-transact-sql) para identificar estatísticas de consulta, o texto da consulta e o plano de execução armazenado em cache. 

## <a name="sysviews"></a>Sys.views

A CTE a seguir fornece informações sobre o número de execuções, o tempo total de execução e as páginas lidas da memória. Os resultados podem ser usados para identificar consultas que podem ser candidatos para otimização. 
  
  >[!NOTE]
  > Os resultados dessa consulta podem variar dependendo da versão do SQL Server.  


```SQL
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

## <a name="sysdmvexeccachedplans"></a>Sys.dmv_exec_cached_plans

A consulta final fornece informações sobre as exibições não utilizadas, usando o DMV [sys.dmv_exec_cached_plans](https://docs.microsoft.com/sql/relational-databases/system-dynamic-management-views/sys-dm-exec-cached-plans-transact-sql). No entanto, o cache do plano de execução é dinâmico e os resultados podem variar. Sendo assim, use esta consulta ao longo do tempo para determinar se uma exibição está de fato sendo usada ou não. 


```SQL
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

## <a name="related-external-resources"></a>Recursos externos relacionados

- [DMVs for Performance Tuning (DMVs para ajuste de desempenho) (Vídeo – SQL Saturday Pordenone)](https://www.youtube.com/watch?v=9FQaFwpt3-k)
- [DMVs for Performance Tuning (DMVs para ajuste de desempenho) (Slide e demonstração – SQL Saturday Pordenone)](https://www.sqlsaturday.com/589/Sessions/Details.aspx?sid=57409)
- [SQL Server Tuning in capsule form (Ajuste do SQL Server em formato de cápsula) (filme – SQL Saturday Parma)](https://vimeo.com/200980883)
- [SQL Server Tuning in a nutshell (Ajuste do SQL Server em poucas palavras) (slides e demonstração – SQL Saturday Parma)](https://www.sqlsaturday.com/566/Sessions/Details.aspx?sid=53988)
- [Ajuste de desempenho com exibições de gerenciamento dinâmico do SQL Server](https://www.red-gate.com/library/performance-tuning-with-sql-server-dynamic-management-views)
- [Os tipos de espera mais proeminentes do SQL Server 2016](https://channel9.msdn.com/Blogs/MVP-Data-Platform/The-Most-Prominent-Wait-Types-of-your-SQL-Server-2016)
