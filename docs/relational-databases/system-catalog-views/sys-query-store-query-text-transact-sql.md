---
title: query_store_query_text (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- SYS.QUERY_STORE_QUERY_TEXT
- QUERY_STORE_QUERY_TEXT
- SYS.QUERY_STORE_QUERY_TEXT_TSQL
- QUERY_STORE_QUERY_TEXT_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.query_store_query_text catalog view
- query_store_query_text catalog view
ms.assetid: f7032fa0-7c16-4492-bb82-685806c63a8c
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 22691879e773939f1c70260460434ee04030f3da
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47747134"
---
# <a name="sysquerystorequerytext-transact-sql"></a>query_store_query_text (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Contém o [!INCLUDE[tsql](../../includes/tsql-md.md)] texto e o identificador SQL da consulta.  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**query_text_id**|**bigint**|Chave primária.|  
|**query_sql_text**|**nvarchar(max)**|Texto SQL da consulta, conforme fornecido pelo usuário. Inclui espaços em branco, dicas e comentários.|  
|**statement_sql_handle**|**vabinary(64)**|Identificador SQL da consulta individual.|  
|**is_part_of_encrypted_module**|**bit**|Texto da consulta é uma parte de um módulo criptografado.|  
|**has_restricted_text**|**bit**|Texto da consulta contém uma senha ou outras palavras unmentionable.|  
  
## <a name="permissions"></a>Permissões  
 Requer o **VIEW DATABASE STATE** permissão.  
  
## <a name="see-also"></a>Consulte também  
 [sys.database_query_store_options &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-query-store-options-transact-sql.md)   
 [sys.query_context_settings &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-context-settings-transact-sql.md)   
 [sys.query_store_plan &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-plan-transact-sql.md)   
 [sys.query_store_query &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-query-transact-sql.md)   
 [sys.query_store_runtime_stats &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-runtime-stats-transact-sql.md)   
 [sys.query_store_wait_stats &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-wait-stats-transact-sql.md)  
 [sys.query_store_runtime_stats_interval &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-runtime-stats-interval-transact-sql.md)   
 [Monitorando o desempenho com o repositório de consultas](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)   
 [Exibições de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Procedimentos armazenados do Repositório de Consultas &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/query-store-stored-procedures-transact-sql.md)   
 [sys.fn_stmt_sql_handle_from_sql_stmt &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-stmt-sql-handle-from-sql-stmt-transact-sql.md)  
  
  
