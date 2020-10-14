---
description: sys.pdw_index_mappings (Transact-SQL)
title: sys.pdw_index_mappings (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: d62b0e25-3226-4f87-a10a-b3a0d9555e19
author: ronortloff
ms.author: rortloff
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 05aec55dda150df8e686d5f2f50deca9e5b722ff
ms.sourcegitcommit: 22dacedeb6e8721e7cdb6279a946d4002cfb5da3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/14/2020
ms.locfileid: "92036993"
---
# <a name="syspdw_index_mappings-transact-sql"></a>sys.pdw_index_mappings (Transact-SQL)
[!INCLUDE[applies-to-version/asa-pdw](../../includes/applies-to-version/asa-pdw.md)]

  Mapeia os índices lógicos para o nome físico usado em nós de computação, conforme refletido por uma combinação exclusiva de **object_id** da tabela que contém o índice e o **index_id** de um índice específico dentro dessa tabela.  
  
|Nome da coluna|Tipo de Dados|DESCRIÇÃO|Intervalo|  
|-----------------|---------------|-----------------|-----------|  
|object_id|**int**|A ID de objeto para a tabela lógica na qual esse índice existe. Consulte [Sys. objects &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md).<br /><br /> **physical_name** e **object_id** formate a chave para essa exibição.||  
|index_id|**nvarchar(32)**|A ID do índice. Consulte [Sys. indexes &#40;&#41;Transact-SQL ](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md).||  
|physical_name|**nvarchar (36)**|O nome do índice nos bancos de dados nos nós de computação.<br /><br /> **physical_name** e **object_id** formate a chave para essa exibição.||  
  
## <a name="see-also"></a>Consulte Também  
 [Exibições de Catálogo do Azure Synapse Analytics e do Parallel Data Warehouse](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)   
 [&#41;&#40;Transact-SQL de sys.pdw_table_mappings ](../../relational-databases/system-catalog-views/sys-pdw-table-mappings-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sys.pdw_permanent_table_mappings ](../../relational-databases/system-catalog-views/sys-pdw-permanent-table-mappings-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sys.pdw_database_mappings ](../../relational-databases/system-catalog-views/sys-pdw-database-mappings-transact-sql.md)  
  
  
