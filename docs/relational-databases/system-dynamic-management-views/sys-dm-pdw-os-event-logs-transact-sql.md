---
title: sys.dm_pdw_os_event_logs (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: a0daa8cf-72e2-4349-8be1-d3cc0f9b1e02
caps.latest.revision: 7
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>= aps-pdw-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 3311090840a2373652239e03f125b86030030a9d
ms.sourcegitcommit: 7019ac41524bdf783ea2c129c17b54581951b515
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/23/2018
ms.locfileid: "34466692"
---
# <a name="sysdmpdwoseventlogs-transact-sql"></a>sys.dm_pdw_os_event_logs (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md.md)]

  Contém informações sobre os diferentes eventos do Windows registra em nós diferentes.  
  
|Nome da coluna|Tipo de dados|Description|Intervalo|  
|-----------------|---------------|-----------------|-----------|  
|pdw_node_id|**Int**|Esse log é de um nó de dispositivo.<br /><br /> pdw_node_id e nome_registo formam a chave para este modo de exibição.||  
|nome_registo|**nvarchar(255)**|Nome do log de eventos do Windows.<br /><br /> pdw_node_id e nome_registo formam a chave para este modo de exibição.||  
|log_source|**nvarchar(255)**|Nome de origem de log de eventos do Windows.||  
|event_id|**Int**|ID do evento. Não é exclusivo.||  
|event_type|**nvarchar(255)**|Tipo de evento, identificando a gravidade.|'Informações', 'Aviso', 'Erro'|  
|event_message|**nvarchar(4000)**|Detalhes do evento.||  
|generate_time|**datetime**|Hora que do evento foi criado.||  
|write_time|**datetime**|O evento realmente foi gravado no log de tempo.||  
  
 Para obter informações sobre o máximo de linhas mantido por esta exibição, consulte a seção de valores máximos de modo de exibição de sistema no [valores mínimo e máximo (SQL Server PDW)](http://msdn.microsoft.com/en-us/5243f018-2713-45e3-9b61-39b2a57401b9) tópico.  
  
## <a name="see-also"></a>Consulte também  
 [SQL Data Warehouse Parallel Data Warehouse e exibições de gerenciamento dinâmico &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
