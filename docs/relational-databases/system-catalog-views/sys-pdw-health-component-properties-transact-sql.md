---
description: sys. pdw_health_component_properties (Transact-SQL)
title: sys. pdw_health_component_properties (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: conceptual
ms.assetid: 66999c0c-dc43-4327-99fb-8366f465e69d
author: ronortloff
ms.author: rortloff
monikerRange: '>= aps-pdw-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: b39e099e2b76c740621fa6844409955d2452d936
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88475373"
---
# <a name="syspdw_health_component_properties-transact-sql"></a>sys. pdw_health_component_properties (Transact-SQL)
[!INCLUDE [pdw](../../includes/applies-to-version/pdw.md)]

  Armazena as propriedades que descrevem um dispositivo. Algumas propriedades mostram o status do dispositivo e algumas propriedades descrevem o próprio dispositivo.  
  
|Nome da coluna|Tipo de Dados|DESCRIÇÃO|Intervalo|  
|-----------------|---------------|-----------------|-----------|  
|property_id|**int**|Identificador exclusivo da propriedade de um componente.<br /><br /> property_id e component_id formate a chave para essa exibição.|NOT NULL|  
|component_id|**int**|A ID do componente. Consulte [Sys. pdw_health_components &#40;&#41;Transact-SQL ](../../relational-databases/system-catalog-views/sys-pdw-health-components-transact-sql.md).<br /><br /> property_id e component_id formate a chave para essa exibição.|NOT NULL|  
|property_name|**nvarchar(255)**|Nome da propriedade.|NOT NULL|  
|physical_name|**nvarchar(32)**|Nome da propriedade, conforme definido pelo fabricante.|NOT NULL|  
|is_key|**bit**|Determina se a instância do dispositivo é exclusiva ou não exclusiva.|NOT NULL<br /><br /> 0-a instância do dispositivo é exclusiva.<br /><br /> 1-a instância do dispositivo não é exclusiva.|  
  
## <a name="see-also"></a>Consulte Também  
 [Exibições de Catálogo do SQL Data Warehouse e Parallel Data Warehouse](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)  
  
  
