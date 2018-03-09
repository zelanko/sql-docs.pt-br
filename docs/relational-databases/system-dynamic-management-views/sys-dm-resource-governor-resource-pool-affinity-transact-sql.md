---
title: sys.dm_resource_governor_resource_pool_affinity (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 08/09/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: dmv's
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 83c425a7346e58b4332ee4c8e78b4fe607b9ca6a
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/03/2018
---
# <a name="sysdmresourcegovernorresourcepoolaffinity-transact-sql"></a>sys.dm_resource_governor_resource_pool_affinity (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Acompanha a afinidade do pool de recursos.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "ícone de link do tópico") [convenções de sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md).  
  
|Nome de Colmn|Tipo de dados|Description|  
|----------------|---------------|-----------------|  
|Pool_id|**Int**|ID do pool de recursos. Não permite valor nulo.|  
|Processor_group|**smallint**|A ID do grupo de processadores lógicos do Windows. Não permite valor nulo.|  
|Scheduler_mask|**bigint**|A máscara binária que representa os agendadores associados a esse pool. Não permite valor nulo.|  
  
## <a name="remarks"></a>Remarks  
 Pools criados com uma afinidade de AUTO não aparecerão nessa exibição, pois eles não têm nenhuma afinidade. Para obter mais informações, consulte o [CREATE RESOURCE POOL &#40; Transact-SQL &#41; ](../../t-sql/statements/create-resource-pool-transact-sql.md) e [ALTER RESOURCE POOL &#40; Transact-SQL &#41; ](../../t-sql/statements/alter-resource-pool-transact-sql.md) instruções.  
  
## <a name="see-also"></a>Consulte também  
 [sys.dm_resource_governor_external_resource_pool_affinity &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-external-resource-pool-affinity-transact-sql.md)  
  
  
