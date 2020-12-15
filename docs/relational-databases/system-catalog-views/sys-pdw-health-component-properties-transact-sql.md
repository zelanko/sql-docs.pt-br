---
description: sys.pdw_health_component_properties (Transact-SQL)
title: sys.pdw_health_component_properties (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: conceptual
ms.assetid: 66999c0c-dc43-4327-99fb-8366f465e69d
author: ronortloff
ms.author: rortloff
monikerRange: '>= aps-pdw-2016'
ms.openlocfilehash: a6446cb81a33fef53ac398f9e23bd080b310ede4
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97439471"
---
# <a name="syspdw_health_component_properties-transact-sql"></a>sys.pdw_health_component_properties (Transact-SQL)
[!INCLUDE [pdw](../../includes/applies-to-version/pdw.md)]

  Armazena as propriedades que descrevem um dispositivo. Algumas propriedades mostram o status do dispositivo e algumas propriedades descrevem o próprio dispositivo.  
  
|Nome da coluna|Tipo de Dados|DESCRIÇÃO|Intervalo|  
|-----------------|---------------|-----------------|-----------|  
|property_id|**int**|Identificador exclusivo da propriedade de um componente.<br /><br /> property_id e component_id formate a chave para essa exibição.|NOT NULL|  
|component_id|**int**|A ID do componente. Confira [sys.pdw_health_components &#40;&#41;Transact-SQL ](../../relational-databases/system-catalog-views/sys-pdw-health-components-transact-sql.md).<br /><br /> property_id e component_id formate a chave para essa exibição.|NOT NULL|  
|property_name|**nvarchar(255)**|Nome da propriedade.|NOT NULL|  
|physical_name|**nvarchar(32)**|Nome da propriedade, conforme definido pelo fabricante.|NOT NULL|  
|is_key|**bit**|Determina se a instância do dispositivo é exclusiva ou não exclusiva.|NOT NULL<br /><br /> 0-a instância do dispositivo é exclusiva.<br /><br /> 1-a instância do dispositivo não é exclusiva.|  
  
## <a name="see-also"></a>Consulte Também  
 [Exibições de Catálogo do Azure Synapse Analytics e do Parallel Data Warehouse](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)  
  
  
