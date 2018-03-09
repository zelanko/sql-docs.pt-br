---
title: spatial_index_tessellations (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- spatial_index_tessellations
- sys.spatial_index_tessellations_TSQL
- spatial_index_tessellations_TSQL
- sys.spatial_index_tessellations
dev_langs: TSQL
helpviewer_keywords: sys.spatial_index_tessellations catalog view
ms.assetid: 8b17a9a4-b57f-4220-8138-fc73581b1670
caps.latest.revision: "30"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: fdac2e76ed1bc15a97981d91285569b4a18eb0a1
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="sysspatialindextessellations-transact-sql"></a>sys.spatial_index_tessellations (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

 Representa as informações sobre o esquema de mosaico e os parâmetros de cada um dos índices espaciais.  
  
> [!NOTE]  
>  Para obter informações sobre mosaico, consulte [visão geral de índices espaciais](../../relational-databases/spatial/spatial-indexes-overview.md).  
  

|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|object_id|**int**|ID do objeto no qual o índice é definido. Cada (object_id, index_id) par tem uma entrada correspondente em [spatial_indexes](../../relational-databases/system-catalog-views/sys-spatial-indexes-transact-sql.md).|  
|index_id|**int**|ID do índice espacial no qual a coluna indexada é definida.|  
|tessellation_scheme|**sysname**|Nome do esquema de mosaico, um dos: GEOMETRY_GRID, GEOGRAPHY_GRID|  
|bounding_box_xmin|**float(53)**|A coordenada X do canto inferior esquerdo da delimitadora caixa, um dos: NULL = não aplicável para um determinado esquema de mosaico (como GEOGRAPHY_GRID)  *n*  = se tessellation_scheme for GEOMETRY_GRID, a coordenada x mínima valor.                     **Observação:** as coordenadas definidas pelos parâmetros de caixa delimitadora são interpretadas para cada objeto de acordo com seu [identificador de referência espacial (SRID)](../../relational-databases/spatial/spatial-reference-identifiers-srids.md).|  
|bounding_box_ymin|**float(53)**|A coordenada Y do canto inferior esquerdo da delimitadora caixa, um dos: NULL = não aplicável para um determinado esquema de mosaico (como GEOGRAPHY_GRID)  *n*  = se tessellation_scheme for GEOMETRY_GRID, a coordenada y mínima valor|  
|bounding_box_xmax|**float(53)**|A coordenada X do canto superior direito da delimitadora caixa, um dos: NULL = não aplicável para um determinado esquema de mosaico (como GEOGRAPHY_GRID)  *n*  = se tessellation_scheme for GEOMETRY_GRID, a coordenada x máxima valor|  
|bounding_box_ymax|**float(53)**|Coordenada Y do canto superior direito da delimitadora caixa, um dos: NULL = não aplicável para um determinado esquema de mosaico (como GEOGRAPHY_GRID)  *n*  = se tessellation_scheme for GEOMETRY_GRID, o valor máximo da coordenada y|  
|level_1_grid|**smallint**|Densidade de grade para a grade de nível superior. Se tessellation_scheme for GEOMETRY_GRID ou GEOGRAPHY_GRID, um de: 16 = grade 4 por 4 (baixa) 64 = 8 por 8 grade (médio) 256 = 16 por 16 grade (alto) NULL = não aplicável para determinados índice espacial tipo ou esquema de mosaico.  NULL é retornado quando o novo mosaico do SQL Server 11 é usado.|  
|level_1_grid_desc|**nvarchar (60)**|Densidade de grade para grade de nível superior, um de: baixo Média alta NULL = não aplicável para determinados índice espacial tipo ou esquema de mosaico.  NULL é retornado quando o novo mosaico do SQL Server 11 é usado.|  
|level_2_grid|**smallint**|Densidade de grade para a grade de 2º nível. Se tessellation_scheme for GEOMETRY_GRID ou GEOGRAPHY_GRID, um de: 16 = grade 4 por 4 (baixa) 64 = 8 por 8 grade (médio) 256 = 16 por 16 grade (alto) NULL = não aplicável para determinados índice espacial tipo ou esquema de mosaico.  NULL é retornado quando o novo mosaico do SQL Server 11 é usado.|  
|level_2_grid_desc|**nvarchar (60)**|Densidade da grade para grade de 2º nível, um de: baixo Média alta NULL = não aplicável para determinados índice espacial tipo ou esquema de mosaico.  NULL é retornado quando o novo mosaico do SQL Server 11 é usado.|  
|level_3_grid|**smallint**|Densidade de grade para grade de 3º nível.   Se tessellation_scheme for GEOMETRY_GRID ou GEOGRAPHY_GRID, um de: 16 = grade 4 por 4 (baixa) 64 = 8 por 8 grade (médio) 256 = 16 por 16 grade (alto) NULL = não aplicável para determinados índice espacial tipo ou esquema de mosaico.  NULL é retornado quando o novo mosaico do SQL Server 11 é usado.|  
|level_3_grid_desc|**nvarchar (60)**|Densidade da grade para grade de 3º nível, um de: baixo Média alta NULL = não aplicável para determinados índice espacial tipo ou esquema de mosaico.  NULL é retornado quando o novo mosaico do SQL Server 11 é usado.|  
|level_4_grid|**smallint**|Densidade de grade para grade de 4º nível. Se tessellation_scheme for GEOMETRY_GRID ou GEOGRAPHY_GRID, um de: 16 = grade 4 por 4 (baixa) 64 = 8 por 8 grade (médio) 256 = 16 por 16 grade (alto) NULL = não aplicável para determinados índice espacial tipo ou esquema de mosaico.  NULL é retornado quando o novo mosaico do SQL Server 11 é usado.|  
|level_4_grid_desc|**nvarchar (60)**|Densidade da grade para grade de 4º nível, um de: < baixa Média alta NULL = não aplicável para determinados índice espacial tipo ou esquema de mosaico.  NULL é retornado quando o novo mosaico do SQL Server 11 é usado.|  
|cells_per_object|**int**|Número de células por objeto espacial, um de: se tessellation_scheme for GEOMETRY_GRID ou GEOGRAPHY_GRID,  *n*  = número de células por objeto NULL = não aplicável para determinados índice espacial tipo ou esquema de mosaico|  
  
## <a name="permissions"></a>Permissões  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)]  
  
## <a name="see-also"></a>Consulte também  
 [Exibições de catálogo de objeto &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [Visão geral de índices espaciais](../../relational-databases/spatial/spatial-indexes-overview.md)   
 [sys. Objects &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)   
 [spatial_indexes &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-spatial-indexes-transact-sql.md)   
 [sys.indexes &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)   
 [sys.index_columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-index-columns-transact-sql.md)  
  
  
