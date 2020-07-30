---
title: sys. dm_pdw_os_event_logs (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: a0daa8cf-72e2-4349-8be1-d3cc0f9b1e02
author: CarlRabeler
ms.author: carlrab
monikerRange: '>= aps-pdw-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 086666160c990ee2606688376db624c1aee5fbf9
ms.sourcegitcommit: df1f0f2dfb9452f16471e740273cd1478ff3100c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/29/2020
ms.locfileid: "87396616"
---
# <a name="sysdm_pdw_os_event_logs-transact-sql"></a>sys. dm_pdw_os_event_logs (Transact-SQL)
[!INCLUDE [pdw](../../includes/applies-to-version/pdw.md)]

  Contém informações sobre os diferentes logs de eventos do Windows em nós diferentes.  
  
|Nome da coluna|Tipo de Dados|DESCRIÇÃO|Intervalo|  
|-----------------|---------------|-----------------|-----------|  
|pdw_node_id|**int**|Nó do dispositivo do qual este log se encontra.<br /><br /> pdw_node_id e log_name formate a chave para essa exibição.||  
|log_name|**nvarchar(255)**|Nome do log de eventos do Windows.<br /><br /> pdw_node_id e log_name formate a chave para essa exibição.||  
|log_source|**nvarchar(255)**|Nome de origem do log de eventos do Windows.||  
|event_id|**int**|ID do evento. Não exclusivo.||  
|event_type|**nvarchar(255)**|Tipo do evento, identificando a severidade.|' Informações ', ' aviso ', ' erro '|  
|event_message|**nvarchar(4000)**|Detalhes do evento.||  
|generate_time|**datetime**|Hora em que o evento foi criado.||  
|write_time|**datetime**|Hora em que o evento foi realmente gravado no log.||  
  
 Para obter informações sobre o máximo de linhas retidas por essa exibição, consulte a seção de metadados no tópico [limites de capacidade](/azure/sql-data-warehouse/sql-data-warehouse-service-capacity-limits#metadata) . 
  
## <a name="see-also"></a>Consulte Também  
 [Exibições de gerenciamento dinâmico de SQL Data Warehouse e paralelo data warehouse &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
