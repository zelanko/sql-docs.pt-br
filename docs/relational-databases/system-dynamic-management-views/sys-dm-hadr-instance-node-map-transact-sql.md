---
title: sys.dm_hadr_instance_node_map (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.sys.dm_hadr_instance_node_map_TSQL
- sys.sys.dm_hadr_instance_node_map
- sys.dm_hadr_instance_node_map_TSQL
- sys.dm_hadr_instance_node_map
dev_langs:
- TSQL
helpviewer_keywords:
- Availability Groups [SQL Server], monitoring
- Availability Groups [SQL Server], WSFC
- sys.sys.dm_hadr_instance_node_map dynamic management view
ms.assetid: ccfaf62c-9f87-43cf-a5e7-8942e91dd041
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: c3e0b022996ab5b0f6de91773871fc7357c29e7f
ms.sourcegitcommit: 2827d19393c8060eafac18db3155a9bd230df423
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/27/2019
ms.locfileid: "58511383"
---
# <a name="sysdmhadrinstancenodemap-transact-sql"></a>sys.dm_hadr_instance_node_map (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Para cada instância de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que hospeda uma réplica de disponibilidade que é unida a seu grupo de disponibilidade Always On, retorna o nome do nó de Cluster de Failover do servidor (WSFC) do Windows que hospeda a instância do servidor. Esta exibição de gerenciamento dinâmico tem os seguintes usos:  
  
-   Esta exibição de gerenciamento dinâmico será útil para detectar um grupo de disponibilidade com várias réplicas de disponibilidade que são hospedadas no mesmo nó do WSFC, que é uma configuração sem suporte que poderá ocorrer depois de um failover de FCI se o grupo de disponibilidade estiver configurado incorretamente. Para obter mais informações, veja [Clustering de failover e Grupos de Disponibilidade AlwaysOn &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/failover-clustering-and-always-on-availability-groups-sql-server.md).  
  
-   Quando várias instâncias do SQL Server são hospedadas no mesmo nó do WSFC, a DLL de Recurso usa esta exibição de gerenciamento dinâmico para determinar a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] à qual se conectar.  
   
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**ag_resource_id**|**nvarchar(256)**|ID exclusiva do grupo de disponibilidade como um recurso do WSFC.|  
|**instance_name**|**nvarchar(256)**|Nome -*server*/*instância*-de uma instância de servidor que hospeda uma réplica para o grupo de disponibilidade.|  
|**node_name**|**nvarchar(256)**|Nome do nó WSFC.|  
  
## <a name="permissions"></a>Permissões  
 , é necessário ter permissão VIEW SERVER STATE no servidor.  
  
## <a name="see-also"></a>Consulte também  
 [Funções e exibições de gerenciamento dinâmico de Grupos de Disponibilidade AlwaysOn &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/always-on-availability-groups-dynamic-management-views-functions.md)   
 [Exibições de catálogo de grupos de disponibilidade AlwaysOn &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/always-on-availability-groups-catalog-views-transact-sql.md)   
 [Monitorar grupos de disponibilidade &#40;Transact-SQL&#41;](../../database-engine/availability-groups/windows/monitor-availability-groups-transact-sql.md)   
 [Grupos de Disponibilidade AlwaysOn &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/always-on-availability-groups-sql-server.md)  
  
  
