---
title: sys. internal_partitions (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/26/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 0262df2b-5ba7-4715-b17b-3d9ce470a38e
author: ronortloff
ms.author: rortloff
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: f0d1e6e4fa9c88fc67b15a076a6c96a742fd7fdc
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "72304814"
---
# <a name="sysinternal_partitions-transact-sql"></a>sys. internal_partitions (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Retorna uma linha para cada conjunto de linhas que rastreia dados internos para índices columnstore em tabelas baseadas em disco. Esses conjuntos de linhas são internos a índices columnstore e rastreiam linhas excluídas, mapeamentos de rowgroup e grupos de itens de loja Delta. Eles controlam os dados para cada partição de tabela; cada tabela tem pelo menos uma partição. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]recria os conjuntos de linhas a cada vez que recria o índice columnstore.   
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|partition_id|**bigint**|ID da partição para esta partição. É exclusiva em um banco de dados.|  
|object_id|**int**|ID de objeto da tabela que contém a partição.|  
|index_id|**int**|ID de índice para o índice columnstore definido na tabela.<br /><br /> 1 = índice columnstore clusterizado<br /><br /> 2 = índice columnstore não clusterizado|  
|partition_number|**int**|O número da partição.<br /><br /> 1 = primeira partição de uma tabela particionada ou a partição única de uma tabela não particionada.<br /><br /> 2 = segunda partição e assim por diante.|  
|internal_object_type|**tinyint**|Objetos de conjunto de linhas que rastreiam dados internos para o índice columnstore.<br /><br /> 2 = COLUMN_STORE_DELETE_BITMAP<br /><br /> 3 = COLUMN_STORE_DELTA_STORE<br /><br /> 4 = COLUMN_STORE_DELETE_BUFFER<br /><br /> 5 = COLUMN_STORE_MAPPING_INDEX|  
|internal_object_type_desc|**nvarchar(60)**|COLUMN_STORE_DELETE_BITMAP-esse índice de bitmap rastreia as linhas marcadas como excluídas do columnstore. O bitmap é para cada rowgroup, já que as partições podem ter linhas em várias RowGroups. As linhas ainda estão fisicamente presentes e ocupando espaço no columnstore.<br /><br /> O COLUMN_STORE_DELTA_STORE-armazena grupos de linhas, chamados de RowGroups, que não foram compactados no armazenamento de colunas. Cada partição de tabela pode ter zero ou mais grupos de deltastore.<br /><br /> COLUMN_STORE_DELETE_BUFFER-para manter as exclusões para índices columnstore não clusterizados atualizáveis. Quando uma consulta exclui uma linha da tabela de armazenamento de linhas subjacente, o buffer de exclusão rastreia a exclusão do columnstore. Quando o número de linhas excluídas excede 1048576, elas são mescladas de volta ao thread de exclusão de bitmap por segundo plano do motor de tupla ou por um comando de reorganização explícito.  Em qualquer momento determinado, a União do bitmap de exclusão e do buffer de exclusão representa todas as linhas excluídas.<br /><br /> COLUMN_STORE_MAPPING_INDEX-usado somente quando o índice columnstore clusterizado tem um índice não clusterizado secundário. Isso mapeia chaves de índice não clusterizado para o rowgroup e a ID de linha corretos no columnstore. Ele armazena apenas as chaves para linhas que se movem para um rowgroup diferente; Isso ocorre quando um rowgroup Delta é compactado no columnstore e quando uma operação de mesclagem mescla linhas de dois RowGroups diferentes.|  
|Row_group_id|**int**|ID para o rowgroup deltastore. Cada partição de tabela pode ter zero ou mais grupos de deltastore.|  
|hobt_id|**bigint**|ID do objeto de conjunto de linhas interno (HoBT). Essa é uma boa chave para ingressar com outras DMVs para obter mais informações sobre as características físicas do conjunto de linhas interno.|  
|rows|**bigint**|Número aproximado de linhas nesta partição.|  
|data_compression|**tinyint**|O estado de compactação para o conjunto de linhas:<br /><br /> 0 = NONE<br /><br /> 1 = ROW<br /><br /> 2 = PAGE|  
|data_compression_desc|**nvarchar(60)**|O estado de compactação para cada partição. Os valores possível para as tabelas rowstore são NONE, ROW e PAGE. Os valores possível para as tabelas columnstor são COLUMNSTORE e COLUMNSTORE_ARCHIVE.|  
|optimize_for_sequential_key|**bit**|1 = a partição tem a otimização de inserção da última página habilitada.<br><br>0 = valor padrão. A otimização de inserção da última página foi desabilitada na partição.|
  
## <a name="permissions"></a>Permissões  
 Exige a associação à função `public`.  Para obter mais informações, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="general-remarks"></a>Comentários gerais  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]recria novos índices internos columnstore cada vez que cria ou recria um índice columnstore.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-view-all-of-the-internal-rowsets-for-a-table"></a>a. Exibir todos os conjuntos de linhas internos de uma tabela  
 Este exemplo retorna todos os conjuntos de linhas columnstore internos para uma tabela. Você também pode usar o hobt_id para encontrar mais informações sobre o conjunto de linhas específico.  
  
```sql  
SELECT i.object_id, i.index_id, i.name, p.hobt_id, p.internal_object_type_id, p.internal_object_type_desc  
FROM sys.internal_partitions AS p  
JOIN sys.indexes AS i  
on i.object_id = p.object_id  
WHERE p.object_id = OBJECT_ID ( '<table name' ) ;  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Exibições de catálogo de objetos &#40;&#41;Transact-SQL](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [Exibições de catálogo &#40;&#41;Transact-SQL](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Consultando as perguntas frequentes do catálogo do sistema do SQL Server](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)  
  
  
