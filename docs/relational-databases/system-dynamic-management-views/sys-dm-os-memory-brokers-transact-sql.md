---
title: sys.DM os_memory_brokers (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/18/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.dm_os_memory_brokers
- dm_os_memory_brokers_TSQL
- sys.dm_os_memory_brokers_TSQL
- dm_os_memory_brokers
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_os_memory_brokers dynamic management view
ms.assetid: 48dd6ad9-0d36-4370-8a12-4921d0df4b86
caps.latest.revision: 20
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: c0d32ef0b368c0e3c5a0de1cbb9c0a2f60110050
ms.sourcegitcommit: 7019ac41524bdf783ea2c129c17b54581951b515
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/23/2018
ms.locfileid: "34466322"
---
# <a name="sysdmosmemorybrokers-transact-sql"></a>sys.dm_os_memory_brokers (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  As alocações internas ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usam o gerenciador de memória do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Controle da diferença entre contadores de memória do processo do **sys.DM os_process_memory** e contadores internos pode indicar uso de memória de componentes externos a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] espaço de memória.  
  
 Os agentes de memória distribuem alocações de memória razoavelmente entre vários componentes no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], com base no uso projetado e atual. Eles não executam alocações. Só controlam alocações para computar a distribuição.  
  
 A tabela a seguir fornece informações sobre agentes de memória.  
  
> [!NOTE]  
>  Para chamar essa de [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] ou [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], use o nome **sys.dm_pdw_nodes_os_memory_brokers**.  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**pool_id**|**Int**|ID do pool de recursos caso seja associado a um pool do Administrador de recursos.|  
|**memory_broker_type**|**nvarchar(60)**|Tipo de agente de memória. Há três tipos de agentes de memória no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], listados abaixo e suas descrições.<br /><br /> **MEMORYBROKER_FOR_CACHE** : memória alocada para uso por objetos armazenados em cache.<br /><br /> **MEMORYBROKER_FOR_STEAL** : memória usada do pool de buffers. Essa memória não estará disponível para reutilização por outros componentes até ser liberada pelo proprietário atual.<br /><br /> **MEMORYBROKER_FOR_RESERVE** : memória reservada para uso futuro por solicitações atualmente em execução.|  
|**allocations_kb**|**bigint**|Quantidade de memória, em quilobytes (KB), alocada a este tipo de agente.|  
|**allocations_kb_per_sec**|**bigint**|Taxa de alocações de memória em quilobytes (KB) por segundo. Esse valor pode ser negativo para desalocações de memória.|  
|**predicted_allocations_kb**|**bigint**|Quantidade prevista de memória alocada pelo agente. Tem como base o padrão de uso da memória.|  
|**target_allocations_kb**|**bigint**|Quantidade recomendada de memória alocada, em quilobytes (KB), com base nas configurações atuais e no padrão de uso da memória. Esse agente deve aumentar ou diminuir em relação a esse número.|  
|**future_allocations_kb**|**bigint**|Número projetado de alocações, em quilobytes (KB), que serão feitas nos próximos segundos.|  
|**overall_limit_kb**|**bigint**|Quantidade máxima de memória, em quilobytes (KB), que o agente pode alocar.|  
|**last_notification**|**nvarchar(60)**|Recomendação de uso de memória com base nas configurações atuais e no padrão de uso. Estes são os valores válidos:<br /><br /> grow<br /><br /> shrink<br /><br /> stable|  
|**pdw_node_id**|**Int**|**Aplica-se a**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)], [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> O identificador para o nó que essa distribuição é no.|  
  
## <a name="permissions"></a>Permissões  

Em [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], requer `VIEW SERVER STATE` permissão.   
Em [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)], requer o `VIEW DATABASE STATE` no banco de dados.   
  
## <a name="see-also"></a>Consulte também  

  [Sistema operacional SQL Server relacionadas exibições de gerenciamento dinâmico &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)  
  
  


