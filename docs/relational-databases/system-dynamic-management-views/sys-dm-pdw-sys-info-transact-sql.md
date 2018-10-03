---
title: sys.dm_pdw_sys_info (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: ''
ms.prod_service: sql-data-warehouse, pdw
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 686976b4-2d5d-4d64-bf12-56eba1dc59b1
author: ronortloff
ms.author: rortloff
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: ad7311759e2ea38f5b9b375785b7f035d1dcdbfa
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47821514"
---
# <a name="sysdmpdwsysinfo-transact-sql"></a>sys.dm_pdw_sys_info (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  Fornece um conjunto de contadores de nível de dispositivo que refletem a atividade geral no dispositivo.  
  
|Nome da coluna|Tipo de dados|Description|Intervalo|  
|-----------------|---------------|-----------------|-----------|  
|total_sessions|**int**|Número de sessões atualmente no sistema.|0 para max_active_sessions (veja abaixo).|  
|idle_sessions|**int**|Número de sessões ociosos no momento.||  
|active_requests|**int**|Número de solicitações ativas em execução no momento.||  
|queued_requests|**int**|Número de solicitações em fila no momento.||  
|active_loads|**int**|Número de cargas em execução no sistema.||  
|queued_loads|**int**|Número de cargas em fila aguardando execução.||  
|active_backups|**int**|Número de backups em execução no momento.||  
|active_restores|**int**|Número de restaurações de backup em execução no momento.||  
  
## <a name="see-also"></a>Consulte também  
 [SQL Data Warehouse e Parallel Data Warehouse exibições de gerenciamento dinâmico &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
