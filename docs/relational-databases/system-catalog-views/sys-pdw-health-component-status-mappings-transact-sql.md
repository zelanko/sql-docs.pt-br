---
description: sys.pdw_health_component_status_mappings (Transact-SQL)
title: sys.pdw_health_component_status_mappings (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: conceptual
ms.assetid: 4272cfad-5ad7-493d-9edd-d9111619bda0
author: ronortloff
ms.author: rortloff
monikerRange: '>= aps-pdw-2016'
ms.openlocfilehash: d0d5bfea5d43315fed6b74f8767cea6cb89904a9
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97466937"
---
# <a name="syspdw_health_component_status_mappings-transact-sql"></a>sys.pdw_health_component_status_mappings (Transact-SQL)
[!INCLUDE [pdw](../../includes/applies-to-version/pdw.md)]

  Define o mapeamento entre os [!INCLUDE[ssDW](../../includes/ssdw-md.md)] status do componente e os nomes de componentes definidos pelo fabricante.  
  
|Nome da coluna|Tipo de Dados|DESCRIÇÃO|Intervalo|  
|-----------------|---------------|-----------------|-----------|  
|property_id|**int**|Identificador exclusivo da propriedade.<br /><br /> property_id, component_id e physical_name formam a chave para essa exibição.|NOT NULL|  
|component_id|**int**|A ID do componente. Confira [sys.pdw_health_components &#40;&#41;Transact-SQL ](../../relational-databases/system-catalog-views/sys-pdw-health-components-transact-sql.md).<br /><br /> property_id, component_id e physical_name formam a chave para essa exibição.|NOT NULL|  
|physical_name|**nvarchar(32)**|Nome da propriedade, conforme definido pelo fabricante.<br /><br /> property_id, component_id e physical_name formam a chave para essa exibição.|NOT NULL|  
|logical_name|**nvarchar(255)**|Nome da propriedade, conforme definido por [!INCLUDE[ssDW](../../includes/ssdw-md.md)] .|NOT NULL<br /><br /> 0-a instância do dispositivo é exclusiva.<br /><br /> 1-a instância do dispositivo não é exclusiva.|  
  
## <a name="see-also"></a>Consulte Também  
 [Exibições de Catálogo do Azure Synapse Analytics e do Parallel Data Warehouse](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)  
  
  
