---
title: sys.database_query_store_options (Transact-SQL) | Microsoft Docs
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
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 24222ed24da0fea385e27aa13bd518efa15a32c3
ms.sourcegitcommit: ee76381cfb1c16e0a063315c9c7005f10e98cfe6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/26/2019
ms.locfileid: "55071333"
---
# <a name="sysdatabasequerystoreoptions-transact-sql"></a>sys.database_query_store_options (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-asdw-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-asdw-xxx-md.md)]

  Retorna as opções de Store de consulta para esse banco de dados.  
  
**Aplica-se a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ( [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]), [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)].
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**desired_state**|**smallint**|Indica o modo de operação desejada de Store de consulta, explicitamente definidas pelo usuário.<br /> 0 = OFF <br /> 1 = READ_ONLY<br /> 2 = READ_WRITE|  
|**desired_state_desc**|**nvarchar(60)**|Descrição textual do modo de operação desejada da consulta Store:<br />OFF<br />READ_ONLY<br />READ_WRITE|  
|**actual_state**|**smallint**|Indica o modo de operação de consulta Store. Além de lista de estados desejados exigidos pelo usuário, o estado real pode ser um estado de erro.<br /> 0 = OFF <br /> 1 = READ_ONLY<br /> 2 = READ_WRITE<br /> 3 = ERROR|  
|**actual_state_desc**|**nvarchar(60)**|Descrição textual do modo de operação real da consulta Store.<br />OFF<br />READ_ONLY<br />READ_WRITE<br />erro<br /><br /> Há situações quando o estado real for diferente do estado desejado:<br />-Se o banco de dados está definido para o modo somente leitura ou se o tamanho de consulta Store exceder sua cota configurada, consulta Store podem operar em modo somente leitura, mesmo se leitura / gravação tiver sido especificada pelo usuário.<br />-Em cenários extremos Store consulta pode entrar em um estado de erro devido a erros internos. Se isso acontecer, consulta Store pode ser recuperado executando o `sp_query_store_consistency_check` procedimento armazenado no banco de dados afetado.|  
|**readonly_reason**|**int**|Quando o **desired_state_desc** é READ_WRITE e o **actual_state_desc** é READ_ONLY, **readonly_reason** retorna um pouco do mapa para indicar por que a consulta Store está em modo somente leitura.<br /><br /> **1** -banco de dados está no modo somente leitura<br /><br /> **2** -banco de dados está no modo de usuário único<br /> **4** -banco de dados está no modo de emergência<br /> **8** -banco de dados é a réplica secundária (aplica-se ao Always On e [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] replicação geográfica). Esse valor pode ser observado com eficiência apenas no **legível** réplicas secundárias<br /> **65536** -Store a consulta atingiu o limite de tamanho definido pela opção MAX_STORAGE_SIZE_MB.<br /> **131072** -o número de instruções diferentes em Store consulta atingiu o limite de memória interna. Considere remover consultas que você não precisa ou atualizando para uma camada de serviço superior para habilitar a transferência de Store de consulta para o modo de leitura / gravação.<br />**Aplica-se ao:** [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].<br /> **262144** -tamanho dos itens na memória aguardando para ser persistido em disco atingiu o limite de memória interna. Consulta Store estará em modo somente leitura temporariamente, até que os itens na memória são mantidos em disco. <br />**Aplica-se ao:** [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].<br /><br /> **524288** -banco de dados atingiu o limite de tamanho de disco. Consulta Store é parte do banco de dados de usuário, portanto, se não houver espaço não mais disponível para um banco de dados, o que significa que Store de consulta não pode crescer mais mais.<br />**Aplica-se ao:** [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]. <br /> <br /> Para alternar as operações de consulta Store back modo leitura / gravação, consulte **Verify Query Store está coletando dados de consulta continuamente** seção [melhor prática com a Store consulta](../../relational-databases/performance/best-practice-with-the-query-store.md#Verify).|  
|**current_storage_size_mb**|**bigint**|Tamanho da consulta Store em disco em megabytes.|  
|**flush_interval_seconds**|**bigint**|O período regular liberar dos dados de Store de consulta para o disco em segundos. Valor padrão é **900** (15 min).<br /><br /> Alteração usando o `ALTER DATABASE <database> SET QUERY_STORE (DATA_FLUSH_INTERVAL_SECONDS  = <interval>)` instrução.|  
|**interval_length_minutes**|**bigint**|O intervalo de agregação de estatísticas em minutos. Não são permitidos valores arbitrários. Use um dos seguintes: 1, 5, 10, 15, 30, 60 e 1440 minutos. O valor padrão é **60** minutos.|  
|**max_storage_size_mb**|**bigint**|Tamanho máximo em disco para a Store consulta em megabytes (MB). Valor padrão é **100** MB.<br />Para [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)] Premium edition, o padrão é 1 GB e para [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)] Basic edition, o padrão é 10 MB.<br /><br /> Alteração usando o `ALTER DATABASE <database> SET QUERY_STORE (MAX_STORAGE_SIZE_MB = <size>)` instrução.|  
|**stale_query_threshold_days**|**bigint**|Número de dias que consultas sem as configurações de política são mantidas na consulta Store. Valor padrão é **30**. Defina como 0 para desabilitar a política de retenção.<br />Para o [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)] Basic Edition, o padrão é 7 dias.<br /><br /> Alteração usando o `ALTER DATABASE <database> SET QUERY_STORE ( CLEANUP_POLICY = ( STALE_QUERY_THRESHOLD_DAYS = <value> ) )` instrução.|  
|**max_plans_per_query**|**bigint**|Limita o número máximo de planos armazenados. Valor padrão é **200**. Se o valor máximo for atingido, a consulta Store interrompe a captura de novos planos para a consulta. Configuração para 0 remove a limitação em relação o número de planos capturados.<br /><br /> Alteração usando o `ALTER DATABASE<database> SET QUERY_STORE (MAX_PLANS_PER_QUERY = <n>)` instrução.|  
|**query_capture_mode**|**smallint**|O modo de captura de consulta ativa no momento:<br /><br /> **1** = ALL - todas as consultas são capturadas. Esse é o valor de configuração padrão para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] por meio de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]).<br /><br /> 2 = AUTOcaptura de consultas de relevantes com base no consumo de recursos e a contagem de execução. Esse é o valor de configuração padrão para [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)].<br /><br /> 3 = nenhuma - pare de capturar novas consultas. O Repositório de Consultas continuará a coletar estatísticas de compilação e tempo de execução para consultas que já foram capturadas. Use essa configuração com cuidado, pois você poderá deixar de capturar consultas importantes.|  
|**query_capture_mode_desc**|**nvarchar(60)**|Descrição textual do modo de captura real da consulta Store:<br /><br /> Todos os (padrão para [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)])<br /><br /> **AUTO** (padrão para [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)])<br /><br /> Nenhuma|  
|**size_based_cleanup_mode**|**smallint**|Controla se a limpeza será ativada automaticamente quando a quantidade total de dados se aproximar do tamanho máximo:<br /><br /> 0 = OFF - tamanho limpeza com base em não será ativada automaticamente.<br /><br /> **1** = AUTOtamanho limpeza com base em será ativada automaticamente quando o tamanho em disco atingir **90 por cento** de *max_storage_size_mb*. Esse é o valor de configuração padrão.<br /><br />Limpeza com base no tamanho remove as consultas menos dispendiosas e mais antigas primeiro. Ele é interrompido quando aproximadamente **80 por cento** dos *max_storage_size_mb* for atingido.|  
|**size_based_cleanup_mode_desc**|**nvarchar(60)**|Descrição textual do modo de limpeza de baseado no tamanho real da consulta Store:<br /><br /> OFF <br /> **AUTO** (padrão)|  
|**wait_stats_capture_mode**|**smallint**|Controla se Store consulta realiza a captura de estatísticas de espera: <br /><br /> 0 = OFF <br /> **1** = ON<br /> **Aplica-se a**: do [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].|
|**wait_stats_capture_mode_desc**|**nvarchar(60)**|Descrição textual do modo de captura de estatísticas de espera real: <br /><br /> OFF <br /> **ON** (padrão)<br /> **Aplica-se a**: do [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
  
## <a name="permissions"></a>Permissões  
 Requer a permissão `VIEW DATABASE STATE`.  
  
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
 [Procedimentos armazenados de Store de consulta &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/query-store-stored-procedures-transact-sql.md)  
  
  
