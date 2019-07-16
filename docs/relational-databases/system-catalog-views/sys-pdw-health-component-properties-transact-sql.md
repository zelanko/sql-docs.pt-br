---
title: sys.pdw_health_component_properties (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.technology: system-objects
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: 66999c0c-dc43-4327-99fb-8366f465e69d
author: ronortloff
ms.author: rortloff
monikerRange: '>= aps-pdw-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: c2bca7f0deef9a5cb137525e165670404cad65ae
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68016556"
---
# <a name="syspdwhealthcomponentproperties-transact-sql"></a>sys.pdw_health_component_properties (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md.md)]

  Armazena as propriedades que descrevem um dispositivo. Algumas propriedades mostram o status do dispositivo e algumas propriedades descrevem o próprio dispositivo.  
  
|Nome da coluna|Tipo de dados|Descrição|Intervalo|  
|-----------------|---------------|-----------------|-----------|  
|property_id|**int**|Identificador exclusivo da propriedade de um componente.<br /><br /> property_id e identificação_do_componente formam a chave para esta exibição.|NOT NULL|  
|component_id|**int**|A ID do componente. Ver [sys.pdw_health_components &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-pdw-health-components-transact-sql.md).<br /><br /> property_id e identificação_do_componente formam a chave para esta exibição.|NOT NULL|  
|property_name|**nvarchar(255)**|Nome da propriedade.|NOT NULL|  
|physical_name|**nvarchar(32)**|Nome da propriedade conforme definido pelo fabricante.|NOT NULL|  
|is_key|**bit**|Determina se a instância do dispositivo é exclusivo ou não exclusivo.|NOT NULL<br /><br /> 0 - a instância do dispositivo é exclusiva.<br /><br /> 1 - a instância de dispositivo não é exclusiva.|  
  
## <a name="see-also"></a>Consulte também  
 [SQL Data Warehouse e Parallel Data Warehouse exibições do catálogo](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)  
  
  
