---
title: sys. resource_governor_external_resource_pools (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 11/13/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.resource_governor_external_resource_pools
- sys.resource_governor_external_resource_pools_TSQL
- resource_governor_external_resource_pools
- resource_governor_external_resource_pools_TSQL
helpviewer_keywords:
- sys.resource_governor_external_resource_pools
- resource_governor_external_resource_pools
ms.assetid: 75063e36-a91b-496f-9936-88f3d57bd447
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 4d9b7a733acaf5f6136f6746b313c30c03f63683
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/05/2020
ms.locfileid: "82834087"
---
# <a name="sysresource_governor_external_resource_pools-transact-sql"></a>sys. resource_governor_external_resource_pools (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]
**Aplica-se a:** [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] [!INCLUDE[rsql-productname-md](../../includes/rsql-productname-md.md)]e [!INCLUDE[sssql17-md](../../includes/sssql17-md.md)][!INCLUDE[rsql-productnamenew-md](../../includes/rsql-productnamenew-md.md)]

Retorna a configuração do pool de recursos externos armazenado no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Cada linha da exibição determina a configuração de um pool.
  
|Nome da coluna|Tipo de dados|Descrição|
|-----------------|---------------|-----------------|
|external_pool_id|**int**|ID exclusivo do pool de recursos. Não permite valor nulo.|
|Nome|**sysname**|Nome do pool de recursos. Não permite valor nulo.|
|max_cpu_percent|**int**|Largura de banda de CPU máxima permitida para todas as solicitações no pool de recursos quando houver contenção de CPU. Não permite valor nulo.|
|max_memory_percent|**int**|Porcentagem de memória total de servidor que pode ser usada por solicitações nesse pool de recursos. Não permite valor nulo. O efetivo máximo depende dos mínimos de pools. Por exemplo, max_memory_percent pode ser definido como 100, mas o máximo efetivo é inferior.|
|max_processes|**int**|Número máximo de processos externos simultâneos. O valor padrão, 0, não especifica nenhum limite. Não permite valor nulo.|
|version|**bigint**|Número de versão interno.|
  
## <a name="permissions"></a>Permissões

Requer a permissão VIEW SERVER STAT.

## <a name="see-also"></a>Confira também

[Governança de recursos para o aprendizado de máquina no SQL Server](../../machine-learning/administration/resource-governor.md)

[Resource Governor exibições de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/resource-governor-catalog-views-transact-sql.md)

[sys.dm_resource_governor_resource_pools &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-resource-pools-transact-sql.md)

[Resource Governor](../../relational-databases/resource-governor/resource-governor.md)

[sys. dm_resource_governor_resource_pool_affinity &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-resource-pool-affinity-transact-sql.md)

[Opção de Configuração do servidor external scripts enabled](../../database-engine/configure-windows/external-scripts-enabled-server-configuration-option.md)

[ALTER EXTERNAL RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/alter-external-resource-pool-transact-sql.md)
