---
title: sys.dm_pdw_diag_processing_stats (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: df659c55-4f63-45f8-8afe-ce300031bc5b
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>= aps-pdw-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: f1e2180e6d22cee81c94d880eca1debaa20c8c5d
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47837184"
---
# <a name="sysdmpdwdiagprocessingstats-transact-sql"></a>sys.dm_pdw_diag_processing_stats (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md.md)]

  Exibe informações relacionadas a todos os eventos de diagnóstico internos que podem ser incorporados em sessões de diagnóstico definidas pelo administrador. Consulte essa exibição para entender as estatísticas por trás do diagnóstico e os subsistemas de eventos que a população de todos os outros DMVs de unidade. Há um grupo de filas para cada processo em cada nó.  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**pdw_node_id**|**int**|Esse log é de um nó de dispositivo.|  
|**process_id**|**int**|Identificador do processo em execução enviando essa estatística.|  
|**target_name**|**nvarchar(255)**|O nome da fila.|  
|**queue_size**|**int**|O número de itens na fila de processo. O tamanho da fila geralmente é 0. Um número positivo indica que o sistema está sob carga excessiva e está criando a lista de pendências de eventos. Uma contagem positiva nas outras colunas significa que o sistema se tornaram corrompido para essa fila particular e todos os DMVs relacionados.|  
|**lost_events_count**|**bigint**|O número de eventos perdidos.|  
  
## <a name="see-also"></a>Consulte também  
 [SQL Data Warehouse e Parallel Data Warehouse exibições de gerenciamento dinâmico &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
