---
description: Tabelas de eventos estendidas – trace_xe_event_map
title: trace_xe_event_map (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- trace_xe_event_map_TSQL
- trace_xe_event_map
dev_langs:
- TSQL
helpviewer_keywords:
- trace_xe_event_map
- extended events [SQL Server], tables
ms.assetid: 537aa292-3540-47e8-be28-56dc01abc343
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 2e5a00eee3eb03b469f53fef18bb0512b8e2f32d
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89545754"
---
# <a name="extended-events-tables---trace_xe_event_map"></a>Tabelas de eventos estendidas – trace_xe_event_map
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Contém uma linha para cada evento Eventos Estendidos mapeado para uma classe de evento do Rastreamento do SQL. Essa tabela é armazenada no banco de dados mestre, no esquema sys.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|trace_event_id|**smallint**|A ID da coluna da classe de evento do Rastreamento do SQL que está sendo mapeada.|  
|package_name|**nvarchar(60)**|O nome do pacote de Eventos Estendidos onde o evento mapeado reside.|  
|xe_event_name|**nvarchar(60)**|O nome do evento de Eventos Estendidos que é mapeado para a classe de evento de Rastreamento do SQL.|  
  
## <a name="remarks"></a>Comentários  
 Você pode usar a consulta a seguir para identificar os eventos de Eventos Estendidos que são equivalentes às classes de evento de Rastreamento do SQL:  
  
```  
SELECT te.name, xe.package_name, xe.xe_event_name  
FROM sys.trace_events AS te  
LEFT JOIN sys.trace_xe_event_map AS xe  
   ON te.trace_event_id = xe.trace_event_id  
WHERE xe.trace_event_id IS NOT NULL  
```  
  
 Nem todas as classes de evento têm eventos de Eventos Estendidos equivalentes. Você pode usar a seguinte consulta para listar as classes de evento que não têm um equivalente a Eventos Estendidos:  
  
```  
SELECT te.trace_event_id, te.name  
FROM sys.trace_events AS te  
LEFT JOIN sys.trace_xe_event_map AS xe  
   ON te.trace_event_id = xe.trace_event_id  
WHERE xe.trace_event_id IS NULL  
```  
  
 Na consulta anterior, a maioria das classes de evento retornadas está relacionada à auditoria. Nós recomendamos que você use a Auditoria do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para auditar. A Auditoria do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usa Eventos Estendidos para ajudar a criar uma auditoria. Para obter mais informações, veja [Auditoria do SQL Server &#40;Mecanismo de Banco de Dados&#41;](../../relational-databases/security/auditing/sql-server-audit-database-engine.md).  
  
## <a name="see-also"></a>Consulte Também  
 [trace_xe_action_map &#40;Transact-SQL&#41;](../../relational-databases/system-tables/extended-events-tables-trace-xe-action-map.md)  
  
  
