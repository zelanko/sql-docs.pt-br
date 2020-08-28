---
description: sys. dm_exec_query_plan_stats (Transact-SQL)
title: sys. dm_exec_query_plan_stats (Transact-SQL) | Microsoft Docs
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
ms.openlocfilehash: 0ab11e74205f47d50e927680081e8e13dfee37fb
ms.sourcegitcommit: 9be0047805ff14e26710cfbc6e10d6d6809e8b2c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2020
ms.locfileid: "89042469"
---
# <a name="sysdm_exec_query_plan_stats-transact-sql"></a>sys. dm_exec_query_plan_stats (Transact-SQL)
[!INCLUDE[SQL Server 2019](../../includes/tsql-appliesto-ssver15-asdb-xxxx-xxx.md)]

Retorna o equivalente do último plano de execução real conhecido para um plano de consulta armazenado em cache anteriormente.

## <a name="syntax"></a>Sintaxe

```
sys.dm_exec_query_plan_stats(plan_handle)  
``` 

## <a name="arguments"></a>Argumentos 
*plan_handle*  
É um token que identifica exclusivamente um plano de execução de consulta para um lote que foi executado e seu plano reside no cache de planos ou está em execução no momento. *plan_handle* é **varbinary (64)**.   

Os *plan_handle* podem ser obtidos nos seguintes objetos de gerenciamento dinâmico:  
  
-   [sys.dm_exec_cached_plans &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-cached-plans-transact-sql.md)  
  
-   [sys.dm_exec_query_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-stats-transact-sql.md)  
  
-   [sys.dm_exec_requests &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)  

-   [sys. dm_exec_procedure_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-procedure-stats-transact-sql.md)  

-   [sys. dm_exec_trigger_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-trigger-stats-transact-sql.md)  

## <a name="table-returned"></a>Tabela retornada

|Nome da coluna|Tipo de Dados|Descrição|  
|-----------------|---------------|-----------------|
|**DBID**|**smallint**|A ID do banco de dados de contexto em vigor quando a instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] correspondente a esse plano foi compilada. Para instruções SQL preparadas e ad hoc, a ID do banco de dados no qual as instruções foram compiladas.<br /><br /> A coluna é anulável.|  
|**objectid**|**int**|A identificação do objeto (por exemplo, procedimento armazenado ou função definida pelo usuário) para este plano de consulta. Para lotes ad hoc e preparados, essa coluna é **null**.<br /><br /> A coluna é anulável.|  
|**number**|**smallint**|Inteiro de procedimento armazenado numerado. Por exemplo, um grupo de procedimentos para o aplicativo de ** pedidos** pode ser nomeado **orderproc;1**, **orderproc;2** e assim por diante. Para lotes ad hoc e preparados, essa coluna é **null**.<br /><br /> A coluna é anulável.|  
|**criptografados**|**bit**|Indica se o procedimento armazenado correspondente está criptografado.<br /><br /> 0 = não criptografado<br /><br /> 1 = criptografado<br /><br /> A coluna não é anulável.|  
|**query_plan**|**xml**|Contém a última representação de SHOWPLAN de tempo de execução conhecida do plano de execução de consulta real que é especificado com *plan_handle*. O Showplan está em formato XML. Um plano é gerado para cada lote que contém, por exemplo, instruções ad hoc [!INCLUDE[tsql](../../includes/tsql-md.md)], chamadas de procedimento armazenado e chamadas de função definidas pelo usuário.<br /><br /> A coluna é anulável.| 

## <a name="remarks"></a>Comentários
Esse é um recurso de opção de aceitação. Para habilitar no nível do servidor, use o [sinalizador de rastreamento](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md) 2451. Para habilitar no nível de banco de dados, use a opção LAST_QUERY_PLAN_STATS em [ALTER DATABASE scopeed CONFIGURATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md).

Essa função do sistema funciona na infraestrutura de criação de perfil de estatísticas de execução de consulta **leve** . Para obter mais informações, confira [Infraestrutura de Criação de Perfil de Consulta](../../relational-databases/performance/query-profiling-infrastructure.md).  

A saída Showplan `sys.dm_exec_query_plan_stats` contém as seguintes informações:
-  Todas as informações de tempo de compilação encontradas no plano em cache
-  Informações de tempo de execução, como o número real de linhas por operador, o tempo total de CPU de consulta e o tempo de execução, avisos de despejo, DOP real, a memória máxima usada e a memória concedida

Sob as condições a seguir, uma saída Showplan **equivalente a um plano de execução real** é retornada na coluna **query_plan** da tabela retornada para `sys.dm_exec_query_plan_stats` :  

-   O plano pode ser encontrado em [Sys. dm_exec_cached_plans](../../relational-databases/system-dynamic-management-views/sys-dm-exec-cached-plans-transact-sql.md).     
    **AND**    
-   A consulta que está sendo executada é complexa ou consumida por recursos.

Sob as condições a seguir, uma saída **simplificada de <sup>1</sup> ** plano de segundo é retornada na coluna **query_plan** da tabela retornada para `sys.dm_exec_query_plan_stats` :  

-   O plano pode ser encontrado em [Sys. dm_exec_cached_plans](../../relational-databases/system-dynamic-management-views/sys-dm-exec-cached-plans-transact-sql.md).     
    **AND**    
-   A consulta é simples o suficiente, normalmente categorizada como parte de uma carga de trabalho OLTP.

<sup>1</sup> refere-se a um Showplan que contém apenas o operador de nó raiz (SELECT).

Sob as seguintes condições, **nenhuma saída é retornada** de `sys.dm_exec_query_plan_stats` :

-   O plano de consulta especificado usando `plan_handle` o foi removido do cache de planos.     
    **OR**    
-   O plano de consulta não estava armazenado em cache em primeiro lugar. Para obter mais informações, consulte [cache e reutilização do plano de execução ](../../relational-databases/query-processing-architecture-guide.md#execution-plan-caching-and-reuse).
  
> [!NOTE] 
> Devido a uma limitação no número de níveis aninhados permitido no tipo de dados **XML** , o `sys.dm_exec_query_plan` não pode retornar planos de consulta que atendam ou ultrapassem 128 níveis de elementos aninhados. Em versões anteriores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , essa condição impediu que o plano de consulta retornasse e gerasse o [erro 6335](../../relational-databases/errors-events/database-engine-events-and-errors.md#errors-6000-to-6999). No [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] Service Pack 2 e versões posteriores, a `query_plan` coluna retorna NULL.  

## <a name="permissions"></a>Permissões  
 Requer a permissão `VIEW SERVER STATE` no servidor.  

## <a name="examples"></a>Exemplos  
  
### <a name="a-looking-at-last-known-actual-query-execution-plan-for-a-specific-cached-plan"></a>a. Examinando o último plano de execução de consulta real conhecido para um plano em cache específico  
 O exemplo a seguir consulta **Sys. dm_exec_cached_plans** para localizar o plano interessante e copiar seu `plan_handle` da saída.  
  
```sql  
SELECT * FROM sys.dm_exec_cached_plans;  
GO  
```  
  
Em seguida, para obter o último plano de execução de consulta real conhecido, use a `plan_handle` função de sistema Copie com **sys. dm_exec_query_plan_stats**.  
  
```sql  
SELECT * FROM sys.dm_exec_query_plan_stats(< copied plan_handle >);  
GO  
```   

### <a name="b-looking-at-last-known-actual-query-execution-plan-for-all-cached-plans"></a>B. Examinando o último plano de execução de consulta real conhecido para todos os planos em cache
  
```sql  
SELECT *   
FROM sys.dm_exec_cached_plans AS cp
CROSS APPLY sys.dm_exec_sql_text(plan_handle) AS st
CROSS APPLY sys.dm_exec_query_plan_stats(plan_handle) AS qps;  
GO  
```   

### <a name="c-looking-at-last-known-actual-query-execution-plan-for-a-specific-cached-plan-and-query-text"></a>C. Examinando o último plano de execução de consulta real conhecido para um plano armazenado em cache e um texto de consulta específicos

```sql  
SELECT *   
FROM sys.dm_exec_cached_plans AS cp
CROSS APPLY sys.dm_exec_sql_text(plan_handle) AS st
CROSS APPLY sys.dm_exec_query_plan_stats(plan_handle) AS qps
WHERE st.text LIKE 'SELECT * FROM Person.Person%';  
GO  
```   

### <a name="d-look-at-cached-events-for-trigger"></a>D. Examinar eventos em cache para o gatilho

```sql
SELECT *
FROM sys.dm_exec_cached_plans
CROSS APPLY sys.dm_exec_query_plan_stats(plan_handle)
WHERE objtype ='Trigger';
GO
```

## <a name="see-also"></a>Consulte Também
  [Sinalizadores de rastreamento](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md)  
 [Exibições e funções de gerenciamento dinâmico &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Exibições de gerenciamento dinâmico relacionadas à execução &#40;&#41;Transact-SQL ](../../relational-databases/system-dynamic-management-views/execution-related-dynamic-management-views-and-functions-transact-sql.md)  

