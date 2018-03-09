---
title: sys.index_resumable_operations (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/10/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.reviewer: 
ms.service: 
ms.component: system-catalog-views
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.index_resumable_operations_TSQL
- sys.indexes_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.indexes
- sys.index_resumable_operations
ms.assetid: 
caps.latest.revision: 
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 53b6aad214f3d1760bb03ff340e5a5dab30c1067
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/03/2018
---
# <a name="indexresumableoperations-transact-sql"></a>index_resumable_operations (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2017-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-asdb-xxxx-xxx-md.md)]
**sys.index_resumable_operations** é uma exibição de sistema que monitora e verifica o status de execução atual para recompilação de índice reiniciável.  
**Aplica-se a**: SQL Server 2017 e o Azure banco de dados SQL 
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**object_id**|**Int**|ID do objeto ao qual este índice pertence (não permite valor nulo).|  
|**index_id**|**Int**|ID do índice (não permite valor nulo). **index_id** só é exclusivo dentro do objeto.|
|**name**|**sysname**|Nome do índice. **nome** só é exclusivo dentro do objeto.|  
|**sql_text**|**nvarchar(max)**|Texto da instrução DDL T-SQL|
|**last_max_dop**|**smallint**|Última MAX_DOP usada (padrão = 0)|
|**partition_number**|**Int**|Número de partição no índice ou heap de propriedade. Para tabelas não particionadas e índices ou em caso de todas as partições estão sendo recompilar o valor dessa coluna é NULL.|
|**state**|**tinyint**|Estado operacional para retomável índice:<br /><br />0 = em execução<br /><br />1 = pausa|
|**state_desc**|**nvarchar(60)**|Descrição do estado operacional retomáveis índice (em execução ou em pausa)|  
|**start_time**|**datetime**|Hora de início de operação de índice (não permite valor nulo)|
|**last_pause_time**|**datatime**| Última vez em pausa (nulo) da operação de índice. NULL se a operação está em execução e nunca em pausa.|
|**total_execution_time**|**Int**|Tempo total de execução da hora de início em minutos (não permite valor nulas)|
|**percent_complete**|**real**|Preenchimento de andamento de operação de índice no % (não permite valor nulo).|
|**page_count**|**bigint**|Número total de páginas de índice alocada pela operação de compilação de índice para o novo e índices de mapeamento (não permite valor nulas). 

## <a name="permissions"></a>Permissões  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obter mais informações, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
   
## <a name="example"></a>Exemplo  
 Liste todas as operações de recriação de índice retomáveis que estão no estado de pausa. 
  
```  
SELECT * FROM  sys.index_resumable_operations WHERE STATE = 1;  
```  
  
## <a name="see-also"></a>Consulte também 
 [ALTER INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-index-transact-sql.md)    
 [Exibições de catálogo &#40; Transact-SQL &#41; ](catalog-views-transact-sql.md) [Objeto exibições de catálogo &#40; Transact-SQL &#41; ](object-catalog-views-transact-sql.md) [sys. Indexes &#40; Transact-SQL &#41; ](sys-xml-indexes-transact-sql.md) [index_columns &#40; Transact-SQL &#41;](sys-index-columns-transact-sql.md)   
 [sys.xml_indexes &#40;Transact-SQL&#41;](sys-xml-indexes-transact-sql.md)   
 [sys.objects &#40;Transact-SQL&#41;](sys-index-columns-transact-sql.md)   
 [sys.key_constraints &#40;Transact-SQL&#41;](sys-key-constraints-transact-sql.md)   
 [sys.filegroups &#40;Transact-SQL&#41;](sys-filegroups-transact-sql.md)   
 [sys.partition_schemes &#40;Transact-SQL&#41;](sys-partition-schemes-transact-sql.md)   
 [Consultando as perguntas frequentes do catálogo do sistema do SQL Server](querying-the-sql-server-system-catalog-faq.md)   
  
