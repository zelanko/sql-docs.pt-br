---
title: STATS_DATE (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 12/18/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- STATS_DATE_TSQL
- STATS_DATE
dev_langs: TSQL
helpviewer_keywords:
- statistical information [SQL Server], last time updated
- STATS_DATE function
- query optimization statistics [SQL Server], last time updated
- last time statistics updated
- stats update date
ms.assetid: f9ec3101-1e41-489d-b519-496a0d6089fb
caps.latest.revision: "43"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: de308046d069b6efa6115cf1efae33af7c07128c
ms.sourcegitcommit: 2208a909ab09af3b79c62e04d3360d4d9ed970a7
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/02/2018
---
# <a name="statsdate-transact-sql"></a>STATS_DATE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Retorna a data da mais recente atualização de estatísticas em uma tabela ou exibição indexada.  
  
 Para obter mais informações sobre como atualizar estatísticas, consulte [estatísticas](../../relational-databases/statistics/statistics.md).  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
STATS_DATE ( object_id , stats_id )  
```  
  
## <a name="arguments"></a>Argumentos  
 *object_id*  
 ID da tabela ou exibição indexada com as estatísticas.  
  
 *stats_id*  
 ID do objeto de estatísticas.  
  
## <a name="return-types"></a>Tipos de retorno  
 Retorna **datetime** em caso de sucesso. Retorna **nulo** se um blob de estatísticas não foi criado.  
  
## <a name="remarks"></a>Remarks  
 As funções do sistema podem ser usadas na lista de seleção, na cláusula WHERE e em qualquer local onde uma expressão puder ser usada.  
 
 Data de atualização de estatísticas é armazenada no [objeto de estatísticas de blob](../../relational-databases/statistics/statistics.md#DefinitionQOStatistics) junto com o [histograma](../../relational-databases/statistics/statistics.md#histogram) e [vetor de densidade](../../relational-databases/statistics/statistics.md#density), não nos metadados. Quando nenhum dado é lida para gerar dados de estatísticas, o blob de estatísticas não é criado e a data não está disponível. Esse é o caso para estatísticas filtradas para que o predicado não retornar linhas, ou para novas tabelas vazias.
 
 Se as estatísticas corresponderem a um índice, o *stats_id* valor no [Stats](../../relational-databases/system-catalog-views/sys-stats-transact-sql.md) exibição do catálogo é o mesmo que o *index_id* valor o [sys. Indexes](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md) exibição do catálogo.
  
## <a name="permissions"></a>Permissões  
 Requer associação à função de banco de dados fixa db_owner ou permissão para exibir os metadados da tabela ou da exibição indexada.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-return-the-dates-of-the-most-recent-statistics-for-a-table"></a>A. Retornar as datas das estatísticas mais recentes de uma tabela  
 O exemplo a seguir retorna a data da mais recente atualização de cada objeto de estatísticas na tabela `Person.Address`.  
  
```sql  
USE AdventureWorks2012;  
GO  
SELECT name AS stats_name,   
    STATS_DATE(object_id, stats_id) AS statistics_update_date  
FROM sys.stats   
WHERE object_id = OBJECT_ID('Person.Address');  
GO  
```  
  
 Se as estatísticas corresponderem a um índice, o *stats_id* valor no [Stats](../../relational-databases/system-catalog-views/sys-stats-transact-sql.md) exibição do catálogo é o mesmo que o *index_id* valor o [sys. Indexes](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md) exibição do catálogo e a consulta a seguir retorna os mesmos resultados da consulta anterior. Se as estatísticas não corresponderem a um índice, elas estarão nos resultados de sys.stats mas não nos resultados de sys.indexes.  
  
```sql  
USE AdventureWorks2012;  
GO  
SELECT name AS index_name,   
    STATS_DATE(object_id, index_id) AS statistics_update_date  
FROM sys.indexes   
WHERE object_id = OBJECT_ID('Person.Address');  
GO  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Exemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] e[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="b-learn-when-a-named-statistics-was-last-updated"></a>B. Saber quando uma estatística nomeada última atualização  
 O exemplo a seguir cria estatísticas na coluna LastName da tabela DimCustomer. Ele executa uma consulta para mostrar a data das estatísticas. Em seguida, ele as estatísticas de atualizações e executa a consulta novamente para mostrar os dados atualizados.  
  
```sql
--First, create a statistics object  
USE AdventureWorksPDW2012;  
GO  
CREATE STATISTICS Customer_LastName_Stats  
ON AdventureWorksPDW2012.dbo.DimCustomer (LastName)  
WITH SAMPLE 50 PERCENT;  
GO  
  
--Return the date when Customer_LastName_Stats was last updated  
USE AdventureWorksPDW2012;  
GO  
SELECT stats_id, name AS stats_name,   
    STATS_DATE(object_id, stats_id) AS statistics_date  
FROM sys.stats s  
WHERE s.object_id = OBJECT_ID('dbo.DimCustomer')  
    AND s.name = 'Customer_LastName_Stats';  
GO  
  
--Update Customer_LastName_Stats so it will have a different timestamp in the next query  
GO  
UPDATE STATISTICS dbo.dimCustomer (Customer_LastName_Stats);  
  
--Return the date when Customer_LastName_Stats was last updated.  
SELECT stats_id, name AS stats_name,   
    STATS_DATE(object_id, stats_id) AS statistics_date  
FROM sys.stats s  
WHERE s.object_id = OBJECT_ID('dbo.DimCustomer')  
    AND s.name = 'Customer_LastName_Stats';  
GO    
```  
  
### <a name="c-view-the-date-of-the-last-update-for-all-statistics-on-a-table"></a>C. Exiba a data da última atualização de todas as estatísticas em uma tabela  
 Este exemplo retorna a data de cada objeto de estatísticas na tabela DimCustomer foi atualizada pela última vez.  
  
```sql  
--Return the dates all statistics on the table were last updated.  
SELECT stats_id, name AS stats_name,   
    STATS_DATE(object_id, stats_id) AS statistics_date  
FROM sys.stats s  
WHERE s.object_id = OBJECT_ID('dbo.DimCustomer');  
GO  
```  
  
 Se as estatísticas corresponderem a um índice, o *stats_id* valor no [Stats](../../relational-databases/system-catalog-views/sys-stats-transact-sql.md) exibição do catálogo é o mesmo que o *index_id* valor o [sys. Indexes](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md) exibição do catálogo e a consulta a seguir retorna os mesmos resultados da consulta anterior. Se as estatísticas não corresponderem a um índice, elas estarão nos resultados de sys.stats mas não nos resultados de sys.indexes.  
  
```sql  
USE AdventureWorksPDW2012;  
GO  
SELECT name AS index_name,   
    STATS_DATE(object_id, index_id) AS statistics_update_date  
FROM sys.indexes   
WHERE object_id = OBJECT_ID('dbo.DimCustomer');  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Funções de sistema &#40;Transact-SQL&#41;](../../relational-databases/system-functions/system-functions-for-transact-sql.md)   
 [UPDATE STATISTICS &#40;Transact-SQL&#41;](../../t-sql/statements/update-statistics-transact-sql.md)   
 [sp_autostats &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-autostats-transact-sql.md)   
 [Estatísticas](../../relational-databases/statistics/statistics.md)    
 [sys.dm_db_stats_properties &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-stats-properties-transact-sql.md)   
 [sys.stats](../../relational-databases/system-catalog-views/sys-stats-transact-sql.md)   
  
  

