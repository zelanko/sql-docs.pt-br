---
title: sys. pdw_health_component_status_mappings (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.technology: system-objects
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: 4272cfad-5ad7-493d-9edd-d9111619bda0
author: ronortloff
ms.author: rortloff
monikerRange: '>= aps-pdw-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: ec631e9008cc37a7b4f91ed3f530e5388bdf9c0d
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68127495"
---
# <a name="syspdw_health_component_status_mappings-transact-sql"></a>sys. pdw_health_component_status_mappings (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md.md)]

  Define o mapeamento entre os [!INCLUDE[ssDW](../../includes/ssdw-md.md)] status do componente e os nomes de componentes definidos pelo fabricante.  
  
|Nome da coluna|Tipo de Dados|DESCRIÇÃO|Intervalo|  
|-----------------|---------------|-----------------|-----------|  
|property_id|**int**|Identificador exclusivo da propriedade.<br /><br /> property_id, component_id e physical_name formam a chave para essa exibição.|NOT NULL|  
|component_id|**int**|A ID do componente. Consulte [Sys. pdw_health_components &#40;&#41;Transact-SQL ](../../relational-databases/system-catalog-views/sys-pdw-health-components-transact-sql.md).<br /><br /> property_id, component_id e physical_name formam a chave para essa exibição.|NOT NULL|  
|physical_name|**nvarchar (32)**|Nome da propriedade, conforme definido pelo fabricante.<br /><br /> property_id, component_id e physical_name formam a chave para essa exibição.|NOT NULL|  
|logical_name|**nvarchar (255)**|Nome da propriedade, conforme [!INCLUDE[ssDW](../../includes/ssdw-md.md)]definido por.|NOT NULL<br /><br /> 0-a instância do dispositivo é exclusiva.<br /><br /> 1-a instância do dispositivo não é exclusiva.|  
  
## <a name="see-also"></a>Consulte Também  
 [Exibições de Catálogo do SQL Data Warehouse e Parallel Data Warehouse](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)  
  
  
