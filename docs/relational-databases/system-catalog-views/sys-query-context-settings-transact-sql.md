---
title: sys. query_context_settings (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 11/29/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- QUERY_CONTEXT_SETTINGS_TSQL
- SYS.QUERY_CONTEXT_SETTINGS_TSQL
- SYS.QUERY_CONTEXT_SETTINGS
- QUERY_CONTEXT_SETTINGS
dev_langs:
- TSQL
helpviewer_keywords:
- sys.query_context_settings catalog view
ms.assetid: 3c1887df-6bd8-491e-82fc-d25ad9589faf
author: CarlRabeler
ms.author: carlrab
monikerRange: =azuresqldb-current||>=sql-server-2016||= azure-sqldw-latest||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: d39fe1b573e038459853857496c651e9ad2af83b
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/05/2020
ms.locfileid: "82831460"
---
# <a name="sysquery_context_settings-transact-sql"></a>sys. query_context_settings (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-asdw-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-asdw-xxx-md.md)]

  Contém informações sobre a semântica que afeta as configurações de contexto associadas a uma consulta. Há várias configurações de contexto disponíveis no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que influenciam a semântica da consulta (definindo o resultado correto da consulta). O mesmo texto de consulta compilado em configurações diferentes pode produzir resultados diferentes (dependendo dos dados subjacentes).  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**context_settings_id**|**bigint**|Chave primária. Esse valor é exposto em Showplan XML para consultas.|  
|**set_options**|**varbinary (8)**|Máscara de bits refletindo o estado de várias opções de conjunto. Para obter mais informações, consulte [Sys. dm_exec_plan_attributes &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-plan-attributes-transact-sql.md).|  
|**language_id**|**smallint**|A ID do idioma. Para obter mais informações, consulte [Sys. syslanguages &#40;&#41;Transact-SQL ](../../relational-databases/system-compatibility-views/sys-syslanguages-transact-sql.md).|  
|**date_format**|**smallint**|O formato de data. Para obter mais informações, veja [SET DATEFORMAT &#40;Transact-SQL&#41;](../../t-sql/statements/set-dateformat-transact-sql.md).|  
|**date_first**|**tinyint**|O primeiro valor da data. Para obter mais informações, veja [SET DATEFIRST &#40;Transact-SQL&#41;](../../t-sql/statements/set-datefirst-transact-sql.md).|  
|**status**|**varbinary (2)**|O campo de bitmask que indica o tipo de consulta ou contexto no qual a consulta foi executada. <br />O valor da coluna pode ser uma combinação de vários sinalizadores (expressos em hexadecimal):<br /><br /> 0x0-consulta regular (nenhum sinalizador específico)<br /><br /> 0x1-consulta executada por meio de um dos procedimentos armazenados de APIs de cursor<br /><br /> 0x2-consulta para notificação<br /><br /> 0x4-consulta interna<br /><br /> 0x8-consulta parametrizada automaticamente sem parametrização universal<br /><br /> 0x10-consulta de atualização do cursor FETCH<br /><br /> 0x20-consulta que está sendo usada em solicitações de atualização de cursor<br /><br /> 0x40-o conjunto de resultados inicial é retornado quando um cursor é aberto (busca automática do cursor)<br /><br /> consulta criptografada por 0x80<br /><br /> 0x100-consulta no contexto do predicado de segurança em nível de linha|  
|**required_cursor_options**|**int**|Opções de cursor especificadas pelo usuário, como o tipo de cursor.|  
|**acceptable_cursor_options**|**int**|Opções de cursor que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pode converter implicitamente para  aceitar a execução da instrução.|  
|**merge_action_type**|**smallint**|O tipo de plano de execução de gatilho usado como resultado de uma instrução **Merge** .<br /><br /> 0 indica um plano que não é de gatilho, um plano de gatilho que não é executado como resultado de uma instrução **Merge** ou um plano de gatilho que é executado como resultado de uma instrução **Merge** que especifica apenas uma ação de **exclusão** .<br /><br /> 1 indica um plano de gatilho de **inserção** que é executado como resultado de uma instrução **Merge** .<br /><br /> 2 indica um plano de disparo de **atualização** que é executado como resultado de uma instrução **Merge** .<br /><br /> 3 indica um plano de gatilho de **exclusão** que é executado como resultado de uma instrução **Merge** que contém uma ação de **inserção** ou **atualização** correspondente.<br /><br /> <br /><br /> Para gatilhos aninhados executados por ações em cascata, esse valor é a ação da instrução **Merge** que causou a cascata.|  
|**default_schema_id**|**int**|ID do esquema padrão, que é usado para resolver nomes que não são totalmente qualificados.|  
|**is_replication_specific**|**bit**|Usado para replicação.|  
|**is_contained**|**varbinary (1)**|1 indica um banco de dados independente.|  
  
## <a name="permissions"></a>Permissões  
 Requer a permissão **View Database State** .  
  
## <a name="see-also"></a>Consulte Também  
 [sys. database_query_store_options &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-query-store-options-transact-sql.md)   
 [sys. query_store_plan &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-plan-transact-sql.md)   
 [sys. query_store_query &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-query-transact-sql.md)   
 [sys. query_store_query_text &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-query-text-transact-sql.md)   
 [sys. query_store_runtime_stats &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-runtime-stats-transact-sql.md)   
 [sys. query_store_wait_stats &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-wait-stats-transact-sql.md)   
 [sys. query_store_runtime_stats_interval &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-runtime-stats-interval-transact-sql.md)   
 [Monitorando o desempenho com o repositório de consultas](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)   
 [Exibições de catálogo &#40;&#41;Transact-SQL](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Repositório de Consultas procedimentos armazenados &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/query-store-stored-procedures-transact-sql.md)   
 [sys.fn_stmt_sql_handle_from_sql_stmt &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-stmt-sql-handle-from-sql-stmt-transact-sql.md)  
  
  
