---
title: sys.dm_pdw_os_event_logs (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.technology: system-objects
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: a0daa8cf-72e2-4349-8be1-d3cc0f9b1e02
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>= aps-pdw-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 44a24b12c284cf253838bc1c2252e4081b8efe98
ms.sourcegitcommit: 706f3a89fdb98e84569973f35a3032f324a92771
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2019
ms.locfileid: "58657225"
---
# <a name="sysdmpdwoseventlogs-transact-sql"></a>sys.dm_pdw_os_event_logs (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md.md)]

  Contém informações sobre o evento do Windows diferentes logs em nós diferentes.  
  
|Nome da coluna|Tipo de Dados|Descrição|Intervalo|  
|-----------------|---------------|-----------------|-----------|  
|pdw_node_id|**int**|Esse log é de um nó de dispositivo.<br /><br /> pdw_node_id e nome_registo formam a chave para esta exibição.||  
|log_name|**nvarchar(255)**|Nome de log de eventos do Windows.<br /><br /> pdw_node_id e nome_registo formam a chave para esta exibição.||  
|log_source|**nvarchar(255)**|Nome de origem de log de eventos do Windows.||  
|event_id|**int**|ID do evento. Não é exclusivo.||  
|event_type|**nvarchar(255)**|Tipo de evento, identificando a gravidade.|'Information', 'Warning', 'Error'|  
|event_message|**nvarchar(4000)**|Detalhes do evento.||  
|generate_time|**datetime**|Tempo que o evento foi criado.||  
|write_time|**datetime**|Na verdade, o evento foi gravado no log de tempo.||  
  
 Para obter informações sobre o máximo de linhas mantido por esta exibição, consulte a seção de metadados na [limites de capacidade](/azure/sql-data-warehouse/sql-data-warehouse-service-capacity-limits#metadata) tópico. 
  
## <a name="see-also"></a>Consulte também  
 [SQL Data Warehouse e Parallel Data Warehouse exibições de gerenciamento dinâmico &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
