---
title: sys. spatial_indexes (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.spatial_indexes_TSQL
- spatial_indexes
- spatial_indexes_TSQL
- sys.spatial_indexes
dev_langs:
- TSQL
helpviewer_keywords:
- sys.spatial_indexes catalog view
ms.assetid: 40e967d5-2e8d-45af-bf5e-5251493cf7cb
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: a5264661a94b4802d6f06ab1af8ae74436b63b09
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/05/2020
ms.locfileid: "82833965"
---
# <a name="sysspatial_indexes-transact-sql"></a>sys.spatial_indexes (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Representa as principais informações dos índices espaciais.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|\<colunas herdadas>||Herda colunas de [Sys. Indexes](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md).|  
|spatial_index_type|**tinyint**|Tipo de índice espacial:<br /><br /> 1 = Índice espacial geométrico<br /><br /> 2 = Índice espacial geográfico|  
|spatial_index_type_desc|**nvarchar(60)**|Descrição do tipo de índice espacial:<br /><br /> GEOMETRY = Índice espacial geométrico<br /><br /> GEOGRAPHY = Índice espacial geográfico|  
|tessellation_scheme|**sysname**|Nome do esquema de mosaico:<br /><br /> GEOMETRY_GRID, GEOMETRY_AUTO_GRID,<br /><br /> GEOGRAPHY_GRID, GEOGRAPHY_AUTO_GRID<br /><br /> Observação: para obter informações sobre esquemas de mosaico, consulte [visão geral de índices espaciais](../../relational-databases/spatial/spatial-indexes-overview.md).|  
|\<colunas herdadas>||Herda colunas de [Sys. Indexes](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md).<br /><br /> As colunas herdadas has_filter and filter_definition são exibidas depois das colunas que são específicas para índices espaciais.|  
  
## <a name="permissions"></a>Permissões  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)]  
  
## <a name="see-also"></a>Consulte Também  
 [sys. Objects &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)   
 [sys. spatial_index_tessellations &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-spatial-index-tessellations-transact-sql.md)   
 [sys. Indexes &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)   
 [sys. index_columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-index-columns-transact-sql.md)   
 [Visão geral de índices espaciais](../../relational-databases/spatial/spatial-indexes-overview.md)  
  
  
