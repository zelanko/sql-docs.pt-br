---
title: sys.pdw_health_alerts (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.technology: system-objects
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: 49c01e5f-ee47-41a0-871d-35a759f50851
author: ronortloff
ms.author: rortloff
manager: craigg
monikerRange: '>= aps-pdw-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 41ae6d70399dea79a92cbc4fd77ba6e08f660d7c
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/11/2019
ms.locfileid: "56025447"
---
# <a name="syspdwhealthalerts-transact-sql"></a>sys.pdw_health_alerts (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md.md)]

  Armazena as propriedades para os alertas diferentes que podem ocorrer no sistema. Essa é uma tabela de catálogo para alertas.  
  
|Nome da coluna|Tipo de Dados|Descrição|Intervalo|  
|-----------------|---------------|-----------------|-----------|  
|alert_id|**int**|Identificador exclusivo do alerta.<br /><br /> A chave para este modo de exibição.|NOT NULL|  
|component_id|**int**|ID do componente a que esse alerta aplica-se. O componente é um identificador de componente gerais, como "Fonte de energia" e não é específico para uma instalação. Ver [sys.pdw_health_components &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-pdw-health-components-transact-sql.md).|NOT NULL|  
|alert_name|**nvarchar(255)**|Nome do alerta.|NOT NULL|  
|state|**nvarchar(32)**|Estado do alerta.|NOT NULL<br /><br /> Valores possíveis:<br /><br /> 'Operacional'<br /><br /> 'NonOperational'<br /><br /> 'Degradado'<br /><br /> 'Failed'|  
|severidade|**nvarchar(32)**|Severidade do alerta.|NOT NULL<br /><br /> Valores possíveis:<br /><br /> 'Informacional'<br /><br /> 'Warning'<br /><br /> 'Error'|  
|Tipo|**nvarchar(32)**|Tipo de alerta.|NOT NULL<br /><br /> Valores possíveis:<br /><br /> StatusChange - o status do dispositivo foi alterado.<br /><br /> Limite - um valor excedeu o valor de limite.|  
|descrição|**nvarchar(4000)**|Descrição do alerta.|NOT NULL|  
|Condição|**nvarchar(255)**|Usado quando digite = limite. Define como o limite de alerta é calculado.|NULL|  
|status|**nvarchar(32)**|Status do alerta|NULL|  
|condition_value|**bit**|Indica se o alerta pode ocorrer durante a operação do sistema.|NULL<br /><br /> Valores possíveis<br /><br /> 0 - o alerta não é gerado.<br /><br /> 1 - alerta é gerado.|  
  
## <a name="see-also"></a>Consulte também  
 [SQL Data Warehouse e Parallel Data Warehouse exibições do catálogo](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)  
  
  
