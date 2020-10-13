---
description: sys.query_store_query_text (Transact-SQL)
title: sys.query_store_query_text (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/23/2019
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
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||>=sql-server-2016||= azure-sqldw-latest||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 2d0dd52ae5c84ab13266bc1c90f81a3d9b2ad869
ms.sourcegitcommit: a5398f107599102af7c8cda815d8e5e9a367ce7e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/13/2020
ms.locfileid: "92005630"
---
# <a name="sysquery_store_query_text-transact-sql"></a>sys.query_store_query_text (Transact-SQL)
[!INCLUDE [sqlserver2016-asdb-asdbmi-asa](../../includes/applies-to-version/sqlserver2016-asdb-asdbmi-asa.md)]

  Contém o [!INCLUDE[tsql](../../includes/tsql-md.md)] texto e o identificador SQL da consulta.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**query_text_id**|**bigint**|Chave primária.|  
|**query_sql_text**|**nvarchar(max)**|Texto SQL da consulta, conforme fornecido pelo usuário. Inclui espaços em branco, dicas e comentários. Comentários e espaços antes e depois o texto da consulta são ignorados. Comentários e espaços dentro do texto não são ignorados.|  
|**statement_sql_handle**|**vabinary (64)**|Identificador SQL da consulta individual.|  
|**is_part_of_encrypted_module**|**bit**|O texto da consulta faz parte de um módulo criptografado.<br/>**Observação:** A análise de Synapse do Azure sempre retornará zero (0).|
|**has_restricted_text**|**bit**|O texto da consulta contém uma senha ou outras palavras não mencionadas.<br/>**Observação:** A análise de Synapse do Azure sempre retornará zero (0).|
  
## <a name="permissions"></a>Permissões  
 Requer a permissão **View Database State** .  
  
## <a name="see-also"></a>Consulte Também  
 [&#41;&#40;Transact-SQL de sys.database_query_store_options ](../../relational-databases/system-catalog-views/sys-database-query-store-options-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sys.query_context_settings ](../../relational-databases/system-catalog-views/sys-query-context-settings-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sys.query_store_plan ](../../relational-databases/system-catalog-views/sys-query-store-plan-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sys.query_store_query ](../../relational-databases/system-catalog-views/sys-query-store-query-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sys.query_store_runtime_stats ](../../relational-databases/system-catalog-views/sys-query-store-runtime-stats-transact-sql.md)   
 [sys.query_store_wait_stats &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-wait-stats-transact-sql.md)  
 [&#41;&#40;Transact-SQL de sys.query_store_runtime_stats_interval ](../../relational-databases/system-catalog-views/sys-query-store-runtime-stats-interval-transact-sql.md)   
 [Monitorando o desempenho com o repositório de consultas](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)   
 [Exibições de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Procedimentos armazenados do Repositório de Consultas &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/query-store-stored-procedures-transact-sql.md)   
 [sys.fn_stmt_sql_handle_from_sql_stmt &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-stmt-sql-handle-from-sql-stmt-transact-sql.md)  
  
  
