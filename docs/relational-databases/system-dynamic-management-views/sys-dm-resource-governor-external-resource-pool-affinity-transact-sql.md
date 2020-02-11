---
title: sys. dm_resource_governor_external_resource_pool_affinity (Transact-SQL) | Microsoft Docs
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
ms.openlocfilehash: 02ec95d318825c1759067455b62f3dae6a86c184
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68053331"
---
# <a name="sysdm_resource_governor_external_resource_pool_affinity-transact-sql"></a>sys. dm_resource_governor_external_resource_pool_affinity (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]
**Aplica-se a:** [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] [!INCLUDE[rsql-productname-md](../../includes/rsql-productname-md.md)] e [!INCLUDE[sssql17-md](../../includes/sssql17-md.md)] [!INCLUDE[rsql-productnamenew-md](../../includes/rsql-productnamenew-md.md)]

Retorna informações de afinidade de CPU sobre a configuração atual do pool de recursos externos.
  
|Nome da coluna|Tipo de dados|DESCRIÇÃO|
|----------------|---------------|-----------------|
|pool_id|**int**|A ID do pool de recursos externos. Não permite valor nulo.|
|processor_group|**smallint**|A ID do grupo de processadores lógicos do Windows. Não permite valor nulo.|
|cpu_mask|**bigint**|A máscara binária que representa as CPUs associadas a este pool. Não permite valor nulo.|
  
## <a name="remarks"></a>Comentários

Os pools criados com uma afinidade de não `AUTO` aparecem nesse modo de exibição porque não têm afinidade. Para obter mais informações, consulte [criar pool de recursos externos &#40;Transact-sql&#41;](../../t-sql/statements/create-external-resource-pool-transact-sql.md) e [alterar o pool de recursos externos &#40;instruções transact-SQL&#41;](../../t-sql/statements/alter-external-resource-pool-transact-sql.md) .

## <a name="permissions"></a>Permissões

Requer a permissão `VIEW SERVER STATE`.

## <a name="see-also"></a>Confira também

[Governança de recursos para aprendizado de máquina no SQL Server](../../advanced-analytics/r/resource-governance-for-r-services.md)

[sys. dm_resource_governor_resource_pool_affinity &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-resource-pool-affinity-transact-sql.md)

[Opção de Configuração do servidor external scripts enabled](../../database-engine/configure-windows/external-scripts-enabled-server-configuration-option.md)

[ALTER EXTERNAL RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/alter-external-resource-pool-transact-sql.md)
