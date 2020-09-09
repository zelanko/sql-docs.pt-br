---
description: sys.dm_resource_governor_resource_pool_affinity (Transact-SQL)
title: sys. dm_resource_governor_resource_pool_affinity (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_resource_governor_resource_pool_affinity_TSQL
- sys.dm_resource_governor_resource_pool_affinity
- dm_resource_governor_resource_pool_affinity
- dm_resource_governor_resource_pool_affinity_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- dm_resource_governor_resource_pool_affinity
- sys.dm_resource_governor_resource_pool_affinity
ms.assetid: a197ec19-a2ba-44f5-a4f2-3eee33ebd77d
author: markingmyname
ms.author: maghan
ms.openlocfilehash: c304b552dfbf09786af4c7d61edc64c99b004adc
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89546519"
---
# <a name="sysdm_resource_governor_resource_pool_affinity-transact-sql"></a>sys.dm_resource_governor_resource_pool_affinity (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Acompanha a afinidade do pool de recursos.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md).  
  
|Nome do Colmn|Tipo de dados|Descrição|  
|----------------|---------------|-----------------|  
|Pool_id|**int**|ID do pool de recursos. Não permite valor nulo.|  
|Processor_group|**smallint**|A ID do grupo de processadores lógicos do Windows. Não permite valor nulo.|  
|Scheduler_mask|**bigint**|A máscara binária que representa os agendadores associados a esse pool. Não permite valor nulo.|  
  
## <a name="remarks"></a>Comentários  
 Pools criados com uma afinidade de AUTO não aparecerão nessa exibição, pois eles não têm nenhuma afinidade. Para obter mais informações, consulte [Create Resource pool &#40;Transact-sql&#41;](../../t-sql/statements/create-resource-pool-transact-sql.md) e [ALTER RESOURCE pool &#40;instruções transact-SQL&#41;](../../t-sql/statements/alter-resource-pool-transact-sql.md) .  
  
## <a name="see-also"></a>Consulte Também  
 [sys.dm_resource_governor_external_resource_pool_affinity &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-external-resource-pool-affinity-transact-sql.md)  
  
  
