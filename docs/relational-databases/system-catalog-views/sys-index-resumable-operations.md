---
title: index_resumable_operations (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/10/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.component: system-catalog-views
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.index_resumable_operations_TSQL
- sys.indexes_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.indexes
- sys.index_resumable_operations
ms.assetid: ''
caps.latest.revision: 1
author: CarlRabeler
ms.author: carlrab
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2017||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 0d0da28f06dc079d468b2b8862855e1e2f957540
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2018
ms.locfileid: "43076943"
---
# <a name="indexresumableoperations-transact-sql"></a>index_resumable_operations (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2017-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-asdb-xxxx-xxx-md.md)]
**index_resumable_operations** é uma exibição de sistema que monitora e verifica o status de execução atual para recompilação de índice retomável.  
**Aplica-se a**: SQL Server 2017 e o Azure SQL Database 
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|ID do objeto ao qual este índice pertence (não permite valor nulo).|  
|**index_id**|**int**|ID do índice (não permite valor nulo). **index_id** é exclusivo somente dentro do objeto.|
|**name**|**sysname**|Nome do índice. **nome** só é exclusivo dentro do objeto.|  
|**sql_text**|**nvarchar(max)**|Texto da instrução DDL T-SQL|
|**last_max_dop**|**smallint**|Último MAX_DOP usada (padrão = 0)|
|**partition_number**|**int**|Número de partição no índice ou heap de propriedade. Para índices e tabelas não particionadas ou caso todas as partições estão sendo recompilação o valor desta coluna é NULL.|
|**state**|**tinyint**|Estado operacional para o índice retomável:<br /><br />0 = em execução<br /><br />1 = pausa|
|**state_desc**|**nvarchar(60)**|Descrição do estado operacional (em execução ou em pausa) de índice retomável|  
|**start_time**|**datetime**|Hora de início de operação de índice (não permite valor nulo)|
|**last_pause_time**|**datatime**| Hora da última pausa (anulável) da operação de índice. NULL se a operação está em execução e nunca em pausa.|
|**total_execution_time**|**int**|Tempo de execução total da hora de início em minutos (não permite valor nulas)|
|**percent_complete**|**real**|Conclusão de progresso da operação de índice em % (não permite valor nulo).|
|**page_count**|**bigint**|Número total de páginas de índice alocadas pela operação de compilação de índice para o novo e índices de mapeamento (não permite valor nulas). 

## <a name="permissions"></a>Permissões  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obter mais informações, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
   
## <a name="example"></a>Exemplo  
 Liste todas as operações de recompilação de índice retomável que estão no estado de pausa. 
  
```  
SELECT * FROM  sys.index_resumable_operations WHERE STATE = 1;  
```  
  
## <a name="see-also"></a>Consulte também 
 [ALTER INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-index-transact-sql.md)    
 [Exibições do catálogo &#40;Transact-SQL&#41; ](catalog-views-transact-sql.md) [exibições do catálogo de objeto &#40;Transact-SQL&#41; ](object-catalog-views-transact-sql.md) [sys. Indexes &#40;Transact-SQL&#41; ](sys-xml-indexes-transact-sql.md) [sys. index_columns &#40;Transact-SQL&#41;](sys-index-columns-transact-sql.md)   
 [sys.xml_indexes &#40;Transact-SQL&#41;](sys-xml-indexes-transact-sql.md)   
 [sys.objects &#40;Transact-SQL&#41;](sys-index-columns-transact-sql.md)   
 [sys.key_constraints &#40;Transact-SQL&#41;](sys-key-constraints-transact-sql.md)   
 [sys.filegroups &#40;Transact-SQL&#41;](sys-filegroups-transact-sql.md)   
 [sys.partition_schemes &#40;Transact-SQL&#41;](sys-partition-schemes-transact-sql.md)   
 [Consultando as perguntas frequentes do catálogo do sistema do SQL Server](querying-the-sql-server-system-catalog-faq.md)   
  
