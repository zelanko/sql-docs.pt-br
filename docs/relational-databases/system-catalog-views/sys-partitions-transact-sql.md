---
title: sys. Partitions (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- partitions
- partitions_TSQL
- sys.partitions_TSQL
- sys.partitions
dev_langs: TSQL
helpviewer_keywords: sys.partitions catalog view
ms.assetid: 1c19e1b1-c925-4dad-a652-581692f4ab5e
caps.latest.revision: "60"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 658d0d22bf2dc757854626f792cc49429ab98916
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="syspartitions-transact-sql"></a>sys.partitions (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-asdb-asdw-pdw-md.md)]

  Contém uma linha para cada partição de todas as tabelas e para a maioria dos tipos de índices no banco de dados. Tipos de índice especiais, como Texto Completo, Espacial e XML, não estão incluídos nessa exibição. Todos os índices e tabelas no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] contêm pelo menos uma partição, estejam ou não explicitamente particionados.  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|partition_id|**bigint**|Indica a ID da partição. É exclusivo em um banco de dados.|  
|object_id|**int**|Indica a ID do objeto ao qual pertence o particionamento. Toda tabela ou exibição é composta por pelo menos uma partição.|  
|index_id|**int**|Indica a ID do índice no objeto ao qual pertence o particionamento.<br /><br /> 0 = heap<br />1 = índice clusterizado<br />2 ou maior = índices não clusterizados|  
|partition_number|**int**|É um número de partição com base em um 1 no índice ou heap de propriedade. Para tabelas e índices não particionados, o valor desta coluna é 1.|  
|hobt_id|**bigint**|Indica a ID do heap de dados ou da árvore B que contém as linhas para essa partição.|  
|rows|**bigint**|Indica o número aproximado de linhas nessa partição.|  
|filestream_filegroup_id|**smallint**|**Aplica-se a**: do [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> Indica a ID do grupo de arquivos FILESTREAM armazenado nesta partição.|  
|data_compression|**tinyint**|Indica o estado da compactação de cada partição:<br /><br /> 0 = NONE <br />1 = ROW <br />2 = PAGE <br />3 = COLUMNSTORE: **aplica-se a**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] por meio de[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]<br />4 = COLUMNSTORE_ARCHIVE: **aplica-se a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] por meio de[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]<br /><br /> **Observação:** índices de texto completo serão compactados em qualquer edição do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|data_compression_desc|**nvarchar (60)**|Indica o estado da compactação de cada partição. Os valores possível para as tabelas rowstore são NONE, ROW e PAGE. Os valores possível para as tabelas columnstor são COLUMNSTORE e COLUMNSTORE_ARCHIVE.|  
  
## <a name="permissions"></a>Permissões  
 Requer associação à função **pública** . Para obter mais informações, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Consulte também  
 [Exibições de catálogo de objeto &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [Exibições de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Consultando as perguntas frequentes do catálogo do sistema do SQL Server](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)  
  
  
