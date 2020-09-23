---
description: DBCC FREEPROCCACHE (Transact-SQL)
title: DBCC FREEPROCCACHE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 10/13/2017
ms.prod: sql
ms.prod_service: sql-data-warehouse, pdw, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- FREEPROCCACHE_TSQL
- FREEPROCCACHE
- DBCC_FREEPROCCACHE_TSQL
- DBCC FREEPROCCACHE
dev_langs:
- TSQL
helpviewer_keywords:
- freeing procedure cache
- removing procedure cache elements
- deleting procedure cache elements
- DBCC FREEPROCCACHE statement
- procedure cache [SQL Server]
- clearing procedure cache
ms.assetid: 0e09d210-6f23-4129-aedb-3d56b2980683
author: pmasl
ms.author: umajay
monikerRange: '>=aps-pdw-2016||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 583bed1efb0f19b1924fe007be7a6f49c2587a52
ms.sourcegitcommit: 1126792200d3b26ad4c29be1f561cf36f2e82e13
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/14/2020
ms.locfileid: "90076600"
---
# <a name="dbcc-freeproccache-transact-sql"></a>DBCC FREEPROCCACHE (Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

Remove todos os elementos do cache do plano, remove um plano específico do cache do plano, por meio da especificação de um identificador de plano ou identificador SQL ou remove todas as entradas de cache com um pool de recursos especificado.

> [!NOTE]
> DBCC FREEPROCCACHE não desmarca as estatísticas de execução para procedimentos armazenados compilados de modo nativo. O cache de procedimento não contém informações sobre procedimentos armazenados compilados de modo nativo. Todas as estatísticas de execução coletadas de execuções de procedimento serão exibidas nas DMVs de estatísticas de execução: [sys.dm_exec_procedure_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-procedure-stats-transact-sql.md) e [sys.dm_exec_query_plan &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-plan-transact-sql.md).  
  
![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxe  
Sintaxe para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:

```sql
DBCC FREEPROCCACHE [ ( { plan_handle | sql_handle | pool_name } ) ] [ WITH NO_INFOMSGS ]  
```  

Sintaxe para [!INCLUDE[ssSDW](../../includes/sssdwfull-md.md)] e [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]:
  
```sql
DBCC FREEPROCCACHE [ ( COMPUTE | ALL ) ] 
     [ WITH NO_INFOMSGS ]   
[;]  
```  

[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>Argumentos
 ( { *plan_handle* | *sql_handle* | *pool_name* } )  
*plan_handle* identifica exclusivamente um plano de consulta de um lote que foi executado e cujo plano reside no cache de planos. *plan_handle* é **varbinary(64)** e pode ser obtido dos seguintes objetos de gerenciamento dinâmico:  
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

*pool_name* é o nome de um pool de recursos do Resource Governor. *pool_name* é **sysname** e pode ser obtido por meio da consulta da exibição de gerenciamento dinâmico [sys.dm_resource_governor_resource_pools](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-resource-pools-transact-sql.md).  
 Para associar um grupo de carga de trabalho do Resource Governor a um pool de recursos, consulte a exibição de gerenciamento dinâmico [sys.dm_resource_governor_workload_groups](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-workload-groups-transact-sql.md). Para obter informações sobre o grupo de carga de trabalho durante uma sessão, consulte a exibição de gerenciamento dinâmico [sys.dm_exec_sessions](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sessions-transact-sql.md).  

  
 WITH NO_INFOMSGS  
 Suprime todas as mensagens informativas.  
  
 COMPUTE  
 Limpe o cache de planos de consulta de cada nó de Computação. Este é o valor padrão.  
  
 ALL  
 Limpe o cache de planos de consulta de cada nó de Computação e do nó de Controle.  

> [!NOTE]
> Começando pelo [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)], o `ALTER DATABASE SCOPED CONFIGURATION CLEAR PROCEDURE_CACHE` para limpar o cache (plano) de procedimento para o banco de dados no escopo.

## <a name="remarks"></a>Comentários  
Use DBCC FREEPROCCACHE para limpar o cache do plano cuidadosamente. A limpeza do cache (plano) de procedimento faz com que todos os planos sejam removidos e as execuções de consulta de entrada compilarão um novo plano, em vez de reutilizar um plano anteriormente armazenado em cache. 

Isso pode causar uma queda repentina e temporária no desempenho da consulta conforme o número de novas compilações aumenta. Para cada armazenamento em cache limpo no cache do plano, o log de erros do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] conterá a seguinte mensagem informativa: "O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] encontrou %d ocorrências de liberação de armazenamento em cache '% s' (parte do cache do plano) devido às operações 'DBCC FREEPROCCACHE' ou 'DBCC FREESYSTEMCACHE'". Essa mensagem é registrada a cada cinco minutos, contanto que o cache seja liberado dentro desse intervalo de tempo.

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
Quando a cláusula WITH NO_INFOMSGS não for especificada, DBCC FREEPROCCACHE retornará: "Execução do DBCC concluída. Se o DBCC imprimiu mensagens de erro, entre em contato com o administrador do sistema".
  
## <a name="permissions"></a>Permissões  
Aplica-se a: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] 
- Exige a permissão ALTER SERVER STATE no servidor.  

Aplica-se a: [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]
- Requer associação à função de servidor fixa DB_OWNER.  

## <a name="general-remarks-for-sssdw-and-sspdw"></a>Comentários gerais sobre [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] e [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
Vários comandos DBCC FREEPROCCACHE podem ser executados simultaneamente.
No [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] ou [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], a limpeza do cache de planos pode causar uma queda temporária no desempenho da consulta conforme as consultas de entrada compilam um novo plano, em vez de reutilizar um plano previamente armazenado em cache. 

DBCC FREEPROCCACHE (COMPUTE) apenas faz com que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] recompile consultas quando elas são executadas nos nós de Computação. Ele não faz com que [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] ou [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] recompile o plano de consulta paralela gerado no nó de Controle.
DBCC FREEPROCCACHE pode ser cancelado durante a execução.
  
## <a name="limitations-and-restrictions-for-sssdw-and-sspdw"></a>Limitações e restrições de [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] e [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
DBCC FREEPROCCACHE não pode ser executado em uma transação.
Não há suporte para DBCC FREEPROCCACHE em uma instrução EXPLAIN.
  
## <a name="metadata-for-sssdw-and-sspdw"></a>Metadados de [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] e [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
Uma nova linha é adicionada à exibição do sistema sys.pdw_exec_requests quando DBCC FREEPROCCACHE é executado.

## <a name="examples-ssnoversion"></a>Exemplos: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
### <a name="a-clearing-a-query-plan-from-the-plan-cache"></a>a. Apagando um plano de consulta do cache do plano  
O exemplo a seguir apaga um plano de consulta do cache do plano especificando o identificador do plano de consulta. Para assegurar que a consulta de exemplo esteja no cache do plano, a consulta será executada primeiro. As exibições de gerenciamento dinâmico `sys.dm_exec_cached_plans` e `sys.dm_exec_sql_text` são consultadas para retornar o identificador de plano da consulta. 

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
O exemplo a seguir limpa todos os elementos do cache do plano. A cláusula WITH `NO_INFOMSGS` é especificada para impedir a exibição da mensagem informativa.
  
```sql  
DBCC FREEPROCCACHE WITH NO_INFOMSGS;  
```  
  
### <a name="c-clearing-all-cache-entries-associated-with-a-resource-pool"></a>C. Limpando todas as entradas do cache associadas a um pool de recursos  
O exemplo a seguir limpa todas as entradas do cache associadas a um pool de recursos especificado. A exibição `sys.dm_resource_governor_resource_pools` é consultada primeiro para obter o valor de *pool_name*.
  
```sql  
SELECT * FROM sys.dm_resource_governor_resource_pools;  
GO  
DBCC FREEPROCCACHE ('default');  
GO  
```  
  
## <a name="examples-sssdw-and-sspdw"></a>Exemplos: [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] e [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="d-dbcc-freeproccache-basic-syntax-examples"></a>D. Exemplos de sintaxe básica de DBCC FREEPROCCACHE  
O exemplo a seguir remove todos os caches de planos de consulta existentes dos nós de Computação. Embora o contexto seja definido como UserDbSales, os caches de plano de consulta do nó de Computação de todos os bancos de dados serão removidos. A cláusula WITH NO_INFOMSGS impede a exibição de mensagens informativas nos resultados.  
  
```sql
USE UserDbSales;  
DBCC FREEPROCCACHE (COMPUTE) WITH NO_INFOMSGS;
```  
  
 O exemplo a seguir traz os mesmos resultados do exemplo anterior, exceto que as mensagens informativas serão exibidas nos resultados.  
  
```sql
USE UserDbSales;  
DBCC FREEPROCCACHE (COMPUTE);  
```  
  
Quando mensagens informativas forem solicitadas e a execução for bem-sucedida, os resultados da consulta terão uma linha por nó de Computação.
  
### <a name="e-granting-permission-to-run-dbcc-freeproccache"></a>E. Concedendo permissão para executar DBCC FREEPROCCACHE  
O exemplo a seguir fornece ao logon Davi a permissão para executar DBCC FREEPROCCACHE.  
  
```sql
GRANT ALTER SERVER STATE TO David; 
GO
```  
  
## <a name="see-also"></a>Consulte Também  
[DBCC &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-transact-sql.md)  
[Resource Governor](../../relational-databases/resource-governor/resource-governor.md)  
[ALTER DATABASE SCOPED CONFIGURATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md)
  
  
