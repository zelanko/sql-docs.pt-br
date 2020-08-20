---
description: sys.fn_stmt_sql_handle_from_sql_stmt (Transact-SQL)
title: sys.fn_stmt_sql_handle_from_sql_stmt (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 6794e073-0895-4507-aba3-c3545acc843f
author: rothja
ms.author: jroth
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 5008d433757351e6d4be65d6db9c3ba8e0deb10f
ms.sourcegitcommit: 331b8495e4ab37266945c81ff5b93d250bdaa6da
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/20/2020
ms.locfileid: "88646496"
---
# <a name="sysfn_stmt_sql_handle_from_sql_stmt-transact-sql"></a>sys.fn_stmt_sql_handle_from_sql_stmt (Transact-SQL)

[!INCLUDE [sqlserver2016-asdb-asdbmi](../../includes/applies-to-version/sqlserver2016-asdb-asdbmi.md)]

  Obtém o **stmt_sql_handle** para uma [!INCLUDE[tsql](../../includes/tsql-md.md)] instrução sob o tipo de parametrização fornecido (simples ou forçado). Isso permite que você faça referência a consultas armazenadas no Repositório de Consultas usando seus **stmt_sql_handle** quando souber seu texto.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
sys.fn_stmt_sql_handle_from_sql_stmt   
(  
    'query_sql_text',   
    [ query_param_type   
) [;]  
```  
  
## <a name="arguments"></a>Argumentos  
 *query_sql_text*  
 É o texto da consulta no repositório de consultas que você deseja que o identificador. *query_sql_text* é um **nvarchar (max)**, sem padrão.  
  
 *query_param_type*  
 É o tipo de parâmetro da consulta. *query_param_type* é um **tinyint**. Os valores possíveis são:  
  
-   NULO-padrão para 0  
  
-   0 – Nenhum  
  
-   1-usuário  
  
-   2 – simples  
  
-   3-forçado  
  
## <a name="columns-returned"></a>Colunas retornadas  
 A tabela a seguir lista as colunas que sys. fn_stmt_sql_handle_from_sql_stmt retorna.  
  
|Nome da coluna|Type|Descrição|  
|-----------------|----------|-----------------|  
|**statement_sql_handle**|**varbinary(64)**|O identificador SQL.|  
|**query_sql_text**|**nvarchar(max)**|O texto da [!INCLUDE[tsql](../../includes/tsql-md.md)] instrução.|  
|**query_parameterization_type**|**tinyint**|O tipo de parametrização de consulta.|  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou 1 (falha)  
  
## <a name="remarks"></a>Comentários  
  
## <a name="permissions"></a>Permissões  
 Requer a permissão **Execute** no banco de dados e a permissão **delete** nas exibições do catálogo do repositório de consultas.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir executa uma instrução e, em seguida, usa `sys.fn_stmt_sql_handle_from_sql_stmt` para retornar o identificador SQL dessa instrução.  
  
```  
SELECT * FROM sys.databases;   
SELECT * FROM sys.fn_stmt_sql_handle_from_sql_stmt('SELECT * FROM sys.databases', NULL);  
```  
  
 Use a função para correlacionar dados de Repositório de Consultas com outras exibições de gerenciamento dinâmico. O exemplo a seguir:  
  
```  
SELECT qt.query_text_id, q.query_id, qt.query_sql_text, qt.statement_sql_handle,  
q.context_settings_id, qs.statement_context_id   
FROM sys.query_store_query_text AS qt  
JOIN sys.query_store_query AS q   
    ON qt.query_text_id = q.query_id  
CROSS APPLY sys.fn_stmt_sql_handle_from_sql_stmt (qt.query_sql_text, null) AS fn_handle_from_stmt  
JOIN sys.dm_exec_query_stats AS qs   
    ON fn_handle_from_stmt.statement_sql_handle = qs.statement_sql_handle;  
```  
  
## <a name="see-also"></a>Consulte Também  
 [&#41;&#40;Transact-SQL de sp_query_store_force_plan ](../../relational-databases/system-stored-procedures/sp-query-store-force-plan-transact-sql.md)   
 [sp_query_store_remove_plan &#40;Transct-SQL&#41;](../../relational-databases/system-stored-procedures/sp-query-store-remove-plan-transct-sql.md)   
 [&#41;&#40;Transact-SQL de sp_query_store_unforce_plan ](../../relational-databases/system-stored-procedures/sp-query-store-unforce-plan-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_query_store_reset_exec_stats ](../../relational-databases/system-stored-procedures/sp-query-store-reset-exec-stats-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_query_store_flush_db ](../../relational-databases/system-stored-procedures/sp-query-store-flush-db-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_query_store_remove_query ](../../relational-databases/system-stored-procedures/sp-query-store-remove-query-transact-sql.md)   
 [Repositório de Consultas exibições de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/query-store-catalog-views-transact-sql.md)   
 [Monitorando o desempenho com o repositório de consultas](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)  
  
  
