---
title: sys. database_query_store_options (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/23/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
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
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||= azure-sqldw-latest||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 5f2c8189c19fbdf6dc9a83e62117da517322df86
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "73983168"
---
# <a name="sysdatabase_query_store_options-transact-sql"></a>sys. database_query_store_options (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-asdw-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-asdw-xxx-md.md)]

  Retorna as opções de Repositório de Consultas para este banco de dados.  
  
**Aplica-se a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] e posterior), [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)].
  
|Nome da coluna|Tipo de dados|DESCRIÇÃO|  
|-----------------|---------------|-----------------|  
|**desired_state**|**smallint**|Indica o modo de operação desejado de Repositório de Consultas, definido explicitamente pelo usuário.<br /> 0 = OFF <br /> 1 = READ_ONLY<br /> 2 = READ_WRITE|  
|**desired_state_desc**|**nvarchar (60)**|Descrição textual do modo de operação desejado de Repositório de Consultas:<br />OFF<br />READ_ONLY<br />READ_WRITE|  
|**actual_state**|**smallint**|Indica o modo de operação de Repositório de Consultas. Além da lista de Estados desejados exigida pelo usuário, o estado real pode ser um estado de erro.<br /> 0 = OFF <br /> 1 = READ_ONLY<br /> 2 = READ_WRITE<br /> 3 = ERRO|  
|**actual_state_desc**|**nvarchar (60)**|Descrição textual do modo de operação real de Repositório de Consultas.<br />OFF<br />READ_ONLY<br />READ_WRITE<br />ERROR<br /><br /> Há situações em que o estado real é diferente do estado desejado:<br />-Se o banco de dados estiver definido como modo somente leitura ou se Repositório de Consultas tamanho exceder sua cota configurada, Repositório de Consultas poderá operar no modo somente leitura, mesmo que a leitura-gravação tenha sido especificada pelo usuário.<br />-Em cenários extremos Repositório de Consultas pode inserir um estado de erro devido a erros internos. Se isso acontecer, para o SQL 2017 e posterior, Repositório de Consultas poderá ser recuperado executando o `sp_query_store_consistency_check` procedimento armazenado no banco de dados afetado. Se a `sp_query_store_consistency_check` execução não funcionar e para o SQL 2016, será necessário limpar os dados executando`ALTER DATABASE [YourDatabaseName] SET QUERY_STORE CLEAR ALL;`|  
|**readonly_reason**|**int**|Quando o **desired_state_desc** é READ_WRITE e o **actual_state_desc** é READ_ONLY, **readonly_reason** retorna um mapa de bits para indicar por que o repositório de consultas está no modo ReadOnly.<br /><br /> **1** -o banco de dados está no modo somente leitura<br /><br /> **2** -o banco de dados está no modo de usuário único<br /><br /> **4** -o banco de dados está no modo de emergência<br /><br /> **8** -o banco de dados é uma réplica secundária ( [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] aplica-se a Always on e replicação geográfica). Esse valor pode ser observado efetivamente apenas em réplicas secundárias **legíveis**<br /><br /> **65536** -o repositório de consultas atingiu o limite de tamanho definido pela opção MAX_STORAGE_SIZE_MB.<br /><br /> **131072** -o número de instruções diferentes em repositório de consultas atingiu o limite de memória interna. Considere remover as consultas que você não precisa ou atualizar para uma camada de serviço superior para habilitar a transferência de Repositório de Consultas para o modo de leitura/gravação.<br />**Aplica-se a:** [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].<br /><br /> **262144** -o tamanho dos itens na memória aguardando para serem persistidos no disco atingiu o limite de memória interno. Repositório de Consultas estará no modo somente leitura temporariamente até que os itens na memória sejam persistidos no disco. <br />**Aplica-se a:** [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].<br /><br /> **524288** -o banco de dados atingiu o limite de tamanho do disco. Repositório de Consultas faz parte do banco de dados do usuário, portanto, se não houver mais espaço disponível para um banco de dados, isso significa que Repositório de Consultas ainda não poderá mais crescer.<br />**Aplica-se a:** [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]. <br /> <br /> Para alternar o modo de operações de Repositório de Consultas de volta para leitura e gravação, consulte a seção **verificar repositório de consultas está coletando dados de consulta continuamente** da [prática recomendada com o repositório de consultas](../../relational-databases/performance/best-practice-with-the-query-store.md#Verify).|  
|**current_storage_size_mb**|**bigint**|Tamanho de Repositório de Consultas em disco em megabytes.|  
|**flush_interval_seconds**|**bigint**|O período para a liberação regular de dados de Repositório de Consultas para o disco em segundos. O valor padrão é **900** (15 min).<br /><br /> Altere usando a `ALTER DATABASE <database> SET QUERY_STORE (DATA_FLUSH_INTERVAL_SECONDS  = <interval>)` instrução.|  
|**interval_length_minutes**|**bigint**|O intervalo de agregação de estatísticas em minutos. Valores arbitrários não são permitidos. Use um dos seguintes: 1, 5, 10, 15, 30, 60 e 1440 minutos. O valor padrão é **60** minutos.|  
|**max_storage_size_mb**|**bigint**|Tamanho máximo do disco para o Repositório de Consultas em megabytes (MB). O valor padrão é **100** MB.<br />Para [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)] a edição Premium, o padrão é 1 GB [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)] e para a edição básica, o padrão é 10 MB.<br /><br /> Altere usando a `ALTER DATABASE <database> SET QUERY_STORE (MAX_STORAGE_SIZE_MB = <size>)` instrução.|  
|**stale_query_threshold_days**|**bigint**|Número de dias que consultas sem configurações de política são mantidas em Repositório de Consultas. O valor padrão é **30**. Defina como 0 para desabilitar a política de retenção.<br />Para o [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)] Basic Edition, o padrão é 7 dias.<br /><br /> Altere usando a `ALTER DATABASE <database> SET QUERY_STORE ( CLEANUP_POLICY = ( STALE_QUERY_THRESHOLD_DAYS = <value> ) )` instrução.|  
|**max_plans_per_query**|**bigint**|Limita o número máximo de planos armazenados. O valor padrão é **200**. Se o valor máximo for atingido, Repositório de Consultas interromperá a captura de novos planos para essa consulta. A configuração para 0 remove a limitação com relação ao número de planos capturados.<br /><br /> Altere usando a `ALTER DATABASE<database> SET QUERY_STORE (MAX_PLANS_PER_QUERY = <n>)` instrução.|  
|**query_capture_mode**|**smallint**|O modo de captura de consulta atualmente ativo:<br /><br /> **1** = All-todas as consultas são capturadas. Esse é o valor de configuração padrão [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] (e posterior).<br /><br /> 2 = capturar automaticamente consultas relevantes com base na contagem de execução e no consumo de recursos. Esse é o valor de configuração padrão de [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)].<br /><br /> 3 = NONE-parar de capturar novas consultas. O Repositório de Consultas continuará a coletar estatísticas de compilação e runtime para consultas que já foram capturadas. Use essa configuração com cautela, pois você pode perder a captura de consultas importantes.|  
|**query_capture_mode_desc**|**nvarchar (60)**|Descrição textual do modo de captura real do Repositório de Consultas:<br /><br /> TODOS (padrão para [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)])<br /><br /> **Automático** (padrão para [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)])<br /><br /> Nenhuma|  
|**size_based_cleanup_mode**|**smallint**|Controla se a limpeza será ativada automaticamente quando a quantidade total de dados se aproximar do tamanho máximo:<br /><br /> 0 = a limpeza baseada em tamanho não será ativada automaticamente.<br /><br /> **1** = a limpeza baseada em tamanho automático será ativada automaticamente quando o tamanho no disco atingir **90%** de *max_storage_size_mb*. Esse é o valor de configuração padrão.<br /><br />Limpeza com base no tamanho remove as consultas menos dispendiosas e mais antigas primeiro. Ele para de quando aproximadamente **80%** de *max_storage_size_mb* é atingido.|  
|**size_based_cleanup_mode_desc**|**nvarchar (60)**|Descrição textual do modo de limpeza baseado em tamanho real de Repositório de Consultas:<br /><br /> OFF <br /> **Automático** (padrão)|  
|**wait_stats_capture_mode**|**smallint**|Controla se Repositório de Consultas executa a captura de estatísticas de espera: <br /><br /> 0 = OFF <br /> **1** = ativado<br /> **Aplica-se a**: [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] e posterior.|
|**wait_stats_capture_mode_desc**|**nvarchar (60)**|Descrição textual do modo de captura de estatísticas de espera real: <br /><br /> OFF <br /> **Ativado** (padrão)<br /> **Aplica-se a**: [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] e posterior.| 
  
## <a name="permissions"></a>Permissões  
 Requer a permissão `VIEW DATABASE STATE`.  
  
## <a name="see-also"></a>Consulte Também  
 [sys. query_context_settings &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-context-settings-transact-sql.md)   
 [sys. query_store_plan &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-plan-transact-sql.md)   
 [sys. query_store_query &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-query-transact-sql.md)   
 [sys. query_store_query_text &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-query-text-transact-sql.md)   
 [sys. query_store_runtime_stats &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-runtime-stats-transact-sql.md)   
 [sys. query_store_wait_stats &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-wait-stats-transact-sql.md)  
 [sys. query_store_runtime_stats_interval &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-runtime-stats-interval-transact-sql.md)   
 [Monitorando o desempenho com o repositório de consultas](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)   
 [Exibições de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [sys. fn_stmt_sql_handle_from_sql_stmt &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-stmt-sql-handle-from-sql-stmt-transact-sql.md)   
 [Procedimentos armazenados do Repositório de Consultas &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/query-store-stored-procedures-transact-sql.md)  
  
  
