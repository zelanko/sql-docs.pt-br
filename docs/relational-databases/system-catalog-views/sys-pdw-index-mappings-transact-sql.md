---
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
ms.openlocfilehash: 298a24276ff9c1d73a7b15ddc977d0623af70af3
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68127480"
---
# <a name="syspdwindexmappings-transact-sql"></a>sys.pdw_index_mappings (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  Mapeia a lógica de índices para o nome físico usado em nós de computação, como refletido por uma combinação exclusiva de **object_id** da tabela que contém o índice e o **index_id** de um determinado índice em que tabela.  
  
|Nome da coluna|Tipo de dados|Descrição|Intervalo|  
|-----------------|---------------|-----------------|-----------|  
|object_id|**int**|A ID de objeto para a tabela lógica na qual existe este índice. Ver [sys. Objects &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md).<br /><br /> **physical_name** e **object_id** formam a chave para esta exibição.||  
|index_id|**nvarchar(32)**|A ID do índice. Ver [sys. Indexes &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md).||  
|physical_name|**nvarchar(36)**|O nome do índice nos bancos de dados em nós de computação.<br /><br /> **physical_name** e **object_id** formam a chave para esta exibição.||  
  
## <a name="see-also"></a>Consulte também  
 [Exibições de Catálogo do SQL Data Warehouse e Parallel Data Warehouse](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)   
 [sys.pdw_table_mappings &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-pdw-table-mappings-transact-sql.md)   
 [sys.pdw_database_mappings &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-pdw-database-mappings-transact-sql.md)  
  
  
