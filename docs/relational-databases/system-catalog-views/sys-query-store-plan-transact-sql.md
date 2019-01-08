---
title: query_store_plan (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 11/29/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- QUERY_STORE_PLAN_TSQL
- SYS.QUERY_STORE_PLAN
- SYS.QUERY_STORE_PLAN_TSQL
- QUERY_STORE_PLAN
dev_langs:
- TSQL
helpviewer_keywords:
- query_store_plan catalog view
- sys.query_store_plan catalog view
ms.assetid: b4d05439-6360-45db-b1cd-794f4a64935e
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: a5b7b4b9831fcfa04932ed05951b27bca7e4e4b0
ms.sourcegitcommit: c7febcaff4a51a899bc775a86e764ac60aab22eb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/30/2018
ms.locfileid: "52710767"
---
# <a name="sysquerystoreplan-transact-sql"></a>query_store_plan (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-asdw-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-asdw-xxx-md.md)]

  Contém informações sobre cada plano de execução associado a uma consulta.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**plan_id**|**bigint**|Chave primária.|  
|**query_id**|**bigint**|Chave estrangeira. Ingressa [query_store_query &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-query-transact-sql.md).|  
|**plan_group_id**|**bigint**|ID do grupo de plano. Consultas de cursor normalmente exigem vários (popular e buscar) planos. Preencher e planos de busca que são compilados juntos estão no mesmo grupo.<br /><br /> 0 significa que o plano não está em um grupo.|  
|**engine_version**|**nvarchar(32)**|Versão do mecanismo usado para compilar o plano no **'Major'** formato.|  
|**compatibility_level**|**smallint**|Nível de compatibilidade do banco de dados do banco de dados referenciado na consulta.|  
|**query_plan_hash**|**binary(8)**|Hash MD5 do plano individual.|  
|**query_plan**|**nvarchar(max)**|Showplan XML para o plano de consulta.|  
|**is_online_index_plan**|**bit**|Plano foi usado durante a criação de um índice online.|  
|**is_trivial_plan**|**bit**|Plano é um plano trivial (saída do estágio 0 do otimizador de consulta).|  
|**is_parallel_plan**|**bit**|Plano é paralelo.|  
|**is_forced_plan**|**bit**|Plano está marcado como forçado quando o usuário executa o procedimento armazenado **sys.sp_query_store_force_plan**. Mecanismo de imposição *não garante* que exatamente este plano será usado para a consulta referenciada por **query_id**. A imposição de plano faz com que a consulta a ser compilado novamente e geralmente produz exatamente o plano iguais ou semelhante para o plano referenciado pelo **plan_id**. Se a imposição de plano não for bem-sucedida, **force_failure_count** será incrementado e **last_force_failure_reason** é preenchido com o motivo da falha.|  
|**is_natively_compiled**|**bit**|Plano inclui procedimentos compilados nativamente com otimização de memória. (0 = FALSE, 1 = TRUE).|  
|**force_failure_count**|**bigint**|Número de vezes que impor esse plano falhou. Ele pode ser incrementado somente quando a consulta é recompilada (*não em cada execução*). Ele é redefinido como 0 sempre **is_plan_forced** é alterado de **falso** para **TRUE**.|  
|**last_force_failure_reason**|**int**|Motivo pelo qual a imposição de plano falhou.<br /><br /> 0: não falha, caso contrário, número do erro do erro que causou a imposição de falha<br /><br /> 8637: ONLINE_INDEX_BUILD<br /><br /> 8683: INVALID_STARJOIN<br /><br /> 8684: TIME_OUT<br /><br /> 8689: NO_DB<br /><br /> 8690: HINT_CONFLICT<br /><br /> 8691: SETOPT_CONFLICT<br /><br /> 8694: DQ_NO_FORCING_SUPPORTED<br /><br /> 8698: NO_PLAN<br /><br /> 8712: NO_INDEX<br /><br /> 8713: VIEW_COMPILE_FAILED<br /><br /> \<outro valor >: GENERAL_FAILURE|  
|**last_force_failure_reason_desc**|**nvarchar(128)**|Descrição textual do last_force_failure_reason_desc.<br /><br /> ONLINE_INDEX_BUILD: consulta tenta modificar dados enquanto a tabela de destino tem um índice que está sendo criado online<br /><br /> INVALID_STARJOIN: o plano contém especificação inválida de StarJoin<br /><br /> TIME_OUT: Otimizador excedida o número de operações permitidas ao procurar o plano especificado pelo plano forçado<br /><br /> NO_DB: Um banco de dados especificado no plano não existe<br /><br /> HINT_CONFLICT: A consulta não pode ser compilada porque o plano está em conflito com uma dica de consulta<br /><br /> DQ_NO_FORCING_SUPPORTED: Não é possível executar a consulta porque o plano está em conflito com o uso de consulta distribuída ou operações de texto completo.<br /><br /> NO_PLAN: Processador de consultas não pôde produzir o plano de consulta porque o plano forçado não pôde ser verificado para ser válido para a consulta<br /><br /> NO_INDEX: O índice especificado no plano não existe<br /><br /> VIEW_COMPILE_FAILED: Não foi possível forçar o plano de consulta devido a um problema em uma exibição indexada referenciada no plano<br /><br /> GENERAL_FAILURE: erro geral de imposição (não abordado com motivos acima)|  
|**count_compiles**|**bigint**|Planeje as estatísticas de compilação.|  
|**initial_compile_start_time**|**datetimeoffset**|Planeje as estatísticas de compilação.|  
|**last_compile_start_time**|**datetimeoffset**|Planeje as estatísticas de compilação.|  
|**last_execution_time**|**datetimeoffset**|Último tempo de execução refere-se para a última hora de término do/plano de consulta.|  
|**avg_compile_duration**|**float**|Planeje as estatísticas de compilação.|  
|**last_compile_duration**|**bigint**|Planeje as estatísticas de compilação.|  
  
## <a name="plan-forcing-limitations"></a>Limitações de imposição de plano
O Repositório de Consultas tem um mecanismo para forçar o otimizador de consulta a usar um determinado plano de execução. No entanto, existem algumas limitações que podem impedir que um plano seja forçado. 

Primeiro, se o plano contém as seguintes construções:
* Instrução insert bulk.
* Instrução insert bulk.
* Referência a uma tabela externa
* Consulta distribuída ou operações de texto completo
* Uso de consultas globais 
* Cursores
* Especificação de junção em estrela inválida 

Segundo, quando os objetos dos quais o plano depende, não estão mais disponíveis:
* Banco de dados (se o banco de dados no qual o plano se originou não existe mais)
* Índice (não existe mais ou está desabilitado)

Por fim, problemas com o próprio plano:
* Não é válido para consulta
* O otimizador de consulta excedeu o número de operações permitidas
* XML do plano formatado incorretamente

## <a name="permissions"></a>Permissões  
 Requer o **VIEW DATABASE STATE** permissão.  
  
## <a name="see-also"></a>Consulte também  
 [sys.database_query_store_options &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-query-store-options-transact-sql.md)   
 [sys.query_context_settings &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-context-settings-transact-sql.md)   
 [sys.query_store_query &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-query-transact-sql.md)   
 [sys.query_store_query_text &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-query-text-transact-sql.md)   
 [sys.query_store_runtime_stats &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-runtime-stats-transact-sql.md)   
 [sys.query_store_wait_stats &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-wait-stats-transact-sql.md)  
 [sys.query_store_runtime_stats_interval &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-runtime-stats-interval-transact-sql.md)   
 [Monitorando o desempenho com o repositório de consultas](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)   
 [Exibições de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Procedimentos armazenados de Store de consulta &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/query-store-stored-procedures-transact-sql.md)  
  
  
