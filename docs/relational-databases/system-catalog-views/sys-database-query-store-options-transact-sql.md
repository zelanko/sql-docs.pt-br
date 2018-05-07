---
title: database_query_store_options (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 10/25/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- DATABASE_QUERY_STORE_OPTIONS_TSQL
- DATABASE_QUERY_STORE_OPTIONS
- SYS.DATABASE_QUERY_STORE_OPTIONS_TSQL
- SYS.DATABASE_QUERY_STORE_OPTIONS
dev_langs:
- TSQL
helpviewer_keywords:
- database_query_store_options catalog view
- sys.database_query_store_options catalog view
ms.assetid: 16b47d55-8019-41ff-ad34-1e0112178067
caps.latest.revision: 24
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: a9ce2b5f63405a0754782e0dddae5584c1b47ee2
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2018
---
# <a name="sysdatabasequerystoreoptions-transact-sql"></a>sys.database_query_store_options (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Retorna as opções de repositório de consultas para este banco de dados.  
  
**Aplica-se a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]), [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)].
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**desired_state**|**smallint**|Indica o modo de operação desejado do repositório de consultas, explicitamente definido pelo usuário.<br /> 0 = OFF <br /> 1 = READ_ONLY<br /> 2 = READ_WRITE|  
|**desired_state_desc**|**nvarchar(64)**|Descrição textual do modo de operação desejado do repositório de consultas:<br />OFF<br />READ_ONLY<br />READ_WRITE|  
|**actual_state**|**smallint**|Indica o modo de operação do repositório de consultas. Além de lista de estados desejados exigidos pelo usuário, o estado real pode ser um estado de erro.<br /> 0 = OFF <br /> 1 = READ_ONLY<br /> 2 = READ_WRITE<br /> 3 = ERRO|  
|**actual_state_desc**|**nvarchar(64)**|Descrição textual do modo de operação real do repositório de consultas.<br />OFF<br />READ_ONLY<br />READ_WRITE<br />ERROR<br /><br /> Há situações quando o estado real for diferente do estado desejado:<br /><br /> Repositório de consultas pode operar em modo somente leitura, mesmo se leitura / gravação foi especificada pelo usuário. Por exemplo, isso pode acontecer se o banco de dados está no modo somente leitura ou se o tamanho do repositório de consultas excedeu a cota.<br /><br /> Muito raramente, repositório de consultas pode terminar no estado de erro devido a erros internos. Se isso acontecer, o repositório de consultas pode ser recuperado por execução **sp_query_store_consistency_check** armazenado procedimento no banco de dados afetado.|  
|**readonly_reason**|**Int**|Quando o **desired_state_desc** é READ_WRITE e o **actual_state_desc** é READ_ONLY, **readonly_reason** retorna mapear um pouco para indicar por que o repositório de consultas está em modo somente leitura.<br /><br /> 1 = o banco de dados está no modo somente leitura<br /><br /> 2 – o banco de dados está no modo de usuário único<br /><br /> 4 – o banco de dados está no modo de emergência<br /><br /> 8 – o banco de dados é a réplica secundária (aplica-se sempre ligado e o Azure [!INCLUDE[ssSDS](../../includes/sssds-md.md)] replicação geográfica). Esse valor pode ser observado efetivamente apenas em **legível** réplicas secundárias<br /><br /> 65536 – o repositório de consultas atingiu o limite de tamanho definido pela opção MAX_STORAGE_SIZE_MB.<br /><br /> 131072 - o número de instruções diferentes no repositório de consultas atingiu o limite de memória interna. Considere remover consultas que não é necessário ou atualizar para uma camada de serviço superior para habilitar a transferência de repositório de consultas para o modo de leitura / gravação.<br />Aplica-se apenas ao [!INCLUDE[ssSDS](../../includes/sssds-md.md)].<br /><br /> 262144 – tamanho dos itens na memória aguardando para ser mantido no disco atingiu o limite de memória interna. Repositório de consultas estará no modo somente leitura temporariamente até que os itens na memória são mantidos em disco. <br />Aplica-se apenas ao [!INCLUDE[ssSDS](../../includes/sssds-md.md)].<br /><br />524288 – o banco de dados atingiu o limite de tamanho de disco. Repositório de consultas faz parte do banco de dados de usuário, para que se não houver mais nenhum espaço para um banco de dados, o que significa que o repositório de consultas não pode crescer mais mais.<br />Aplica-se apenas ao [!INCLUDE[ssSDS](../../includes/sssds-md.md)]. <br /> <br /> Para alternar as operações de repositório de consultas novamente de modo leitura / gravação, consulte **Verifique se o repositório de consultas está coletando dados de consulta continuamente** seção [melhor prática com o repositório de consultas](../../relational-databases/performance/best-practice-with-the-query-store.md).|  
|**current_storage_size_mb**|**bigint**|Tamanho do repositório de consultas em disco em megabytes.|  
|**flush_interval_seconds**|**bigint**|Define o período para liberar regular de dados de repositório de consultas para o disco. Valor padrão é 900 (15 min).<br /><br /> Alteração usando o `ALTER DATABASE <database> SET QUERY_STORE (DATA_FLUSH_INTERVAL_SECONDS  = <interval>)` instrução.|  
|**interval_length_minutes**|**bigint**|O intervalo de agregação de estatísticas. Não são permitidos valores arbitrários. Use um dos seguintes: 1, 5, 10, 15, 30, 60 e 1440 minutos. O valor padrão é 60 minutos.|  
|**max_storage_size_mb**|**bigint**|Tamanho máximo do disco para o repositório de consultas. Valor padrão é 100 MB.<br />Para o [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)] Premium Edition, o padrão é 1 Gb e, para o [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)] Basic Edition, o padrão é 10 Mb.<br /><br /> Alteração usando o `ALTER DATABASE <database> SET QUERY_STORE (MAX_STORAGE_SIZE_MB = <size>)` instrução.|  
|**stale_query_threshold_days**|**bigint**|Número de dias que consultas sem as configurações de política são mantidas no repositório de consultas. Valor padrão é 30. Defina como 0 para desabilitar a política de retenção.<br />Para o [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)] Basic Edition, o padrão é 7 dias.<br /><br /> Alteração usando o `ALTER DATABASE <database> SET QUERY_STORE ( CLEANUP_POLICY = ( STALE_QUERY_THRESHOLD_DAYS = <value> ) )` instrução.|  
|**max_plans_per_query**|**bigint**|Limita o número máximo de planos armazenados. Valor padrão é 200. Se o valor máximo for atingido, o repositório de consultas interrompe a captura novos planos de consulta. Configuração para 0 remove a limitação em relação o número de planos capturados.<br /><br /> Alteração usando o `ALTER DATABASE<database> SET QUERY_STORE (MAX_PLANS_PER_QUERY = <n>)` instrução.|  
|**query_capture_mode**|**smallint**|O modo de captura de consulta ativas no momento:<br /><br /> 1 = ALL - todas as consultas são capturadas. Esse é o valor de configuração padrão para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] por meio de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]).<br /><br /> 2 = AUTOcaptura consultas relevantes com base no consumo de recursos e contagem de execução. Esse é o valor de configuração padrão para [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)].<br /><br /> 3 = nenhuma - parar de capturar novas consultas. O Repositório de Consultas continuará a coletar estatísticas de compilação e tempo de execução para consultas que já foram capturadas. Use essa configuração com cuidado porque você poderá perder para capturar consultas importantes.|  
|**query_capture_mode_desc**|**nvarchar(60)**|Descrição textual do modo de captura real do repositório de consultas:<br /><br /> Todos (padrão para [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)])<br /><br /> AUTO (padrão para [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)])<br /><br /> Nenhuma|  
|**size_based_cleanup_mode**|**smallint**|Controla se a limpeza será ativada automaticamente quando a quantidade total de dados se aproximar do tamanho máximo:<br /><br /> 1 = OFF – tamanho limpeza com base não será ativada automaticamente.<br /><br /> 2 = AUTOtamanho limpeza com base será ativada automaticamente quando o tamanho em disco atingir 90% de **max_storage_size_mb**. Esse é o valor de configuração padrão.<br /><br />Limpeza com base no tamanho remove as consultas menos dispendiosas e mais antigas primeiro. Ele interrompe a aproximadamente 80% do max_storage_size_mb.|  
|**size_based_cleanup_mode_desc**|**smallint**|Descrição textual do modo real de limpeza com base no tamanho do repositório de consultas:<br /><br /> OFF <br /><br /> AUTOMÁTICO (padrão)|  
|**wait_stats_capture_mode**|**smallint**|Controla se o repositório de consultas executa captura de estatísticas de espera: <br /><br /> 0 = OFF <br /><br /> 1 = ON<br /> **Aplica-se a**: do [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].|
|**wait_stats_mode_capture_desc**|**nvarchar(60)**|Descrição textual do modo de captura de estatísticas de espera real: <br /><br /> OFF <br /><br /> ON (padrão)<br /> **Aplica-se a**: do [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
  
## <a name="permissions"></a>Permissões  
 Requer o **VIEW DATABASE STATE** permissão.  
  
## <a name="see-also"></a>Consulte também  
 [sys.query_context_settings &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-context-settings-transact-sql.md)   
 [sys.query_store_plan &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-plan-transact-sql.md)   
 [sys.query_store_query &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-query-transact-sql.md)   
 [sys.query_store_query_text &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-query-text-transact-sql.md)   
 [sys.query_store_runtime_stats &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-runtime-stats-transact-sql.md)   
 [sys.query_store_wait_stats &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-wait-stats-transact-sql.md)  
 [sys.query_store_runtime_stats_interval &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-runtime-stats-interval-transact-sql.md)   
 [Monitorando o desempenho com o repositório de consultas](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)   
 [Exibições de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [sys.fn_stmt_sql_handle_from_sql_stmt &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-stmt-sql-handle-from-sql-stmt-transact-sql.md)   
 [Procedimentos armazenados do repositório de consulta &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/query-store-stored-procedures-transact-sql.md)  
  
  
