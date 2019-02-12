---
title: sys.pdw_health_component_status_mappings (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.technology: system-objects
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: 4272cfad-5ad7-493d-9edd-d9111619bda0
author: ronortloff
ms.author: rortloff
manager: craigg
monikerRange: '>= aps-pdw-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 02771656dfdb0b7396e62a5bde364b0eea324aa0
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/11/2019
ms.locfileid: "56031187"
---
# <a name="syspdwhealthcomponentstatusmappings-transact-sql"></a>sys.pdw_health_component_status_mappings (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md.md)]

  Define o mapeamento entre o [!INCLUDE[ssDW](../../includes/ssdw-md.md)] status do componente e os nomes definidos pelo fabricante do componente.  
  
|Nome da coluna|Tipo de Dados|Descrição|Intervalo|  
|-----------------|---------------|-----------------|-----------|  
|property_id|**int**|Identificador exclusivo da propriedade.<br /><br /> property_id e identificação_do_componente physical_name formam a chave para esta exibição.|NOT NULL|  
|component_id|**int**|A ID do componente. Ver [sys.pdw_health_components &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-pdw-health-components-transact-sql.md).<br /><br /> property_id e identificação_do_componente physical_name formam a chave para esta exibição.|NOT NULL|  
|physical_name|**nvarchar(32)**|Nome da propriedade conforme definido pelo fabricante.<br /><br /> property_id e identificação_do_componente physical_name formam a chave para esta exibição.|NOT NULL|  
|logical_name|**nvarchar(255)**|Nome da propriedade conforme definido pelo [!INCLUDE[ssDW](../../includes/ssdw-md.md)].|NOT NULL<br /><br /> 0 - a instância do dispositivo é exclusiva.<br /><br /> 1 - a instância de dispositivo não é exclusiva.|  
  
## <a name="see-also"></a>Consulte também  
 [SQL Data Warehouse e Parallel Data Warehouse exibições do catálogo](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)  
  
  
