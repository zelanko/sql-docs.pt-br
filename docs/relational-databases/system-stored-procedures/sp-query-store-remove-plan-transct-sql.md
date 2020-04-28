---
title: sp_query_store_remove_plan (Transct-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/29/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- SYS.SP_QUERY_STORE_REMOVE_PLAN_TSQL
- SP_QUERY_STORE_REMOVE_PLAN_TSQL
- SP_QUERY_STORE_REMOVE_PLAN
- SYS.SP_QUERY_STORE_REMOVE_PLAN
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sp_query_store_remove_plan
- sp_query_store_remove_plan
ms.assetid: 88734726-135b-4b61-9f3f-f568c1fbece6
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: ef04dee7a7384141aab820c2c65343a18b605ad0
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68418941"
---
# <a name="sp_query_store_remove_plan-transct-sql"></a>sp_query_store_remove_plan (Transct-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Remove um único plano do repositório de consultas.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_query_store_remove_plan [ @plan_id = ] plan_id [;]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @plan_id = ] plan_id`É a ID do plano de consulta a ser removido. *plan_id* é um **bigint**, sem padrão.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou 1 (falha)  
  
## <a name="remarks"></a>Comentários  
  
## <a name="permissions"></a>Permissões  
 Requer a permissão **ALTER** no banco de dados.
  
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
  
 Depois de identificar o plan_id que você deseja excluir, use o exemplo a seguir para excluir um plano de consulta.  
  
```  
EXEC sp_query_store_remove_plan 3;  
```  
  
## <a name="see-also"></a>Consulte Também  
 [&#41;&#40;Transact-SQL de sp_query_store_force_plan](../../relational-databases/system-stored-procedures/sp-query-store-force-plan-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_query_store_remove_query](../../relational-databases/system-stored-procedures/sp-query-store-remove-query-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_query_store_unforce_plan](../../relational-databases/system-stored-procedures/sp-query-store-unforce-plan-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_query_store_reset_exec_stats](../../relational-databases/system-stored-procedures/sp-query-store-reset-exec-stats-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_query_store_flush_db](../../relational-databases/system-stored-procedures/sp-query-store-flush-db-transact-sql.md)   
 [Repositório de Consultas exibições de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/query-store-catalog-views-transact-sql.md)   
 [Monitorando o desempenho com o repositório de consultas](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)  
  
  
