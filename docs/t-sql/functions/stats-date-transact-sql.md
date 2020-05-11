---
title: STATS_DATE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 12/18/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STATS_DATE_TSQL
- STATS_DATE
dev_langs:
- TSQL
helpviewer_keywords:
- statistical information [SQL Server], last time updated
- STATS_DATE function
- query optimization statistics [SQL Server], last time updated
- last time statistics updated
- stats update date
ms.assetid: f9ec3101-1e41-489d-b519-496a0d6089fb
author: julieMSFT
ms.author: jrasnick
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 2962b457655e2621eb28d64820dcad78dbc7e380
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/05/2020
ms.locfileid: "82802903"
---
# <a name="stats_date-transact-sql"></a>STATS_DATE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Retorna a data da mais recente atualização de estatísticas em uma tabela ou exibição indexada.  
  
 Para obter mais informações sobre como atualizar estatísticas, consulte [Estatísticas](../../relational-databases/statistics/statistics.md).  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
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
 Retorna **datetime** em caso de êxito. Retorna **NULL** se um blob de estatísticas não foi criado.  
  
## <a name="remarks"></a>Comentários  
 As funções do sistema podem ser usadas na lista de seleção, na cláusula WHERE e em qualquer local onde uma expressão puder ser usada.  
 
 A data de atualização de estatísticas é armazenada no [objeto de blob de estatísticas](../../relational-databases/statistics/statistics.md#DefinitionQOStatistics), junto com o [histograma](../../relational-databases/statistics/statistics.md#histogram) e o [vetor de densidade](../../relational-databases/statistics/statistics.md#density), não nos metadados. Quando nenhum dado é lido para gerar dados de estatísticas, o blob de estatísticas não é criado e a data não fica disponível. Esse é o caso para estatísticas filtradas para as quais o predicado não retorna nenhuma linha ou para novas tabelas vazias.
 
 Se as estatísticas corresponderem a um índice, o valor de *stats_id* na exibição do catálogo [sys.stats](../../relational-databases/system-catalog-views/sys-stats-transact-sql.md) será o mesmo que o valor de *index_id* na exibição do catálogo [sys.indexes](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md).
  
## <a name="permissions"></a>Permissões  
 Requer associação à função de banco de dados fixa db_owner ou permissão para exibir os metadados da tabela ou da exibição indexada.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-return-the-dates-of-the-most-recent-statistics-for-a-table"></a>a. Retornar as datas das estatísticas mais recentes de uma tabela  
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
  
 Se as estatísticas corresponderem a um índice, o valor de *stats_id* na exibição do catálogo [sys.stats](../../relational-databases/system-catalog-views/sys-stats-transact-sql.md) será igual ao valor de *index_id* da exibição do catálogo [sys.indexes](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md) e a consulta a seguir retornará o mesmo resultado da consulta anterior. Se as estatísticas não corresponderem a um índice, elas estarão nos resultados de sys.stats mas não nos resultados de sys.indexes.  
  
```sql  
USE AdventureWorks2012;  
GO  
SELECT name AS index_name,   
    STATS_DATE(object_id, index_id) AS statistics_update_date  
FROM sys.indexes   
WHERE object_id = OBJECT_ID('Person.Address');  
GO  
```  
  
## <a name="examples-sssdwfull-and-sspdw"></a>Exemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] e [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="b-learn-when-a-named-statistics-was-last-updated"></a>B. Saber a data da última atualização de uma estatística nomeada  
 O exemplo a seguir cria estatísticas na coluna LastName da tabela DimCustomer. Em seguida, ele executa uma consulta para mostrar a data das estatísticas. Depois, ele atualiza as estatísticas e executa a consulta novamente para mostrar os dados atualizados.  
  
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
  
### <a name="c-view-the-date-of-the-last-update-for-all-statistics-on-a-table"></a>C. Exibir a data da última atualização de todas as estatísticas em uma tabela  
 Este exemplo retorna a data da última atualização de cada objeto de estatísticas na tabela DimCustomer.  
  
```sql  
--Return the dates all statistics on the table were last updated.  
SELECT stats_id, name AS stats_name,   
    STATS_DATE(object_id, stats_id) AS statistics_date  
FROM sys.stats s  
WHERE s.object_id = OBJECT_ID('dbo.DimCustomer');  
GO  
```  
  
 Se as estatísticas corresponderem a um índice, o valor de *stats_id* na exibição do catálogo [sys.stats](../../relational-databases/system-catalog-views/sys-stats-transact-sql.md) será igual ao valor de *index_id* da exibição do catálogo [sys.indexes](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md) e a consulta a seguir retornará o mesmo resultado da consulta anterior. Se as estatísticas não corresponderem a um índice, elas estarão nos resultados de sys.stats mas não nos resultados de sys.indexes.  
  
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
 [Funções de sistema &#40;Transact-SQL&#41;](../../relational-databases/system-functions/system-functions-category-transact-sql.md)   
 [UPDATE STATISTICS &#40;Transact-SQL&#41;](../../t-sql/statements/update-statistics-transact-sql.md)   
 [sp_autostats &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-autostats-transact-sql.md)   
 [Estatística](../../relational-databases/statistics/statistics.md)    
 [sys.dm_db_stats_properties &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-stats-properties-transact-sql.md)   
 [sys.stats](../../relational-databases/system-catalog-views/sys-stats-transact-sql.md)   
  
  

