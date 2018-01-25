---
title: DBCC FREEPROCCACHE (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 10/13/2017
ms.prod: sql-non-specified
ms.prod_service: sql-data-warehouse, pdw, sql-database
ms.service: 
ms.component: t-sql|database-console-commands
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- FREEPROCCACHE_TSQL
- FREEPROCCACHE
- DBCC_FREEPROCCACHE_TSQL
- DBCC FREEPROCCACHE
dev_langs: TSQL
helpviewer_keywords:
- freeing procedure cache
- removing procedure cache elements
- deleting procedure cache elements
- DBCC FREEPROCCACHE statement
- procedure cache [SQL Server]
- clearing procedure cache
ms.assetid: 0e09d210-6f23-4129-aedb-3d56b2980683
caps.latest.revision: "61"
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: Active
ms.openlocfilehash: b5fd65fa2a764d87d2c5481a7c20560551ca3311
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/25/2018
---
# <a name="dbcc-freeproccache-transact-sql"></a>DBCC FREEPROCCACHE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-xxxx-asdw-pdw-md.md)]

Remove todos os elementos do cache do plano, remove um plano específico do cache do plano, por meio da especificação de um identificador de plano ou identificador SQL ou remove todas as entradas de cache com um pool de recursos especificado.

>[!NOTE]
>DBCC FREEPROCCACHE não desmarca as estatísticas de execução para procedimentos armazenados compilados de modo nativo. O cache de procedimento não contém informações sobre procedimentos armazenados compilados de modo nativo. Todas as estatísticas de execução coletadas de execuções de procedimento aparecerão nas DMVs de estatísticas de execução: [sys.DM exec_procedure_stats &#40; Transact-SQL &#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-exec-procedure-stats-transact-sql.md) e [sys.DM exec_query_plan &#40; Transact-SQL &#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-plan-transact-sql.md).  
  
![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxe  
Sintaxe do SQL Server:

```sql
DBCC FREEPROCCACHE [ ( { plan_handle | sql_handle | pool_name } ) ] [ WITH NO_INFOMSGS ]  
```  

Sintaxe de SQL do Azure Data Warehouse e o Parallel Data Warehouse:
  
```sql
DBCC FREEPROCCACHE [ ( COMPUTE | ALL ) ] 
     [ WITH NO_INFOMSGS ]   
[;]  
```  
  
## <a name="arguments"></a>Argumentos  
 ( { *plan_handle* | *sql_handle* | *pool_name* } )  
*plan_handle* identifica exclusivamente um plano de consulta para um lote que foi executado e cujo plano reside no cache de plano. *plan_handle* é **varbinary(64)** e pode ser obtido dos seguintes objetos de gerenciamento dinâmico:  
 -   [sys.dm_exec_cached_plans](../../relational-databases/system-dynamic-management-views/sys-dm-exec-cached-plans-transact-sql.md)  
 -   [sys.dm_exec_requests](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)  
 -   [sys.dm_exec_query_memory_grants](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-memory-grants-transact-sql.md)  
 -   [sys.dm_exec_query_stats](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-stats-transact-sql.md)  

*sql_handle* é o identificador SQL do lote a ser apagado. *sql_handle* é **varbinary(64)** e pode ser obtido dos seguintes objetos de gerenciamento dinâmico:  
 -   [sys.dm_exec_query_stats](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-stats-transact-sql.md)  
 -   [sys.dm_exec_requests](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)  
 -   [sys.dm_exec_cursors](../../relational-databases/system-dynamic-management-views/sys-dm-exec-cursors-transact-sql.md)  
 -   [sys.dm_exec_xml_handles](../../relational-databases/system-dynamic-management-views/sys-dm-exec-xml-handles-transact-sql.md)  
 -   [sys.dm_exec_query_memory_grants](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-memory-grants-transact-sql.md)  

*nome_do_pool* é o nome de um pool de recursos do administrador de recursos. *nome_do_pool* é **sysname** e pode ser obtido consultando o [sys.DM resource_governor_resource_pools](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-resource-pools-transact-sql.md) exibição de gerenciamento dinâmico.  
 Para associar um grupo de carga de trabalho do administrador de recursos um pool de recursos, consulte o [sys.DM resource_governor_workload_groups](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-workload-groups-transact-sql.md) exibição de gerenciamento dinâmico. Para obter informações sobre o grupo de carga de trabalho para uma sessão, consulte o [sys.DM exec_sessions](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sessions-transact-sql.md) exibição de gerenciamento dinâmico.  

  
 WITH NO_INFOMSGS  
 Suprime todas as mensagens informativas.  
  
 COMPUTE  
 Limpe o cache do plano de consulta de cada nó de computação. Este é o valor padrão.  
  
 ALL  
 Limpe o cache do plano de consulta de cada nó de computação e a partir do nó de controle.  

> [!NOTE]
> Começando com [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)], o `ALTER DATABASE SCOPED CONFIGURATION CLEAR PROCEDURE_CACHE` para limpar o cache de procedimento (plano) para o banco de dados no escopo.

## <a name="remarks"></a>Remarks  
Use DBCC FREEPROCCACHE para limpar o cache do plano cuidadosamente. Limpando o procedimento (plano) faz com que o cache de todos os planos a ser removido e consulta de entrada execuções compilará um novo plano, em vez de reutilizá qualquer plano armazenado em cache anteriormente. 

Isso pode causar uma queda repentina e temporária no desempenho de consulta conforme o número de novas compilações. Para cada armazenamento em cache limpo no cache do plano, o log de erros do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] conterá a seguinte mensagem informativa: "O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] encontrou %d ocorrência(s) de liberação de armazenamento em cache '% s' (parte do cache do plano) devido às operações 'DBCC FREEPROCCACHE' ou 'DBCC FREESYSTEMCACHE'". Essa mensagem é registrada a cada cinco minutos, contanto que o cache seja liberado dentro desse intervalo de tempo.

As seguintes operações de reconfiguração também são limpas no cache de procedimento:
-   contagem de bucket do cache de verificação de acesso  
-   cota de cache de verificação de acesso  
-   clr enabled  
-   limite de custo para paralelismo  
-   cross db ownership chaining  
-   memória para criar índice  
-   grau máximo de paralelismo  
-   max server memory  
-   max text repl size  
-   máximo de threads de trabalho  
-   min memory per query  
-   min server memory  
-   limite de custo do administrador de consulta  
-   espera da consulta  
-   remote query timeout  
-   opções de usuário  
  
## <a name="result-sets"></a>Conjuntos de resultados  
Quando a cláusula WITH NO_INFOMSGS não for especificada, DBCC FREEPROCCACHE retornará: "execução do DBCC foi concluída. Se o DBCC imprimiu mensagens de erro, entre em contato com o administrador do sistema".
  
## <a name="permissions"></a>Permissões  
Aplica-se a: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)],[!INCLUDE[ssPDW](../../includes/sspdw-md.md)] 
- Exige a permissão ALTER SERVER STATE no servidor.  

Aplica-se a:[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]
- Requer associação na função de servidor fixa DB_OWNER.  

## <a name="general-remarks-for-includesssdwincludessssdw-mdmd-and-includesspdwincludessspdw-mdmd"></a>Comentários gerais para [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] e[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
Vários comandos DBCC FREEPROCCACHE podem ser executados simultaneamente.
Em [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] ou [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], limpar o cache de plano pode causar uma queda temporária no desempenho de consulta como um novo plano de compilação de consultas de entrada, em vez de reutilizá qualquer anteriormente plano armazenado em cache. 

DBCC FREEPROCCACHE (computação) faz com que apenas [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para recompilar consultas quando eles são executados em nós de computação. Ela não causa o [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] ou [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] para recompilar um plano de consulta paralela que é gerado no nó de controle.
DBCC FREEPROCCACHE pode ser cancelado durante a execução.
  
## <a name="limitations-and-restrictions-for-includesssdwincludessssdw-mdmd-and-includesspdwincludessspdw-mdmd"></a>Limitações e restrições para [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] e[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
DBCC FREEPROCCACHE não pode ser executado em uma transação.
Não há suporte para DBCC FREEPROCCAHCE em uma instrução de EXPLICAR.
  
## <a name="metadata-for-includesssdwincludessssdw-mdmd-and-includesspdwincludessspdw-mdmd"></a>Metadados para [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] e[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
Uma nova linha é adicionada ao modo de exibição de sistema sys.pdw_exec_requests quando DBCC FREEPROCCACHE é executado.

## <a name="examples-includessnoversionincludesssnoversion-mdmd"></a>Exemplos:[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
### <a name="a-clearing-a-query-plan-from-the-plan-cache"></a>A. Apagando um plano de consulta do cache do plano  
O exemplo a seguir apaga um plano de consulta do cache do plano especificando o identificador do plano de consulta. Para assegurar que a consulta de exemplo esteja no cache do plano, a consulta será executada primeiro. O `sys.dm_exec_cached_plans` e `sys.dm_exec_sql_text` exibições de gerenciamento dinâmico são consultadas para retornar o identificador de plano para a consulta. 

O valor do identificador do plano do conjunto de resultados é inserido na instrução `DBCC FREEPROCACHE` para remover apenas o plano em questão do cache do plano.
  
```sql  
USE AdventureWorks2012;  
GO  
SELECT * FROM Person.Address;  
GO  
SELECT plan_handle, st.text  
FROM sys.dm_exec_cached_plans   
CROSS APPLY sys.dm_exec_sql_text(plan_handle) AS st  
WHERE text LIKE N'SELECT * FROM Person.Address%';  
GO  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]

```
plan_handle                                         text  
--------------------------------------------------  -----------------------------  
0x060006001ECA270EC0215D05000000000000000000000000  SELECT * FROM Person.Address;  
  
(1 row(s) affected)
 ```
 
```sql  
-- Remove the specific plan from the cache.  
DBCC FREEPROCCACHE (0x060006001ECA270EC0215D05000000000000000000000000);  
GO  
```  
  
### <a name="b-clearing-all-plans-from-the-plan-cache"></a>B. Limpando todos os planos do cache do plano  
O exemplo a seguir limpa todos os elementos do cache do plano. WITH `NO_INFOMSGS` cláusula for especificada para impedir que a mensagem de informação que está sendo exibido.
  
```sql  
DBCC FREEPROCCACHE WITH NO_INFOMSGS;  
```  
  
### <a name="c-clearing-all-cache-entries-associated-with-a-resource-pool"></a>C. Limpando todas as entradas do cache associadas a um pool de recursos  
O exemplo a seguir limpa todas as entradas do cache associadas a um pool de recursos especificado. O `sys.dm_resource_governor_resource_pools` exibição é consultada primeiro para obter o valor de *nome_do_pool*.
  
```sql  
SELECT * FROM sys.dm_resource_governor_resource_pools;  
GO  
DBCC FREEPROCCACHE ('default');  
GO  
```  
  
## <a name="examples-includesssdwincludessssdw-mdmd-and-includesspdwincludessspdw-mdmd"></a>Exemplos: [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] e[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="d-dbcc-freeproccache-basic-syntax-examples"></a>D. Exemplos de sintaxe básica de DBCC FREEPROCCACHE  
O exemplo a seguir remove todos os caches de plano de consulta existente de nós de computação. Embora o contexto é definido como UserDbSales, os caches de plano de consulta de nó computação para todos os bancos de dados serão serão removidos. A cláusula WITH NO_INFOMSGS impede que mensagens informativas que aparecem nos resultados.  
  
```sql
USE UserDbSales;  
DBCC FREEPROCCACHE (COMPUTE) WITH NO_INFOMSGS;
```  
  
 O exemplo a seguir tem os mesmos resultados do exemplo anterior, exceto que as mensagens informativas serão exibidas nos resultados.  
  
```sql
USE UserDbSales;  
DBCC FREEPROCCACHE (COMPUTE);  
```  
  
Quando são solicitadas mensagens informativas e a execução for bem-sucedida, os resultados da consulta terá uma linha por nó de computação.
  
### <a name="e-granting-permission-to-run-dbcc-freeproccache"></a>E. Concedendo permissão para executar DBCC FREEPROCCACHE  
O exemplo a seguir fornece o David permissão logon para executar DBCC FREEPROCCACHE.  
  
```sql
GRANT ALTER SERVER STATE TO David; 
GO
```  
  
## <a name="see-also"></a>Consulte também  
[DBCC &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-transact-sql.md)  
[Administrador de Recursos](../../relational-databases/resource-governor/resource-governor.md)  
[ALTER DATABASE SCOPED CONFIGURATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md)
  
  
