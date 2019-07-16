---
title: DM db_stats_properties (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 12/18/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_db_stats_properties_TSQL
- sys.dm_db_stats_properties
- dm_db_stats_properties_TSQL
- dm_db_stats_properties
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_db_stats_properties
ms.assetid: 8a54889d-e263-4881-9fcb-b1db410a9453
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 274e801bfb8e627564f5586574c16ecd916e9859
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67910709"
---
# <a name="sysdmdbstatsproperties-transact-sql"></a>sys.dm_db_stats_properties (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Retorna propriedades de estatísticas para o objeto de banco de dados especificado (tabela ou exibição indexada) no banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] atual. Para tabelas particionadas, consulte o semelhante [DM db_incremental_stats_properties](../../relational-databases/system-dynamic-management-views/sys-dm-db-incremental-stats-properties-transact-sql.md). 
 
## <a name="syntax"></a>Sintaxe  
  
```  
sys.dm_db_stats_properties (object_id, stats_id)  
```  
  
## <a name="arguments"></a>Argumentos  
 *object_id*  
 É a ID do objeto no banco de dados atual para o qual as propriedades de uma de suas estatísticas é solicitada. *object_id* é **int**.  
  
 *stats_id*  
 É a ID de estatísticas do *object_id*especificado. A ID de estatísticas pode ser obtida na exibição de gerenciamento dinâmico [sys.stats](../../relational-databases/system-catalog-views/sys-stats-transact-sql.md) . *stats_id* é **int**.  
  
## <a name="table-returned"></a>Tabela retornada  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|object_id|**int**|ID do objeto (tabela ou exibição indexada) para o qual as propriedades do objeto de estatísticas serão retornadas.|  
|stats_id|**int**|ID do objeto de estatísticas. É exclusiva na tabela ou exibição indexada. Para obter mais informações, veja [sys.stats &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-stats-transact-sql.md).|  
|last_updated|**datetime2**|Data e hora da última atualização do objeto de estatísticas. Para obter mais informações, consulte a seção de [Comentários](#Remarks) nesta página.|  
|rows|**bigint**|O número total de linhas da tabela ou exibição indexada na última atualização das estatísticas. Se as estatísticas forem filtradas ou corresponderem a um índice filtrado, o número de linhas talvez seja menor do que o número de linhas na tabela.|  
|rows_sampled|**bigint**|O número total de linhas amostradas para cálculos de estatísticas.|  
|etapas|**int**|O número de etapas no histograma. Para obter mais informações, veja [DBCC SHOW_STATISTICS &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-show-statistics-transact-sql.md).|  
|unfiltered_rows|**bigint**|O número total de linhas da tabela antes da aplicação da expressão de filtro (para estatísticas filtradas). Se as estatísticas não forem filtradas, unfiltered_rows será igual ao valor retornado na coluna de linhas.|  
|modification_counter|**bigint**|Número total de modificações da coluna de estatísticas principal (a coluna em que o histograma é criado) desde que as últimas estatísticas de tempo foram atualizadas.<br /><br /> Tabelas com otimização de memória: iniciando [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] e, em [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] esta coluna contém: número total de modificações para a tabela, pois as estatísticas da última vez foram atualizadas ou o banco de dados foi reiniciado.|  
|persisted_sample_percent|**float**|Percentual de amostra persistente usado para as atualizações de estatísticas que não especifica explicitamente um percentual de amostragem. Se o valor for zero, nenhum percentual de amostra persistente será definido para essa estatística.<br /><br /> **Aplica-se a:** [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP1 CU4|  
  
## <a name="Remarks"></a> Comentários  
 **DM db_stats_properties** retorna um conjunto de linhas vazio em qualquer uma das seguintes condições:  
  
-   **object_id** ou **stats_id** é NULL.    
-   O objeto especificado não foi encontrado ou não corresponde a uma tabela ou exibição indexada.    
-   A ID de estatísticas especificada não corresponde às estatísticas existentes para a ID de objeto especificada.    
-   O usuário atual não tem permissões para exibir o objeto de estatísticas.  
  
 Esse comportamento permite o uso seguro de **DM db_stats_properties** quando aplicado a linhas em exibições, como **sys. Objects** e **sys. Stats**.  
 
A data de atualização de estatísticas é armazenada no [objeto de blob de estatísticas](../../relational-databases/statistics/statistics.md#DefinitionQOStatistics), junto com o [histograma](../../relational-databases/statistics/statistics.md#histogram) e o [vetor de densidade](../../relational-databases/statistics/statistics.md#density), não nos metadados. Quando nenhum dado é lido para gerar dados de estatísticas, o blob de estatísticas não é criado, a data não estiver disponível e o *last_updated* coluna será NULL. Esse é o caso para estatísticas filtradas para as quais o predicado não retorna nenhuma linha ou para novas tabelas vazias.
  
## <a name="permissions"></a>Permissões  
 Requer que o usuário tenha permissões selecionadas em colunas de estatísticas, que ele possua a tabela ou que seja membro da função de servidor fixa `sysadmin`, da função de banco de dados fixa `db_owner` ou da função de banco de dados fixa `db_ddladmin`.  
  
## <a name="examples"></a>Exemplos  

### <a name="a-simple-example"></a>A. Exemplo simples
O exemplo a seguir retorna as estatísticas para o `Person.Person` tabela no banco de dados AdventureWorks.

```sql
SELECT * FROM sys.dm_db_stats_properties (object_id('Person.Person'), 1);
``` 
  
### <a name="b-returning-all-statistics-properties-for-a-table"></a>B. Retornando todas as propriedades de estatísticas para uma tabela  
 O exemplo a seguir retorna propriedades de todas as estatísticas que existem para a tabela TEST.  
  
```sql  
SELECT sp.stats_id, name, filter_definition, last_updated, rows, rows_sampled, steps, unfiltered_rows, modification_counter   
FROM sys.stats AS stat   
CROSS APPLY sys.dm_db_stats_properties(stat.object_id, stat.stats_id) AS sp  
WHERE stat.object_id = object_id('TEST');  
```  
  
### <a name="c-returning-statistics-properties-for-frequently-modified-objects"></a>C. Retornando propriedades de estatísticas para objetos modificados com frequência  
 O exemplo a seguir retorna todas as tabelas, exibições indexadas e estatísticas do banco de dados atual para o qual a coluna principal foi modificada mais de 1000 vezes desde a última atualização de estatísticas.  
  
```sql  
SELECT obj.name, obj.object_id, stat.name, stat.stats_id, last_updated, modification_counter  
FROM sys.objects AS obj   
INNER JOIN sys.stats AS stat ON stat.object_id = obj.object_id  
CROSS APPLY sys.dm_db_stats_properties(stat.object_id, stat.stats_id) AS sp  
WHERE modification_counter > 1000;  
```  
  
## <a name="see-also"></a>Consulte também  
 [DBCC SHOW_STATISTICS &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-show-statistics-transact-sql.md)   
 [sys.stats &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-stats-transact-sql.md)   
 [Funções e exibições de gerenciamento dinâmico relacionadas ao objeto &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/object-related-dynamic-management-views-and-functions-transact-sql.md)   
 [Exibições e funções de gerenciamento dinâmico &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)  
 [sys.dm_db_incremental_stats_properties (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-db-incremental-stats-properties-transact-sql.md)  
 [sys.dm_db_stats_histogram (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-db-stats-histogram-transact-sql.md) 
  

