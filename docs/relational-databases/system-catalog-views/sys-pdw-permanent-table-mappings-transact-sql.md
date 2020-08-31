---
title: sys. pdw_permanent_table_mappings (Transact-SQL)
ms.custom: ''
ms.date: 07/24/2020
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
author: mstehrani
ms.author: emtehran
monikerRange: = azure-sqldw-latest || = sqlallproducts-allversions
ms.openlocfilehash: c48cb981549d47b24152772cef9278de6557612f
ms.sourcegitcommit: 883435b4c7366f06ac03579752093737b098feab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/28/2020
ms.locfileid: "89062255"
---
# <a name="syspdw_permanent_table_mappings-transact-sql"></a>sys. pdw_permanent_table_mappings (Transact-SQL)
[!INCLUDE [applies-to-version/asa](../../includes/applies-to-version/asa.md)]

  Vincula tabelas de usuário permanentes a nomes de objetos internos por **object_id**.  
  
> [!NOTE]
> **Sys. pdw_permanent_table_mappings** mantém mapeamentos para tabelas permanentes e não inclui mapeamentos de tabela temporários ou externos.

|Nome da coluna|Tipo de Dados|Descrição|  
|-----------------|---------------|-----------------|  
|physical_name|**nvarchar (36)**|O nome físico da tabela.<br /><br /> **physical_name** e **object_id** formate a chave para essa exibição.||  
|object_id|**int**|A ID de objeto da tabela. Consulte [Sys. objects &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md).<br /><br /> **physical_name** e **object_id** formate a chave para essa exibição.||  
  
## <a name="see-also"></a>Consulte Também  
 [Exibições de Catálogo do SQL Data Warehouse e Parallel Data Warehouse](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)   
 [sys. pdw_index_mappings &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-pdw-index-mappings-transact-sql.md)  
  
  
