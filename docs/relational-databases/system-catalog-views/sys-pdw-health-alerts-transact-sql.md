---
title: sys.pdw_health_alerts (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.prod_service: pdw
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 49c01e5f-ee47-41a0-871d-35a759f50851
caps.latest.revision: "7"
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 0f7e05ccc9cc264faf5d4d7f563d1df028969309
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="syspdwhealthalerts-transact-sql"></a>sys.pdw_health_alerts (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md.md)]

  Armazena as propriedades para os alertas de diferentes que podem ocorrer no sistema. Essa é uma tabela de catálogo para alertas.  
  
|Nome da coluna|Tipo de dados|Description|Intervalo|  
|-----------------|---------------|-----------------|-----------|  
|alert_id|**int**|Identificador exclusivo do alerta.<br /><br /> Chave para este modo de exibição.|NOT NULL|  
|identificação_do_componente|**int**|ID do componente que esse alerta se aplica. O componente é um identificador de componente geral, como "Fonte de alimentação" e não é específico para uma instalação. Consulte [sys.pdw_health_components &#40; Transact-SQL &#41; ](../../relational-databases/system-catalog-views/sys-pdw-health-components-transact-sql.md).|NOT NULL|  
|alert_name|**nvarchar(255)**|Nome do alerta.|NOT NULL|  
|state|**nvarchar (32)**|Estado do alerta.|NOT NULL<br /><br /> Valores possíveis:<br /><br /> 'Operacional'<br /><br /> 'Não-operacional'<br /><br /> 'Degradado'<br /><br /> 'Com falha'|  
|severidade|**nvarchar (32)**|Severidade do alerta.|NOT NULL<br /><br /> Valores possíveis:<br /><br /> 'Informativo'<br /><br /> 'Aviso'<br /><br /> 'Erro'|  
|Tipo|**nvarchar (32)**|Tipo de alerta.|NOT NULL<br /><br /> Valores possíveis:<br /><br /> StatusChange - o status do dispositivo foi alterado.<br /><br /> Limite - um valor excedeu o valor de limite.|  
|descrição|**nvarchar(4000)**|Descrição do alerta.|NOT NULL|  
|condição|**nvarchar(255)**|Tipo usado quando = limite. Define como o limite de alerta é calculado.|NULL|  
|status|**nvarchar (32)**|Status do alerta|NULL|  
|condition_value|**bit**|Indica se o alerta pode ocorrer durante a operação do sistema.|NULL<br /><br /> Valores possíveis<br /><br /> 0 - o alerta não é gerado.<br /><br /> 1 - alerta é gerado.|  
  
## <a name="see-also"></a>Consulte também  
 [SQL Data Warehouse e exibições de catálogo do Parallel Data Warehouse](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)  
  
  
