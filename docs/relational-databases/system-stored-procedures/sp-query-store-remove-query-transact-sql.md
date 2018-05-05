---
title: sp_query_store_remove_query (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/29/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- SP_QUERY_STORE_REMOVE_QUERY
- SP_QUERY_STORE_REMOVE_QUERY_TSQL
- SYS.SP_QUERY_STORE_REMOVE_QUERY
- SYS.SP_QUERY_STORE_REMOVE_QUERY_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sp_query_store_remove_query
- sp_query_store_remove_query
ms.assetid: cc39ca92-3cba-478e-beef-65560aa84007
caps.latest.revision: 8
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: ad280acf3f473c8bd38771cc515d311b7c65dd05
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="spquerystoreremovequery-transact-sql"></a>sp_query_store_remove_query (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Remove a consulta, bem como todos os respectivos planos e estatísticas de tempo de execução do repositório de consultas.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_query_store_remove_query [ @query_id = ] query_id [;]  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@query_id =** ] *query_id*  
 É a id da consulta a ser removido do repositório de consultas. *query_id* é um **bigint**, sem padrão.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou 1 (falha)  
  
## <a name="remarks"></a>Remarks  
  
## <a name="permissions"></a>Permissões  
 Requer o **EXECUTE** no banco de dados, e **excluir** permissão nas exibições do catálogo de repositório de consulta.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir retorna informações sobre as consultas no repositório de consultas.  
  
```  
SELECT Txt.query_text_id, Txt.query_sql_text, Pl.plan_id, Qry.*  
FROM sys.query_store_plan AS Pl  
JOIN sys.query_store_query AS Qry  
    ON Pl.query_id = Qry.query_id  
JOIN sys.query_store_query_text AS Txt  
    ON Qry.query_text_id = Txt.query_text_id ;  
```  
  
 Depois de identificar a query_id que você deseja excluir, use o exemplo a seguir para excluir a consulta.  
  
 O exemplo a seguir.  
  
```  
EXEC sp_query_store_remove_query 3;  
```  
  
## <a name="see-also"></a>Consulte também  
 [sp_query_store_force_plan &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-query-store-force-plan-transact-sql.md)   
 [sp_query_store_remove_plan &#40;Transct-SQL&#41;](../../relational-databases/system-stored-procedures/sp-query-store-remove-plan-transct-sql.md)   
 [sp_query_store_unforce_plan &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-query-store-unforce-plan-transact-sql.md)   
 [sp_query_store_reset_exec_stats &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-query-store-reset-exec-stats-transact-sql.md)   
 [sp_query_store_flush_db &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-query-store-flush-db-transact-sql.md)   
 [Exibições de Catálogo do Repositório de Consultas &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/query-store-catalog-views-transact-sql.md)   
 [Monitorar o desempenho com o Repositório de Consultas](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)  
  
  
