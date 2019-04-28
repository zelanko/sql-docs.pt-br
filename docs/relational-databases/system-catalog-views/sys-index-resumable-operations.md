---
title: sys.index_resumable_operations (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/14/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
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
author: CarlRabeler
ms.author: carlrab
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2017||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 780cffa17f6ee1af70d942545632c98c9d6dc1e7
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63004375"
---
# <a name="indexresumableoperations-transact-sql"></a>index_resumable_operations (Transact-SQL)

[!INCLUDE[tsql-appliesto-ss2017-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-asdb-xxxx-xxx-md.md)]
**index_resumable_operations** é uma exibição de sistema que monitora e verifica o status de execução atual para recompilação de índice retomável.  
**Aplica-se ao**: SQL Server 2017 e o Azure SQL Database
  
|Nome da coluna|Tipo de dados|Descrição|  
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

```sql
SELECT * FROM  sys.index_resumable_operations WHERE STATE = 1;  
```

## <a name="see-also"></a>Consulte também

- [ALTER INDEX](../../t-sql/statements/alter-index-transact-sql.md)
- [CREATE INDEX](../../t-sql/statements/create-index-transact-sql.md)
- [Exibições do catálogo](catalog-views-transact-sql.md)
- [Exibições de catálogo](object-catalog-views-transact-sql.md)
- [sys.indexes](sys-xml-indexes-transact-sql.md)
- [sys.index_columns](sys-index-columns-transact-sql.md)
- [sys.xml_indexes](sys-xml-indexes-transact-sql.md)
- [sys.objects](sys-index-columns-transact-sql.md)
- [sys.key_constraints](sys-key-constraints-transact-sql.md)
- [sys.filegroups](sys-filegroups-transact-sql.md)
- [sys.partition_schemes](sys-partition-schemes-transact-sql.md)
- [Consultando as perguntas frequentes do catálogo do sistema do SQL Server](querying-the-sql-server-system-catalog-faq.md)
