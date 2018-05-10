---
title: sys.internal_partitions (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- Azure SQL Database
- SQL Server 2016 Preview
dev_langs:
- TSQL
ms.assetid: 0262df2b-5ba7-4715-b17b-3d9ce470a38e
caps.latest.revision: 13
author: ronortloff
ms.author: rortloff
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 9d0321089336774e4303418b776eec8a1608613b
ms.sourcegitcommit: d2573a8dec2d4102ce8882ee232cdba080d39628
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/07/2018
---
# <a name="sysinternalpartitions-transact-sql"></a>sys.internal_partitions (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Retorna uma linha para cada conjunto de linhas que controla os dados internos para índices columnstore em tabelas baseadas em disco. Esses conjuntos de linhas são internos para índices columnstore e linhas de faixa excluída, mapeamentos de grupo de linhas e delta rowgroups de armazenamento. Controle os dados para cada um para cada partição de tabela; cada tabela tem pelo menos uma partição. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] recria os conjuntos de linhas de cada vez que ela recria o índice columnstore.   
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|partition_id|**bigint**|ID de partição para essa partição. É exclusiva em um banco de dados.|  
|object_id|**Int**|ID de objeto para a tabela que contém a partição.|  
|index_id|**Int**|ID de índice para o índice de columnstore definido na tabela.<br /><br /> 1 = índice columnstore clusterizado<br /><br /> 2 = índice columnstore não clusterizado|  
|partition_number|**Int**|O número de partição.<br /><br /> 1 = a primeira partição de uma tabela particionada, ou a partição única de uma tabela não particionada.<br /><br /> 2 = segunda partição e assim por diante.|  
|internal_object_type|**tinyint**|Objetos de conjunto de linhas que acompanham os dados internos para o índice columnstore.<br /><br /> 2 = COLUMN_STORE_DELETE_BITMAP<br /><br /> 3 = COLUMN_STORE_DELTA_STORE<br /><br /> 4 = COLUMN_STORE_DELETE_BUFFER<br /><br /> 5 = COLUMN_STORE_MAPPING_INDEX|  
|internal_object_type_desc|**nvarchar(60)**|COLUMN_STORE_DELETE_BITMAP – este índice de bitmap controla linhas que são marcadas como excluídas do columnstore. O bitmap é para cada grupo de linhas como partições podem ter linhas em múltiplos rowgroups. As linhas são que ainda estão fisicamente presentes e ocupando espaço no columnstore.<br /><br /> COLUMN_STORE_DELTA_STORE – grupos de repositórios de linhas, chamados de rowgroups, que não foram compactadas em armazenamento Colunar. Cada partição de tabela pode ter zero ou mais rowgroups do deltastore.<br /><br /> COLUMN_STORE_DELETE_BUFFER – para manter as exclusões para índices columnstore não clusterizado atualizável. Quando uma consulta exclui uma linha da tabela rowstore base, o buffer de exclusão rastreia a exclusão do columnstore. Quando o número de linhas excluídas exceder 1048576, eles são mesclados de volta no bitmap de exclusão por thread do motor da tupla do plano de fundo ou um comando de reorganização explícito.  Em qualquer ponto no tempo, a união entre o bitmap de exclusão e o buffer de exclusão representa excluídas todas as linhas.<br /><br /> COLUMN_STORE_MAPPING_INDEX – usado apenas quando o índice columnstore clusterizado tem um índice não clusterizado secundário. Isso mapeia chaves de índice não clusterizado para o rowgroup correto e a ID de linha no columnstore. Ele apenas armazena as chaves para as linhas que se movem para um grupo de linhas diferente; Isso ocorre quando um delta rowgroup é compactado no columnstore, e quando uma operação de mesclagem mescla linhas de duas rowgroups diferentes.|  
|Row_group_id|**Int**|ID do rowgroup deltastore. Cada partição de tabela pode ter zero ou mais rowgroups do deltastore.|  
|hobt_id|**bigint**|ID do objeto de conjunto de linhas interno. Esta é uma chave válida para unir com outros DMVs para obter mais informações sobre as características físicas do conjunto de linhas interno.|  
|rows|**bigint**|Número aproximado de linhas nesta partição.|  
|data_compression|**tinyint**|O estado de compactação para o conjunto de linhas:<br /><br /> 0 = NONE<br /><br /> 1 = ROW<br /><br /> 2 = PAGE|  
|data_compression_desc|**nvarchar(60)**|O estado de compactação para cada partição. Os valores possível para as tabelas rowstore são NONE, ROW e PAGE. Os valores possível para as tabelas columnstor são COLUMNSTORE e COLUMNSTORE_ARCHIVE.|  
  
## <a name="permissions"></a>Permissões  
 Requer associação à função **pública** . Para obter mais informações, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="general-remarks"></a>Comentários gerais  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] cria novos índices de columnstore interno novamente cada vez que cria ou recria um índice columnstore.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-view-all-of-the-internal-rowsets-for-a-table"></a>A. Exibir todos os conjuntos de linhas internos para uma tabela  
 Este exemplo retorna todos os conjuntos de linhas do columnstore interno para uma tabela. Você também pode usar o hobt_id para obter mais informações sobre o conjunto de linhas específica.  
  
```  
SELECT i.object_id, i.index_id, i.name, p.hobt_id, p.internal_object_type_id, p.internal_object_type_desc  
FROM sys.internal_partitions AS p  
JOIN sys.indexes AS i  
on i.object_id = p.object_id  
WHERE p.object_id = OBJECT_ID ( '<table name' ) ;  
```  
  
## <a name="see-also"></a>Consulte também  
 [Exibições de catálogo de objeto&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [Exibições de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Consultando as perguntas frequentes do catálogo do sistema do SQL Server](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)  
  
  
