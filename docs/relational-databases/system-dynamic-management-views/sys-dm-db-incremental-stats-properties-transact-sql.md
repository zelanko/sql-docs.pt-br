---
description: sys.dm_db_incremental_stats_properties (Transact-SQL)
title: sys. dm_db_incremental_stats_properties (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 12/18/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_db_incremental_stats_properties
- sys.dm_db_incremental_stats_properties_TSQL
- dm_db_incremental_stats_properties
- dm_db_incremental_stats_properties_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_db_incremental_stats_properties
ms.assetid: aa0db893-34d1-419c-b008-224852e71307
author: markingmyname
ms.author: maghan
ms.openlocfilehash: caa090c1835c34bd2d1da6d6b3bcb6caa4077217
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89544788"
---
# <a name="sysdm_db_incremental_stats_properties-transact-sql"></a>sys.dm_db_incremental_stats_properties (Transact-SQL)
[!INCLUDE[sqlserver](../../includes/applies-to-version/sqlserver.md)]

  Retorna propriedades de estatísticas incrementais para o objeto de banco de dados especificado (tabela) no banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] atual. O uso de `sys.dm_db_incremental_stats_properties` (que contém um número de partição) é semelhante ao `sys.dm_db_stats_properties` , que é usado para estatísticas não incrementais. 
  
  Essa função foi introduzida no [!INCLUDE[ssSQL14_md](../../includes/sssql14-md.md)] Service Pack 2 e no [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] Service Pack 1.
  
## <a name="syntax"></a>Sintaxe  
  
```  
sys.dm_db_incremental_stats_properties (object_id, stats_id)  
```  
  
## <a name="arguments"></a>Argumentos  
 *object_id*  
 É a ID do objeto no banco de dados atual para o qual as propriedades de uma de suas estatísticas incrementais é solicitada. *object_id* é **int**.  
  
 *stats_id*  
 É a ID de estatísticas do *object_id*especificado. A ID de estatísticas pode ser obtida na exibição de gerenciamento dinâmico [sys.stats](../../relational-databases/system-catalog-views/sys-stats-transact-sql.md) . *stats_id* é **int**.  
  
## <a name="table-returned"></a>Tabela retornada  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|object_id|**int**|ID do objeto (tabela) para o qual as propriedades do objeto de estatísticas serão retornadas.|  
|stats_id|**int**|ID do objeto de estatísticas. É exclusivo na tabela. Para obter mais informações, veja [sys.stats &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-stats-transact-sql.md).|
|partition_number|**int**|Número da partição que contém a parte da tabela.|  
|last_updated|**datetime2**|Data e hora da última atualização do objeto de estatísticas. Para obter mais informações, consulte a seção de [Comentários](#Remarks) nesta página.|  
|rows|**bigint**|O número total de linhas da tabela na última atualização das estatísticas. Se as estatísticas forem filtradas ou corresponderem a um índice filtrado, o número de linhas talvez seja menor do que o número de linhas na tabela.|  
|rows_sampled|**bigint**|O número total de linhas amostradas para cálculos de estatísticas.|  
|etapas|**int**|O número de etapas no histograma. Para obter mais informações, veja [DBCC SHOW_STATISTICS &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-show-statistics-transact-sql.md).|  
|unfiltered_rows|**bigint**|O número total de linhas da tabela antes da aplicação da expressão de filtro (para estatísticas filtradas). Se as estatísticas não forem filtradas, unfiltered_rows será igual ao valor retornado na coluna de linhas.|  
|modification_counter|**bigint**|Número total de modificações da coluna de estatísticas principal (a coluna em que o histograma é criado) desde que as últimas estatísticas de tempo foram atualizadas.<br /><br /> Essa coluna não mantém informações para tabelas com otimização de memória.|  
  
## <a name="remarks"></a><a name="Remarks"></a> Comentários  
 `sys.dm_db_incremental_stats_properties` retorna um conjunto de linhas vazio em qualquer uma das seguintes condições:  
  
-   `stats_id` ou `object_id` é NULO.   
-   O objeto especificado não foi encontrado ou não corresponde a uma tabela com estatísticas incrementais.  
-   A ID de estatísticas especificada não corresponde às estatísticas existentes para a ID de objeto especificada.  
-   O usuário atual não tem permissões para exibir o objeto de estatísticas.
 
 Esse comportamento permite o uso seguro de `sys.dm_db_incremental_stats_properties` quando aplicado a linhas em exibições como `sys.objects` e `sys.stats`. Esse método pode retornar propriedades para as estatísticas que correspondem a cada partição. Para ver as propriedades das estatísticas mescladas combinadas entre todas as partições, use sys.dm_db_stats_properties. 

A data de atualização de estatísticas é armazenada no [objeto de blob de estatísticas](../../relational-databases/statistics/statistics.md#DefinitionQOStatistics), junto com o [histograma](../../relational-databases/statistics/statistics.md#histogram) e o [vetor de densidade](../../relational-databases/statistics/statistics.md#density), não nos metadados. Quando nenhum dado é lido para gerar dados de estatísticas, o blob de estatísticas não é criado, a data não está disponível e a coluna *Last_updated* é nula. Esse é o caso para estatísticas filtradas para as quais o predicado não retorna nenhuma linha ou para novas tabelas vazias.

## <a name="permissions"></a>Permissões  
 Requer que o usuário tenha permissões selecionadas em colunas de estatísticas, que ele possua a tabela ou que seja membro da função de servidor fixa `sysadmin`, da função de banco de dados fixa `db_owner` ou da função de banco de dados fixa `db_ddladmin`.  
  
## <a name="examples"></a>Exemplos  

### <a name="a-simple-example"></a>a. Exemplo simples
O exemplo a seguir retorna as estatísticas para a tabela `PartitionTable` descrita no tópico [Criar tabelas e índices particionados](../../relational-databases/partitions/create-partitioned-tables-and-indexes.md).

```sql
SELECT * FROM sys.dm_db_incremental_stats_properties (object_id('PartitionTable'), 1);
``` 

Para obter sugestões de uso adicionais, consulte  [sys.dm_db_stats_properties](../../relational-databases/system-dynamic-management-views/sys-dm-db-stats-properties-transact-sql.md).
  
## <a name="see-also"></a>Consulte Também  
 [DBCC SHOW_STATISTICS &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-show-statistics-transact-sql.md)   
 [sys.stats &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-stats-transact-sql.md)   
 [Funções e exibições de gerenciamento dinâmico relacionadas ao objeto &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/object-related-dynamic-management-views-and-functions-transact-sql.md)   
 [Exibições e funções de gerenciamento dinâmico &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)  
 [sys. dm_db_stats_properties](../../relational-databases/system-dynamic-management-views/sys-dm-db-stats-properties-transact-sql.md)   
 [sys.dm_db_stats_histogram (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-db-stats-histogram-transact-sql.md) 
