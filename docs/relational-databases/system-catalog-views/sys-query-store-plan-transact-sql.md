---
title: sys. query_store_plan (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/23/2019
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
monikerRange: =azuresqldb-current||>=sql-server-2016||= azure-sqldw-latest||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 1d1137aab32a98a4699e95b7138bb333f63c65e9
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "74479461"
---
# <a name="sysquery_store_plan-transact-sql"></a>sys.query_store_plan (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-asdw-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-asdw-xxx-md.md)]

  Contém informações sobre cada plano de execução associado a uma consulta.  
  
|Nome da coluna|Tipo de dados|DESCRIÇÃO|  
|-----------------|---------------|-----------------|
|**plan_id**|**bigint**|Chave primária.|  
|**query_id**|**bigint**|Chave estrangeira. Junções em [Sys. query_store_query &#40;&#41;Transact-SQL ](../../relational-databases/system-catalog-views/sys-query-store-query-transact-sql.md).|  
|**plan_group_id**|**bigint**|ID do grupo de planos. As consultas de cursor normalmente exigem vários planos (popular e buscar). Preencher e buscar planos que são compilados juntos estão no mesmo grupo.<br /><br /> 0 significa que o plano não está em um grupo.|  
|**engine_version**|**nvarchar (32)**|Versão do mecanismo usada para compilar o plano no formato **' major. Minor. Build. Revision '** .|  
|**compatibility_level**|**smallint**|Nível de compatibilidade do banco de dados referenciado na consulta.|  
|**query_plan_hash**|**binário (8)**|Hash MD5 do plano individual.|  
|**query_plan**|**nvarchar(max)**|Showplan XML para o plano de consulta.|  
|**is_online_index_plan**|**bit**|O plano foi usado durante uma compilação de índice online. <br/>**Observação:** O SQL Data Warehouse do Azure sempre retornará zero (0).|  
|**is_trivial_plan**|**bit**|O plano é um plano trivial (saída no estágio 0 do otimizador de consulta). <br/>**Observação:** O SQL Data Warehouse do Azure sempre retornará zero (0).|  
|**is_parallel_plan**|**bit**|O plano é paralelo. <br/>**Observação:** O SQL Data Warehouse do Azure sempre retornará um (1).|  
|**is_forced_plan**|**bit**|O plano é marcado como forçado quando o usuário executa o procedimento armazenado **Sys. sp_query_store_force_plan**. O mecanismo de forçação *não garante* que exatamente esse plano será usado para a consulta referenciada pelo **query_id**. A imposição de plano faz com que a consulta seja compilada novamente e, normalmente, produz exatamente o mesmo plano ou semelhante ao plano referenciado por **plan_id**. Se a imposição de plano não for bem sucedido, **force_failure_count** será incrementado e **last_force_failure_reason** será populado com o motivo da falha. <br/>**Observação:** O SQL Data Warehouse do Azure sempre retornará zero (0).|  
|**is_natively_compiled**|**bit**|O plano inclui procedimentos com otimização de memória compilados nativamente. (0 = FALSE, 1 = TRUE). <br/>**Observação:** O SQL Data Warehouse do Azure sempre retornará zero (0).|  
|**force_failure_count**|**bigint**|Número de vezes que a força deste plano falhou. Ele pode ser incrementado somente quando a consulta é recompilada (*não em cada execução*). Ele é redefinido para 0 sempre que **is_plan_forced** é alterado de **false** para **true**. <br/>**Observação:** O SQL Data Warehouse do Azure sempre retornará zero (0).|  
|**last_force_failure_reason**|**int**|Motivo pelo qual a imposição de plano falhou.<br /><br /> 0: nenhuma falha; caso contrário, número do erro que causou a falha na imposição<br /><br /> 8637: ONLINE_INDEX_BUILD<br /><br /> 8683: INVALID_STARJOIN<br /><br /> 8684: TIME_OUT<br /><br /> 8689: NO_DB<br /><br /> 8690: HINT_CONFLICT<br /><br /> 8691: SETOPT_CONFLICT<br /><br /> 8694: DQ_NO_FORCING_SUPPORTED<br /><br /> 8698: NO_PLAN<br /><br /> 8712: NO_INDEX<br /><br /> 8713: VIEW_COMPILE_FAILED<br /><br /> \<outro valor>: GENERAL_FAILURE <br/>**Observação:** O SQL Data Warehouse do Azure sempre retornará zero (0).|  
|**last_force_failure_reason_desc**|**nvarchar(128)**|Descrição textual de last_force_failure_reason_desc.<br /><br /> ONLINE_INDEX_BUILD: a consulta tenta modificar os dados enquanto a tabela de destino tem um índice que está sendo compilado online<br /><br /> INVALID_STARJOIN: o plano contém uma especificação de StarJoin inválida<br /><br /> TIME_OUT: o otimizador excedeu o número de operações permitidas ao pesquisar o plano especificado pelo plano forçado<br /><br /> NO_DB: um banco de dados especificado no plano não existe<br /><br /> HINT_CONFLICT: a consulta não pode ser compilada porque o plano está em conflito com uma dica de consulta<br /><br /> DQ_NO_FORCING_SUPPORTED: não é possível executar a consulta porque o plano está em conflito com o uso de consultas distribuídas ou operações de texto completo.<br /><br /> NO_PLAN: o processador de consultas não pôde produzir o plano de consulta porque não foi possível verificar o plano forçado como válido para a consulta<br /><br /> NO_INDEX: o índice especificado no plano não existe mais<br /><br /> VIEW_COMPILE_FAILED: não foi possível forçar o plano de consulta devido a um problema em uma exibição indexada referenciada no plano<br /><br /> GENERAL_FAILURE: erro de força geral (não coberto por motivos acima) <br/>**Observação:** O SQL Data Warehouse do Azure sempre retornará *nenhum*.|  
|**count_compiles**|**bigint**|Planejar estatísticas de compilação.|  
|**initial_compile_start_time**|**datetimeoffset**|Planejar estatísticas de compilação.|  
|**last_compile_start_time**|**datetimeoffset**|Planejar estatísticas de compilação.|  
|**last_execution_time**|**datetimeoffset**|A hora da última execução refere-se à última hora de término da consulta/plano.|  
|**avg_compile_duration**|**float**|Planejar estatísticas de compilação. <br/>**Observação:** O SQL Data Warehouse do Azure sempre retornará zero (0).|  
|**last_compile_duration**|**bigint**|Planejar estatísticas de compilação. <br/>**Observação:** O SQL Data Warehouse do Azure sempre retornará zero (0).|  
|**plan_forcing_type**|**int**|Tipo de imposição de plano.<br /><br />0: NENHUM<br /><br />1: MANUAL<br /><br />2: AUTOMÁTICO|  
|**plan_forcing_type_desc**|**nvarchar (60)**|Descrição de texto de plan_forcing_type.<br /><br />NENHUM: nenhum plano impondo<br /><br />MANUAL: plano forçado pelo usuário<br /><br />AUTOMÁTICO: plano forçado pelo ajuste automático|  

## <a name="plan-forcing-limitations"></a>Limitações forçadas do plano
O Repositório de Consultas tem um mecanismo para forçar o otimizador de consulta a usar um determinado plano de execução. No entanto, existem algumas limitações que podem impedir que um plano seja forçado. 

Primeiro, se o plano contém as seguintes construções:
* Instrução insert bulk.
* Referência a uma tabela externa
* Consulta distribuída ou operações de texto completo
* Uso de consultas globais 
* Cursores dinâmicos ou de conjunto de chaves 
* Especificação de junção em estrela inválida 

> [!NOTE]
> O banco de dados SQL do Azure e o plano de suporte do SQL Server 2019 são impondo para cursores estáticos e rápidos.

Segundo, quando os objetos dos quais o plano depende, não estão mais disponíveis:
* Banco de dados (se o banco de dados no qual o plano se originou não existe mais)
* Índice (não existe mais ou está desabilitado)

Por fim, problemas com o próprio plano:
* Não é válido para consulta
* O otimizador de consulta excedeu o número de operações permitidas
* XML do plano formatado incorretamente

## <a name="permissions"></a>Permissões  
 Requer a permissão **View Database State** .  
  
## <a name="see-also"></a>Consulte Também  
 [sys. database_query_store_options &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-query-store-options-transact-sql.md)   
 [sys. query_context_settings &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-context-settings-transact-sql.md)   
 [sys. query_store_query &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-query-transact-sql.md)   
 [sys. query_store_query_text &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-query-text-transact-sql.md)   
 [sys. query_store_runtime_stats &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-runtime-stats-transact-sql.md)   
 [sys. query_store_wait_stats &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-wait-stats-transact-sql.md)  
 [sys. query_store_runtime_stats_interval &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-runtime-stats-interval-transact-sql.md)   
 [Monitorando o desempenho com o repositório de consultas](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)   
 [Exibições de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Procedimentos armazenados do Repositório de Consultas &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/query-store-stored-procedures-transact-sql.md)  
  
  
