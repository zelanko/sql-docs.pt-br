---
title: sys. pdw_materialized_view_column_distribution_properties (Transact-SQL)
ms.custom: seo-dt-2019
ms.date: 07/03/2019
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: jrasnick
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: d62b0e25-3226-4f87-a10a-b3a0d9555e19
author: XiaoyuMSFT
ms.author: xiaoyul
monikerRange: = azure-sqldw-latest || = sqlallproducts-allversions
ms.openlocfilehash: 5d5bc07ec3d00ec486d219aaab8980647c6ebfa7
ms.sourcegitcommit: df1f0f2dfb9452f16471e740273cd1478ff3100c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/29/2020
ms.locfileid: "87394111"
---
# <a name="syspdw_materialized_view_column_distribution_properties-transact-sql"></a>sys. pdw_materialized_view_column_distribution_properties (Transact-SQL) 

[!INCLUDE [asa](../../includes/applies-to-version/asa.md)]

Exibe informações de distribuição para colunas em uma exibição materializada.  
  
|Nome da coluna|Tipo de Dados|Descrição|  
|-----------------|---------------|-----------------|  
|object_id|**int**|ID do objeto ao qual a coluna pertence. |  
|column_id|**int**|A ID da coluna.|  
|distribution_ordinal|**tinyint**|0 = não é uma coluna de distribuição.</br> 1 = SQL Data Warehouse está usando essa coluna para distribuir a exibição materializada.|
 
## <a name="permissions"></a>Permissões 

Requer a permissão VIEW DATABASE STATE.

## <a name="see-also"></a>Confira também

[Ajuste de desempenho com exibição materializada](/azure/sql-data-warehouse/performance-tuning-materialized-views)   
[CREATE MATERIALIZED VIEW AS SELECT &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-materialized-view-as-select-transact-sql?view=azure-sqldw-latest)   
[ALTER MATERIALIZED VIEW &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-materialized-view-transact-sql?view=azure-sqldw-latest)   
[EXPLICAR &#40;&#41;Transact-SQL](/sql/t-sql/queries/explain-transact-sql?view=azure-sqldw-latest)   
[sys.pdw_materialized_view_distribution_properties &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-pdw-materialized-view-distribution-properties-transact-sql?view=azure-sqldw-latest)   
[sys.pdw_materialized_view_mappings &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-pdw-materialized-view-mappings-transact-sql?view=azure-sqldw-latest)   
[DBCC PDW_SHOWMATERIALIZEDVIEWOVERHEAD &#40;Transact-SQL&#41;](/sql/t-sql/database-console-commands/dbcc-pdw-showmaterializedviewoverhead-transact-sql?view=azure-sqldw-latest)   
[Exibições de Catálogo do SQL Data Warehouse e Parallel Data Warehouse](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)   
[Exibições do sistema com suporte no SQL Data Warehouse do Azure](/azure/sql-data-warehouse/sql-data-warehouse-reference-tsql-system-views)   
[Instruções T-SQL com suporte no SQL Data Warehouse do Azure](/azure/sql-data-warehouse/sql-data-warehouse-reference-tsql-statements)
