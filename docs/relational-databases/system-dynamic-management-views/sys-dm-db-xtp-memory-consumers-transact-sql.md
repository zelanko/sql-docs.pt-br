---
title: sys.dm_db_xtp_memory_consumers (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.dm_db_xtp_memory_consumers
- dm_db_xtp_memory_consumers
- dm_db_xtp_memory_consumers_TSQL
- sys.dm_db_xtp_memory_consumers_stats_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_db_xtp_memory_consumers dynamic management view
ms.assetid: f7ab2eaf-e627-464d-91fe-0e170b3f37bc
caps.latest.revision: 24
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
monikerRange: = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: d2cb462162ae8a34947631b52fc6c2b10222f640
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="sysdmdbxtpmemoryconsumers-transact-sql"></a>sys.dm_db_xtp_memory_consumers (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2014-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2014-asdb-xxxx-xxx-md.md)]

  Relata os consumidores de memória no nível de banco de dados no mecanismo de banco de dados [!INCLUDE[hek_2](../../includes/hek-2-md.md)]. A exibição retorna uma linha para cada consumidor de memória que o mecanismo de banco de dados usa. Use essa DMV para ver como a memória é distribuída entre diferentes objetos internos.  
  
 Para obter mais informações, veja [OLTP in-memory &#40;Otimização na memória&#41;](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md).  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|memory_consumer_id|**bigint**|ID (interna) do consumidor de memória.|  
|memory_consumer_type|**Int**|O tipo de consumidor de memória:<br /><br /> 0=Agregação. (Agrega o uso de memória de dois ou mais consumidores. Ele não deve ser exibido.)<br /><br /> 2=VARHEAP (Rastreia o consumo de memória para um heap de comprimento variável.)<br /><br /> 3=HASH (Rastreia o consumo da memória para um índice.)<br /><br /> 5=Pool da página do BD (Rastreia o consumo de memória de um pool de página de banco de dados usado em operações de tempo de execução. Por exemplo, as variáveis de tabela e algumas verificações serializáveis. Há apenas um consumidor de memória deste tipo por banco de dados.)|  
|memory_consumer_type_desc|**nvarchar(64)**|Tipo de consumidor de memória: VARHEAP, HASH ou PGPOOL.<br /><br /> 0 – (Não deve ser exibido.)<br /><br /> 2 - VARHEAP<br /><br /> 3 - HASH<br /><br /> 5 - PGPOOL|  
|memory_consumer_desc|**nvarchar(64)**|Descrição da instância do consumidor de memória:<br /><br /> VARHEAP: <br />Heap do banco de dados. Usado para alocar dados do usuário para um banco de dados (linhas).<br />Heap do sistema de banco de dados. Usado para alocar dados do banco de dados que serão incluídos nos despejos de memória e não incluem dados de usuário.<br />Heap do índice de intervalo. Heap privado usado pelo índice de intervalo para alocar páginas do BW.<br /><br /> HASH: Nenhuma descrição desde que o object_id indica a tabela e o index_id, o índice de hash.<br /><br /> PGPOOL: Para o banco de dados há pool da página somente um pool de página do banco de dados de 64K.|  
|object_id|**bigint**|A ID de objeto à qual a memória alocada está atribuída. Um valor negativo de objetos do sistema.|  
|xtp_object_id|**bigint**|A ID de objeto para a tabela com otimização de memória.|  
|index_id|**Int**|A ID de índice do consumidor (se houver). NULL para tabelas base.|  
|allocated_bytes|**bigint**|Número de bytes reservados para o consumidor.|  
|used_bytes|**bigint**|Bytes usados por este consumidor. Aplica-se somente a varheap.|  
|allocation_count|**Int**|Número de alocações.|  
|partition_count|**Int**|Somente para uso interno.|  
|sizeclass_count|**Int**|Somente para uso interno.|  
|min_sizeclass|**Int**|Somente para uso interno.|  
|max_sizeclass|**Int**|Somente para uso interno.|  
|memory_consumer_address|**varbinary**|Endereço interno do consumidor. Somente para uso interno.|  
|xtp_object_id|**bigint**|A ID de objeto OLTP na memória que corresponde à tabela com otimização de memória.|  
  
## <a name="remarks"></a>Remarks  
 Na saída, os alocadores nos níveis de banco de dados fazem referência a tabelas de usuário, índices e tabelas do sistema. VARHEAP com object_id = NULL refere-se à memória alocada para tabelas com colunas de tamanho variável.  
  
## <a name="permissions"></a>Permissões  
 Todas as linhas são retornadas se você tiver a permissão VIEW DATABASE STATE no banco de dados atual. Caso contrário, um conjunto de linhas vazio será retornado.  
  
 Se você não tiver permissão VIEW DATABASE, todas as colunas serão retornadas para as linhas nas tabelas nas quais você tiver permissão SELECT.  
  
 As tabelas do sistema são retornadas apenas para usuários com permissão VIEW DATABASE STATE.  
  
## <a name="general-remarks"></a>Comentários gerais  
 Quando uma tabela com otimização de memória tem um índice columnstore, o sistema usa algumas tabelas internas que consomem memória, para acompanhar os dados para o índice columnstore. Para obter detalhes sobre essas tabelas internas e consultas de exemplo mostrando o consumo de memória, consulte [memory_optimized_tables_internal_attributes (Transact-SQL)](../../relational-databases/system-catalog-views/sys-memory-optimized-tables-internal-attributes-transact-sql.md).
 
  
## <a name="examples"></a>Exemplos  
  
```  
-- memory consumers (database level)  
SELECT OBJECT_NAME(object_id), *   
FROM sys.dm_db_xtp_memory_consumers;  
```  
  
## <a name="user-scenario"></a>Cenário de uso  
  
```  
-- memory consumers (database level)  
  
select  convert(char(10), object_name(object_id)) as Name,   
convert(char(10),memory_consumer_type_desc ) as memory_consumer_type_desc, object_id,index_id, allocated_bytes,  used_bytes   
from sys.dm_db_xtp_memory_consumers  
```  
  
 Veja a saída com um subconjunto de colunas. Os alocadores nos níveis de banco de dados fazem referência a tabelas de usuário, índices e tabelas do sistema. O VARHEAP com object_id = NULL (a última linha) refere-se à memória alocada a linhas de dados das tabelas (no exemplo a seguir, é t1). Os bytes alocados, quando convertidos para MB, são 1340MB.  
  
```  
Name       memory_consumer_type_desc object_id   index_id    allocated_bytes      used_bytes  
---------- ------------------------- ----------- ----------- -------------------- --------------------  
t3         HASH                      629577281   2           8388608              8388608  
t2         HASH                      597577167   2           8388608              8388608  
t1         HASH                      565577053   2           1048576              1048576  
NULL       HASH                      -6          1           2048                 2048  
NULL       VARHEAP                   -6          NULL        0                    0  
NULL       HASH                      -5          3           8192                 8192  
NULL       HASH                      -5          2           8192                 8192  
NULL       HASH                      -5          1           8192                 8192  
NULL       HASH                      -4          1           2048                 2048  
NULL       VARHEAP                   -4          NULL        0                    0  
NULL       HASH                      -3          1           2048                 2048  
NULL       HASH                      -2          2           8192                 8192  
NULL       HASH                      -2          1           8192                 8192  
NULL       VARHEAP                   -2          NULL        196608               26496  
NULL       HASH                      0           1           2048                 2048  
NULL       PGPOOL                    0           NULL        0                    0  
NULL       VARHEAP                   NULL        NULL        1405943808           1231220560  
  
(17 row(s) affected)  
```  
  
 A memória total alocada e usada dessa DMV é o mesma que o nível de objeto em [sys.DM db_xtp_table_memory_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-xtp-table-memory-stats-transact-sql.md).  
  
```  
select  sum(allocated_bytes)/(1024*1024) as total_allocated_MB,   
        sum(used_bytes)/(1024*1024) as total_used_MB  
from sys.dm_db_xtp_memory_consumers  
  
total_allocated_MB   total_used_MB  
-------------------- --------------------  
1358                 1191  
```  
  
## <a name="see-also"></a>Consulte também  
 [Exibições de gerenciamento dinâmico de tabela de otimização de memória &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/memory-optimized-table-dynamic-management-views-transact-sql.md)  
  
  
