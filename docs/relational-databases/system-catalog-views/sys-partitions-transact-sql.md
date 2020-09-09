---
description: sys.partitions (Transact-SQL)
title: sys. partitions (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- partitions
- partitions_TSQL
- sys.partitions_TSQL
- sys.partitions
dev_langs:
- TSQL
helpviewer_keywords:
- sys.partitions catalog view
ms.assetid: 1c19e1b1-c925-4dad-a652-581692f4ab5e
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 0947a58b607d781b05eb5633b0664d7f0da4d107
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89546719"
---
# <a name="syspartitions-transact-sql"></a>sys.partitions (Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  Contém uma linha para cada partição de todas as tabelas e para a maioria dos tipos de índices no banco de dados. Tipos de índice especiais, como Texto Completo, Espacial e XML, não estão incluídos nessa exibição. Todos os índices e tabelas no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] contêm pelo menos uma partição, estejam ou não explicitamente particionados.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|partition_id|**bigint**|Indica a ID da partição. É exclusivo em um banco de dados.|  
|object_id|**int**|Indica a ID do objeto ao qual pertence o particionamento. Toda tabela ou exibição é composta por pelo menos uma partição.|  
|index_id|**int**|Indica a ID do índice no objeto ao qual pertence o particionamento.<br /><br /> 0 = heap<br />1 = índice clusterizado<br />2 ou maior = índices não clusterizados|  
|partition_number|**int**|É um número de partição com base em um 1 no índice ou heap de propriedade. Para tabelas e índices não particionados, o valor desta coluna é 1.|  
|hobt_id|**bigint**|Indica a ID do heap ou árvore B de dados (HoBT) que contém as linhas desta partição.|  
|rows|**bigint**|Indica o número aproximado de linhas nessa partição.|  
|filestream_filegroup_id|**smallint**|**Aplica-se a**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] e posterior.<br /><br /> Indica a ID do grupo de arquivos FILESTREAM armazenado nesta partição.|  
|data_compression|**tinyint**|Indica o estado da compactação de cada partição:<br /><br /> 0 = NONE <br />1 = ROW <br />2 = PAGE <br />3 = COLUMNSTORE: **aplica-se a**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] e posterior<br />4 = COLUMNSTORE_ARCHIVE: **aplica-se a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] e posterior<br /><br /> **Observação:** Os índices de texto completo serão compactados em qualquer edição do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .|  
|data_compression_desc|**nvarchar(60)**|Indica o estado da compactação de cada partição. Os valores possível para as tabelas rowstore são NONE, ROW e PAGE. Os valores possível para as tabelas columnstor são COLUMNSTORE e COLUMNSTORE_ARCHIVE.|  
  
## <a name="permissions"></a>Permissões  
 Requer associação à função **pública** . Para obter mais informações, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Exibições de catálogo de objeto&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [Exibições de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Consultando as perguntas frequentes do catálogo do sistema do SQL Server](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)  
  
  
