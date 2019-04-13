---
title: sys.query_context_settings (Transact-SQL) | Microsoft Docs
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
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||= azure-sqldw-latest||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 6c7ab77981c329c334b22d6fd9735188882b385c
ms.sourcegitcommit: acb5de9f493238180d13baa302552fdcc30d83c0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/12/2019
ms.locfileid: "59542136"
---
# <a name="sysquerycontextsettings-transact-sql"></a>sys.query_context_settings (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-asdw-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-asdw-xxx-md.md)]

  Contém informações sobre a semântica que afetam as configurações de contexto associadas a uma consulta. Há uma série de configurações de contexto disponíveis no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que influenciam a semântica de consulta (definindo o resultado correto da consulta). O mesmo texto de consulta compilado em configurações diferentes pode produzir resultados diferentes (dependendo dos dados subjacentes).  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**context_settings_id**|**bigint**|Chave primária. Esse valor é exposto no Showplan XML para consultas.|  
|**set_options**|**varbinary(8)**|Máscara de bits refletir o estado de várias opções SET. Para obter mais informações, consulte [exec_plan_attributes &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-plan-attributes-transact-sql.md).|  
|**language_id**|**smallint**|A id do idioma. Para obter mais informações, consulte [sys. syslanguages &#40;Transact-SQL&#41;](../../relational-databases/system-compatibility-views/sys-syslanguages-transact-sql.md).|  
|**date_format**|**smallint**|O formato de data. Para obter mais informações, veja [SET DATEFORMAT &#40;Transact-SQL&#41;](../../t-sql/statements/set-dateformat-transact-sql.md).|  
|**date_first**|**tinyint**|O valor da primeira data. Para obter mais informações, veja [SET DATEFIRST &#40;Transact-SQL&#41;](../../t-sql/statements/set-datefirst-transact-sql.md).|  
|**status**|**varbinary(2)**|Campo de máscara de bits que indica o tipo de consulta ou o contexto no qual a consulta foi executada. <br />O valor da coluna pode ser uma combinação de vários sinalizadores (expressada em hexadecimal):<br /><br /> 0x0 – consulta normal (nenhum sinalizador específico)<br /><br /> 0x1 – consulta foi executada por meio de um dos procedimentos armazenados de APIs cursor<br /><br /> 0x2 – consulta para notificação<br /><br /> 0x4 – consulta interna<br /><br /> 0x8 – a consulta parametrizada automaticamente sem parametrização universal<br /><br /> 0x10 – consulta de atualização de busca do cursor<br /><br /> 0x20 – consulta que está sendo usada em solicitações de atualização do cursor<br /><br /> 0x40 – o conjunto de resultados inicial é retornado quando um cursor é aberto (Cursor busca automática)<br /><br /> 0x80 – consulta criptografada<br /><br /> 0x100 - consulta no contexto do predicado de segurança de nível de linha|  
|**required_cursor_options**|**int**|Opções de cursor especificadas pelo usuário, como o tipo de cursor.|  
|**acceptable_cursor_options**|**int**|Opções de cursor que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pode converter implicitamente para  aceitar a execução da instrução.|  
|**merge_action_type**|**smallint**|O tipo de plano de execução de gatilho usado como o resultado de uma **mesclar** instrução.<br /><br /> 0 indica um plano de não gatilho, um plano de gatilho que não é executado como resultado de uma **mesclar** instrução ou um plano de gatilho é executado como resultado de uma **mesclar** declaração que especifica apenas um **Excluir** ação.<br /><br /> 1 indica um **inserir** plano de gatilho é executado como resultado de uma **mesclar** instrução.<br /><br /> 2 indica um **atualização** plano de gatilho é executado como resultado de uma **mesclar** instrução.<br /><br /> 3 indica um **excluir** plano de gatilho é executado como resultado de uma **mesclar** instrução que contém um correspondente **inserir** ou **atualização** ação.<br /><br /> <br /><br /> Para gatilhos aninhados executados por cascateamento de ações, esse valor é a ação do **mesclar** instrução que causou a cascata.|  
|**default_schema_id**|**int**|ID do esquema padrão, que é usado para resolver nomes que não são totalmente qualificados.|  
|**is_replication_specific**|**bit**|Usado para replicação.|  
|**is_contained**|**varbinary(1)**|1 indica um banco de dados independente.|  
  
## <a name="permissions"></a>Permissões  
 Requer o **VIEW DATABASE STATE** permissão.  
  
## <a name="see-also"></a>Consulte também  
 [sys.database_query_store_options &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-query-store-options-transact-sql.md)   
 [sys.query_store_plan &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-plan-transact-sql.md)   
 [sys.query_store_query &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-query-transact-sql.md)   
 [sys.query_store_query_text &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-query-text-transact-sql.md)   
 [sys.query_store_runtime_stats &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-runtime-stats-transact-sql.md)   
 [sys.query_store_wait_stats &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-wait-stats-transact-sql.md)   
 [sys.query_store_runtime_stats_interval &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-runtime-stats-interval-transact-sql.md)   
 [Monitorando o desempenho com o repositório de consultas](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)   
 [Exibições de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Procedimentos armazenados do Repositório de Consultas &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/query-store-stored-procedures-transact-sql.md)   
 [sys.fn_stmt_sql_handle_from_sql_stmt &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-stmt-sql-handle-from-sql-stmt-transact-sql.md)  
  
  
