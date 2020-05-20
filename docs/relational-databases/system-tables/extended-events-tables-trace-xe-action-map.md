---
title: trace_xe_action_map (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- trace_xe_action_map_TSQL
- trace_xe_action_map
dev_langs:
- TSQL
helpviewer_keywords:
- extended events [SQL Server], tables
- trace_xe_action_map
ms.assetid: 208a1413-ce7f-4521-b765-d74723627302
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 77497b56d5f889c698ce5b27088032bb96b7135a
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/05/2020
ms.locfileid: "82806186"
---
# <a name="extended-events-tables---trace_xe_action_map"></a>Tabelas de eventos estendidas – trace_xe_action_map
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Contém uma linha para cada ação de Eventos Estendidos que é mapeada para uma ID de coluna do Rastreamento do SQL. Essa tabela é armazenada no banco de dados mestre, no esquema sys.  
  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|trace_column_id|**smallint**|A ID da coluna do Rastreamento do SQL que está sendo mapeada.|  
|package_name|**nvarchar(60)**|O nome do pacote de Eventos Estendidos onde a ação mapeada reside.|  
|xe_action_name|**nvarchar(60)**|O nome da ação de Eventos Estendidos que é mapeada para a coluna de Rastreamento do SQL.|  
  
## <a name="remarks"></a>Comentários  
 Você pode usar a consulta a seguir para identificar as ações de Eventos Estendidos que são equivalentes às colunas de Rastreamento do SQL:  
  
```  
SELECT tc.name AS trace_column, am.package_name, am.xe_action_name  
FROM sys.trace_columns AS tc  
INNER JOIN sys.trace_xe_action_map AS am  
   ON tc.trace_column_id = am.trace_column_id  
```  
  
 Não são incluídas colunas de Rastreamento do SQL que não são mapeadas para ações na tabela.  
  
## <a name="see-also"></a>Consulte Também  
 [trace_xe_event_map &#40;Transact-SQL&#41;](../../relational-databases/system-tables/extended-events-tables-trace-xe-event-map.md)  
  
  
