---
title: sys. pdw_health_alerts (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: conceptual
ms.assetid: 49c01e5f-ee47-41a0-871d-35a759f50851
author: ronortloff
ms.author: rortloff
monikerRange: '>= aps-pdw-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 2e3ab735a19342e1ecc1a941a185832edae61262
ms.sourcegitcommit: 1be90e93980a8e92275b5cc072b12b9e68a3bb9a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/09/2020
ms.locfileid: "84627446"
---
# <a name="syspdw_health_alerts-transact-sql"></a>sys. pdw_health_alerts (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md.md)]

  Armazena propriedades para os diferentes alertas que podem ocorrer no sistema; Esta é uma tabela de catálogo para alertas.  
  
|Nome da coluna|Tipo de Dados|Descrição|Intervalo|  
|-----------------|---------------|-----------------|-----------|  
|alert_id|**int**|Identificador exclusivo do alerta.<br /><br /> Chave para esta exibição.|NOT NULL|  
|component_id|**int**|ID do componente ao qual este alerta se aplica. O componente é um identificador de componente geral, como "fonte de energia", e não é específico de uma instalação. Consulte [Sys. pdw_health_components &#40;&#41;Transact-SQL ](../../relational-databases/system-catalog-views/sys-pdw-health-components-transact-sql.md).|NOT NULL|  
|alert_name|**nvarchar (255)**|Nome do alerta.|NOT NULL|  
|state|**nvarchar(32)**|Estado do alerta.|NOT NULL<br /><br /> Valores possíveis:<br /><br /> Eficiência<br /><br /> ' Não operacional '<br /><br /> Degradado<br /><br /> Falha ao|  
|severidade|**nvarchar(32)**|Severidade do alerta.|NOT NULL<br /><br /> Valores possíveis:<br /><br /> Informativa<br /><br /> Alerta<br /><br /> Ao|  
|tipo|**nvarchar(32)**|Tipo de alerta.|NOT NULL<br /><br /> Valores possíveis:<br /><br /> StatusChange-o status do dispositivo foi alterado.<br /><br /> Limite-um valor excedeu o valor do limite.|  
|descrição|**nvarchar(4000)**|Descrição do alerta.|NOT NULL|  
|condition|**nvarchar (255)**|Usado quando tipo = limite. Define como o limite de alerta é calculado.|NULO|  
|status|**nvarchar(32)**|Status do alerta|NULO|  
|condition_value|**bit**|Indica se o alerta pode ocorrer durante a operação do sistema.|NULO<br /><br /> Valores possíveis<br /><br /> 0-o alerta não é gerado.<br /><br /> 1-o alerta é gerado.|  
  
## <a name="see-also"></a>Consulte Também  
 [Exibições de Catálogo do SQL Data Warehouse e Parallel Data Warehouse](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)  
  
  
