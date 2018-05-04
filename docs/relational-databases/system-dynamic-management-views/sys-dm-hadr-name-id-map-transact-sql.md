---
title: sys.DM hadr_name_id_map (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.dm_hadr_name_id_map
- sys.dm_hadr_name_id_map_TSQL
- dm_hadr_name_id_map
- dm_hadr_name_id_map_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- Availability Groups [SQL Server], monitoring
- sys.dm_hadr_name_id_map dynamic management view
ms.assetid: e07bb8a9-37de-4a39-a257-950d7c3ae8fb
caps.latest.revision: 8
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 69b1fd2e09b4f7c13540928328e4d5ca0697a530
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="sysdmhadrnameidmap-transact-sql"></a>sys.dm_hadr_name_id_map (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Mostra o mapeamento de grupos de disponibilidade sempre que a instância atual do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ingressou para três IDs exclusivas: uma disponibilidade ID do grupo, uma ID de recurso do WSFC e uma ID de grupo do WSFC. O objetivo desse mapeamento é manipular o cenário no qual o recurso/grupo WSFC é renomeado.  
   
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**ag_name**|**nvarchar(256)**|O nome do grupo de disponibilidade. Este é um nome de usuário especificado deve ser exclusivo dentro do cluster do Windows Server Failover Cluster (WSFC).|  
|**ag_id**|**uniqueidentifier**|GUID (identificador exclusivo) do grupo de disponibilidade.|  
|**ag_resource_id**|**nvarchar(256)**|ID exclusivo do grupo de disponibilidade como um recurso no cluster WSFC.|  
|**ag_group_id**|**nvarchar(256)**|ID do Grupo WSFC exclusivo do grupo de disponibilidade.|  
  
## <a name="permissions"></a>Permissões  
 , é necessário ter permissão VIEW SERVER STATE no servidor.  
  
## <a name="see-also"></a>Consulte também  
 [Funções e exibições de gerenciamento dinâmico de Grupos de Disponibilidade AlwaysOn &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/always-on-availability-groups-dynamic-management-views-functions.md)   
 [Exibições de catálogo de grupos de disponibilidade AlwaysOn &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/always-on-availability-groups-catalog-views-transact-sql.md)   
 [Monitorar grupos de disponibilidade & #40; Transact-SQL & #41;](../../database-engine/availability-groups/windows/monitor-availability-groups-transact-sql.md)   
 [Grupos de Disponibilidade AlwaysOn &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/always-on-availability-groups-sql-server.md)  
  
  
