---
title: sys.dm_resource_governor_external_resource_pool_affinity (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 11/13/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_resource_governor_external_resource_pool_affinity
- sys.dm_resource_governor_external_resource_pool_affinity_TSQL
- dm_resource_governor_external_resource_pool_affinity
- dm_resource_governor_external_resource_pool_affinity_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_resource_governor_external_resource_pool_affinity
- dm_resource_governor_external_resource_pool_affinity
ms.assetid: e32fac49-5161-47c0-8540-af3fe730c00c
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 77d0d322139be1f1c6086622855600a7c24fc4c9
ms.sourcegitcommit: 68583d986ff5539fed73eacb7b2586a71c37b1fa
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/04/2020
ms.locfileid: "80664317"
---
# <a name="sysdm_resource_governor_external_resource_pool_affinity-transact-sql"></a>sys.dm_resource_governor_external_resource_pool_affinity (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]
**Aplica-se a:** [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] [!INCLUDE[rsql-productname-md](../../includes/rsql-productname-md.md)] e [!INCLUDE[sssql17-md](../../includes/sssql17-md.md)] [!INCLUDE[rsql-productnamenew-md](../../includes/rsql-productnamenew-md.md)]

Retorna informações de afinidade da CPU sobre a configuração atual do pool de recursos externos.
  
|Nome da coluna|Tipo de dados|Descrição|
|----------------|---------------|-----------------|
|pool_id|**Int**|O ID do pool de recursos externos. Não permite valor nulo.|
|processor_group|**Smallint**|A ID do grupo de processadores lógicos do Windows. Não permite valor nulo.|
|cpu_mask|**Bigint**|A máscara binária representando as CPUs associadas a este pool. Não permite valor nulo.|
  
## <a name="remarks"></a>Comentários

Piscinas que são criadas `AUTO` com uma afinidade de não aparecem nesta visão porque não têm afinidade. Para obter mais informações, consulte o [CREATE EXTERNAL RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-resource-pool-transact-sql.md) e ALTER EXTERNAL RESOURCE POOL &#40;[Demonstrações de&#41;Transact-SQL.](../../t-sql/statements/alter-external-resource-pool-transact-sql.md)

## <a name="permissions"></a>Permissões

Requer a permissão `VIEW SERVER STATE`.

## <a name="see-also"></a>Confira também

[Governança de recursos para o aprendizado de máquina no SQL Server](../../machine-learning/administration/resource-governor.md)

[sys.dm_resource_governor_resource_pool_affinity &#40;&#41;Transact-SQL](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-resource-pool-affinity-transact-sql.md)

[Opção external scripts enabled de configuração de servidor](../../database-engine/configure-windows/external-scripts-enabled-server-configuration-option.md)

[ALTER EXTERNAL RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/alter-external-resource-pool-transact-sql.md)
