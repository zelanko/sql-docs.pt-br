---
title: sys. data_spaces (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- data_spaces
- sys.data_spaces_TSQL
- sys.data_spaces
- data_spaces_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.data_spaces catalog view
ms.assetid: f39d55fe-2c0f-472d-a77f-cebc6fea95b5
author: CarlRabeler
ms.author: carlrab
monikerRange: '>=aps-pdw-2016||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: df3dd7f9680860455ec6291e8ba4a945f4db2043
ms.sourcegitcommit: df1f0f2dfb9452f16471e740273cd1478ff3100c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/29/2020
ms.locfileid: "87394051"
---
# <a name="sysdata_spaces-transact-sql"></a>sys.data_spaces (Transact-SQL)
[!INCLUDE [sql-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdbmi-asa-pdw.md)]

  Contém uma linha para cada espaço de dados. Esse pode ser um grupo de arquivos, esquema de partição ou grupo de arquivos de dados FILESTREAM.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|name|**sysname**|Nome de espaço de dados, exclusivo no banco de dados.|  
|data_space_id|**int**|Número de ID do espaço de dados, exclusivo no banco de dados.|  
|type|**char(2)**|Tipo de espaço de dados:<br /><br /> FG = Grupo de arquivos<br /><br /> FD = Grupo de arquivos de dados FILESTREAM<br /><br /> FX = Grupo de arquivos de tabelas com otimização de memória<br /><br /> **Aplica-se a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] e posterior.<br /><br /> PS = Esquema de partição|  
|type_desc|**nvarchar(60)**|Descrição do tipo de espaço de dados:<br /><br /> FILESTREAM_DATA_FILEGROUP<br /><br /> MEMORY_OPTIMIZED_DATA_FILEGROUP<br /><br /> **Aplica-se a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] e posterior.<br /><br /> PARTITION_SCHEME<br /><br /> ROWS_FILEGROUP|  
|is_default|**bit**|1 = Este é o espaço de dados padrão. O espaço de dados padrão é usado quando um grupo de arquivos ou esquema de partição não é especificado em uma instrução CREATE TABLE ou CREATE INDEX.<br /><br /> 0 = Este não é o espaço de dados padrão.|  
|is_system|**bit**|**Aplica-se a**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] e posterior.<br /><br /> 1 = O espaço de dados é usado para fragmentos de índice de texto completo.<br /><br /> 0 = O espaço de dados não é usado para fragmentos de índice de texto completo.|  
  
## <a name="permissions"></a>Permissões  
 Requer associação à função public. Para obter mais informações, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Espaços de dados &#40;&#41;Transact-SQL](../../relational-databases/system-catalog-views/data-spaces-transact-sql.md)   
 [Exibições de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [sys.databases &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)   
 [sys. destination_data_spaces &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-destination-data-spaces-transact-sql.md)   
 [sys.filegroups &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-filegroups-transact-sql.md)   
 [sys. partition_schemes &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-partition-schemes-transact-sql.md)   
 [Consultando as perguntas frequentes sobre o catálogo do sistema SQL Server](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)   
 [OLTP in-memory &#40;Otimização na memória&#41;](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  
  
