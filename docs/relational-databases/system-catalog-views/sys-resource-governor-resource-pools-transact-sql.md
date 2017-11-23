---
title: resource_governor_resource_pools (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 08/09/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.resource_governor_resource_pools
- resource_governor_resource_pools
- sys.resource_governor_resource_pools_TSQL
- resource_governor_resource_pools_TSQL
dev_langs: TSQL
helpviewer_keywords: sys.resource_governor_resource_pools catalog view
ms.assetid: 56793e9c-aa90-452e-88c6-d9b799239888
caps.latest.revision: "26"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 2b8c30e6f3298e73a61484ecf9488d71e17701f7
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="sysresourcegovernorresourcepools-transact-sql"></a>sys.resource_governor_resource_pools (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Retorna a configuração armazenada do pool de recursos no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Cada linha da exibição determina a configuração de um pool.  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|pool_id|**int**|ID exclusivo do pool de recursos. Não permite valor nulo.|  
|name|**sysname**|Nome do pool de recursos. Não permite valor nulo.|  
|min_cpu_percent|**int**|Média de largura de banda de CPU garantida para todas as solicitações no pool de recursos quando houver contenção de CPU. Não permite valor nulo.|  
|max_cpu_percent|**int**|Largura de banda de CPU máxima permitida para todas as solicitações no pool de recursos quando houver contenção de CPU. Não permite valor nulo.|  
|min_memory_percent|**int**|Quantidade garantida de memória para todas as solicitações no pool de recursos. Não é compartilhada com outros pools de recursos. Não permite valor nulo.|  
|max_memory_percent|**int**|Porcentagem de memória total de servidor que pode ser usada por solicitações nesse pool de recursos. Não permite valor nulo. O efetivo máximo depende dos mínimos de pools. Por exemplo, max_memory_percent pode ser definido como 100, mas o máximo efetivo é inferior.|  
|cap_cpu_percent|**int**|**Aplica-se a**: do [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> Extremidade rígida na largura de banda de CPU que todas as solicitações no pool de recursos receberão. Limita a largura de banda de CPU máxima ao nível especificado. O intervalo permitido para o valor é de 1 a 100.|  
|min_iops_per_volume|**int**|**Aplica-se a**: do [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> A configuração das operações de E/S por segundo (IOPS) mínimas por volume deste pool. 0 = sem reserva. Não pode ser nulo.|  
|max_iops_per_volume|**int**|**Aplica-se a**: do [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> A configuração das operações de E/S por segundo (IOPS) máximas por volume deste pool. 0 = ilimitado. Não pode ser nulo.|  
  
## <a name="remarks"></a>Comentários  
 A exibição do catálogo exibe os metadados armazenados. Para verificar a configuração na memória, use a exibição de gerenciamento dinâmico correspondente, [sys.DM resource_governor_resource_pools &#40; Transact-SQL &#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-resource-pools-transact-sql.md).  
  
## <a name="permissions"></a>Permissões  
 Requer a permissão VIEW ANY DEFINITION para exibir conteúdo e a permissão CONTROL SERVER para alterar conteúdo.  
  
## <a name="see-also"></a>Consulte também  
 [Exibições de catálogo do administrador de recursos &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/resource-governor-catalog-views-transact-sql.md)   
 [sys.DM resource_governor_resource_pools &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-resource-pools-transact-sql.md)   
 [Administrador de Recursos](../../relational-databases/resource-governor/resource-governor.md)   
 [sys. resource_governor_external_resource_pools &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-resource-governor-external-resource-pools-transact-sql.md)  
  
  
