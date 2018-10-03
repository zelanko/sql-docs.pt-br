---
title: sys.dm_pdw_os_event_logs (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: a0daa8cf-72e2-4349-8be1-d3cc0f9b1e02
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>= aps-pdw-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: ad9c7b96858c1ded81c2651c389ae63490af6408
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47699194"
---
# <a name="sysdmpdwoseventlogs-transact-sql"></a>sys.dm_pdw_os_event_logs (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md.md)]

  Contém informações sobre o evento do Windows diferentes logs em nós diferentes.  
  
|Nome da coluna|Tipo de dados|Description|Intervalo|  
|-----------------|---------------|-----------------|-----------|  
|pdw_node_id|**int**|Esse log é de um nó de dispositivo.<br /><br /> pdw_node_id e nome_registo formam a chave para esta exibição.||  
|nome_registo|**nvarchar(255)**|Nome de log de eventos do Windows.<br /><br /> pdw_node_id e nome_registo formam a chave para esta exibição.||  
|log_source|**nvarchar(255)**|Nome de origem de log de eventos do Windows.||  
|event_id|**int**|ID do evento. Não é exclusivo.||  
|event_type|**nvarchar(255)**|Tipo de evento, identificando a gravidade.|'Informações', 'Aviso', 'Error'|  
|event_message|**nvarchar(4000)**|Detalhes do evento.||  
|generate_time|**datetime**|Tempo que o evento foi criado.||  
|write_time|**datetime**|Na verdade, o evento foi gravado no log de tempo.||  
  
 Para obter informações sobre o máximo de linhas mantido por esta exibição, consulte a seção de valores máximos de modo de exibição de sistema na [valores mínimo e máximo (SQL Server PDW)](http://msdn.microsoft.com/5243f018-2713-45e3-9b61-39b2a57401b9) tópico.  
  
## <a name="see-also"></a>Consulte também  
 [SQL Data Warehouse e Parallel Data Warehouse exibições de gerenciamento dinâmico &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
