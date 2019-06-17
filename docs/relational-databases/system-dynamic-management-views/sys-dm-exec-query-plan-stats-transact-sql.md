---
title: sys.dm_exec_query_plan_stats (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 05/22/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: conceptual
f1_keywords:
- sys.dm_exec_query_plan_stats
- sys.dm_exec_query_plan_stats_TSQL
- dm_exec_query_plan_stats_TSQL
- dm_exec_query_plan_stats
helpviewer_keywords:
- sys.dm_exec_query_plan_stats management view
ms.assetid: fdc7659e-df41-488e-b2b5-0d79734dfacb
author: pmasl
ms.author: pelopes
manager: amitban
ms.openlocfilehash: c4d4f58161885519767e299683fe32b5197a045f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66198213"
---
# <a name="sysdmexecqueryplanstats-transact-sql"></a>sys.dm_exec_query_plan_stats (Transact-SQL)
[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../../includes/tsql-appliesto-ssver15-asdb-xxxx-xxx.md)]

Retorna o equivalente do último plano de execução real conhecido para um plano de consulta armazenados em cache anteriormente.

## <a name="syntax"></a>Sintaxe

```
sys.dm_exec_query_plan_stats(plan_handle)  
``` 

## <a name="arguments"></a>Argumentos 
*plan_handle*  
É um token que identifica exclusivamente um plano de execução de consulta para um lote que foi executado e seu plano reside no cache de plano ou em execução no momento. *plan_handle* is **varbinary(64)** .   

O *plan_handle* pode ser obtido dos seguintes objetos de gerenciamento dinâmico:  
  
-   [sys.dm_exec_cached_plans &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-cached-plans-transact-sql.md)  
  
-   [sys.dm_exec_query_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-stats-transact-sql.md)  
  
-   [sys.dm_exec_requests &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)  

-   [sys.dm_exec_procedure_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-procedure-stats-transact-sql.md)  

-   [sys.dm_exec_trigger_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-trigger-stats-transact-sql.md)  

## <a name="table-returned"></a>Tabela retornada

|Nome da coluna|Tipo de Dados|Descrição|  
|-----------------|---------------|-----------------|
|**dbid**|**smallint**|A ID do banco de dados de contexto em vigor quando a instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] correspondente a esse plano foi compilada. Para instruções SQL preparadas e ad hoc, a ID do banco de dados no qual as instruções foram compiladas.<br /><br /> A coluna é anulável.|  
|**objectid**|**int**|A identificação do objeto (por exemplo, procedimento armazenado ou função definida pelo usuário) para este plano de consulta. Para lotes ad hoc e preparadas, essa coluna é **nulo**.<br /><br /> A coluna é anulável.|  
|**number**|**smallint**|Inteiro de procedimento armazenado numerado. Por exemplo, um grupo de procedimentos para o **pedidos** aplicativo pode ser nomeado **orderproc; 1**, **orderproc; 2**e assim por diante. Para lotes ad hoc e preparadas, essa coluna é **nulo**.<br /><br /> A coluna é anulável.|  
|**encrypted**|**bit**|Indica se o procedimento armazenado correspondente está criptografado.<br /><br /> 0 = não criptografado<br /><br /> 1 = criptografado<br /><br /> A coluna não é anulável.|  
|**query_plan**|**xml**|Contém o último conhecido em tempo de execução representação do plano de execução do plano de execução de consulta real que é especificado com *plan_handle*. O Showplan está em formato XML. Um plano é gerado para cada lote que contém, por exemplo, instruções ad hoc [!INCLUDE[tsql](../../includes/tsql-md.md)], chamadas de procedimento armazenado e chamadas de função definidas pelo usuário.<br /><br /> A coluna é anulável.| 

## <a name="remarks"></a>Comentários
Essa função do sistema está disponível começando com [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] CTP 2.4.

Esse é um recurso opcional e requer que o [sinalizador de rastreamento](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md) 2451 esteja habilitado. Começando com [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] 2.5 CTP, para fazer isso no nível do banco de dados, consulte a opção LAST_QUERY_PLAN_STATS [ALTER DATABASE SCOPED CONFIGURATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md).

Essa função do sistema funciona sob o **leve** infraestrutura de criação de perfil de estatísticas de execução de consulta. Para obter mais informações, confira [Infraestrutura de Criação de Perfil de Consulta](../../relational-databases/performance/query-profiling-infrastructure.md).  

Sob as condições a seguir, um plano de execução de saída **equivalente a um plano de execução real** é retornado na **query_plan** coluna da tabela retornada para **sys.dm_exec_query_plan_ estatísticas de**:  

-   O plano pode ser encontrado na [DM exec_cached_plans](../../relational-databases/system-dynamic-management-views/sys-dm-exec-cached-plans-transact-sql.md).     
    **AND**    
-   A consulta que está sendo executada é complexo ou consumo de recursos.

Sob as seguintes condições, uma **simplificada <sup>1</sup>**  saída Showplan é retornada no **query_plan** coluna da tabela retornada para **sys.dm_exec_ query_plan_stats**:  

-   O plano pode ser encontrado na [DM exec_cached_plans](../../relational-databases/system-dynamic-management-views/sys-dm-exec-cached-plans-transact-sql.md).     
    **AND**    
-   A consulta é simple o suficiente, geralmente categorizados como parte de uma carga de trabalho OLTP.

<sup>1</sup> começando com [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] CTP 2.5, isso se refere a um plano de execução que contém apenas o operador de nó raiz (Selecionar). Para [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] refere-se para o plano armazenado em cache como disponível por meio do CTP 2.4 `sys.dm_exec_cached_plans`.

Nas seguintes condições **nenhuma saída é retornada** partir **sys.dm_exec_query_plan_stats**:

-   O plano de consulta é especificado usando *plan_handle* foi removido do cache do plano.     
    **OR**    
-   O plano de consulta não foi armazenável em cache em primeiro lugar. Para obter mais informações, consulte [cache de plano de execução e reutilização ](../../relational-databases/query-processing-architecture-guide.md#execution-plan-caching-and-reuse).
  
> [!NOTE] 
> Devido a uma limitação no número de níveis aninhados permitida na **xml** tipo de dados **. DM exec_query_plan** não pode retornar planos de consulta que atendem ou excedem 128 níveis de elementos aninhados. Em versões anteriores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], esta condição impediu que o plano de consulta retornando e gera [erro 6335](../../relational-databases/errors-events/database-engine-events-and-errors.md#errors-6000-to-6999). Na [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] Service Pack 2 e versões posteriores, o **query_plan** coluna retorna NULL.  

## <a name="permissions"></a>Permissões  
 Requer a permissão `VIEW SERVER STATE` no servidor.  

## <a name="examples"></a>Exemplos  
  
### <a name="a-looking-at-last-known-actual-query-execution-plan-for-a-specific-cached-plan"></a>A. Procurando pelo último plano de execução de consulta real conhecidos um plano armazenado em cache específico  
 A exemplo a seguir consulta **DM exec_cached_plans** para localizar o plano de interessante e copiar seu `plan_handle` da saída.  
  
```sql  
SELECT * FROM sys.dm_exec_cached_plans;  
GO  
```  
  
Em seguida, para obter o último plano de execução conhecidos consulta propriamente dita, use copiado `plan_handle` com a função do sistema **sys.dm_exec_query_plan_stats**.  
  
```sql  
SELECT * FROM sys.dm_exec_query_plan_stats(< copied plan_handle >);  
GO  
```   

### <a name="b-looking-at-last-known-actual-query-execution-plan-for-all-cached-plans"></a>B. Procurando pelo último plano de execução de consulta real conhecidos todos os planos em cache
  
```sql  
SELECT *   
FROM sys.dm_exec_cached_plans AS cp
CROSS APPLY sys.dm_exec_sql_text(plan_handle) AS st
CROSS APPLY sys.dm_exec_query_plan_stats(plan_handle) AS qps;  
GO  
```   

### <a name="c-looking-at-last-known-actual-query-execution-plan-for-a-specific-cached-plan-and-query-text"></a>C. Procurando pelo último plano de execução de consulta real conhecidos um plano armazenado em cache específico e o texto da consulta

```sql  
SELECT *   
FROM sys.dm_exec_cached_plans AS cp
CROSS APPLY sys.dm_exec_sql_text(plan_handle) AS st
CROSS APPLY sys.dm_exec_query_plan_stats(plan_handle) AS qps
WHERE st.text LIKE 'SELECT * FROM Person.Person%';  
GO  
```   

### <a name="d-look-at-cached-events-for-trigger"></a>D. Examinar eventos armazenados em cache para o gatilho

```sql
SELECT *
FROM sys.dm_exec_cached_plans
CROSS APPLY sys.dm_exec_query_plan_stats(plan_handle)
WHERE objtype ='Trigger';
GO
```

## <a name="see-also"></a>Consulte também
  [Sinalizadores de rastreamento](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md)  
 [Exibições e funções de gerenciamento dinâmico &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Exibições de gerenciamento dinâmico relacionadas à execução &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/execution-related-dynamic-management-views-and-functions-transact-sql.md)  

