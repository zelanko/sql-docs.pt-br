---
description: sys.dm_hadr_name_id_map (Transact-SQL)
title: sys. dm_hadr_name_id_map (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
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
author: markingmyname
ms.author: maghan
ms.openlocfilehash: cdd98f7eaa120814a8f615738cc0cee284b60269
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89532898"
---
# <a name="sysdm_hadr_name_id_map-transact-sql"></a>sys.dm_hadr_name_id_map (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Mostra o mapeamento de grupos de disponibilidade Always On que a instância atual do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ingressou em três IDs exclusivas: uma ID de grupo de disponibilidade, uma ID de recurso do WSFC e uma ID de grupo do WSFC. O objetivo desse mapeamento é manipular o cenário no qual o recurso/grupo WSFC é renomeado.  
   
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**ag_name**|**nvarchar(256)**|O nome do grupo de disponibilidade. Esse é um nome especificado pelo usuário que deve ser exclusivo no Cluster WSFC (cluster de failover do Windows Server).|  
|**ag_id**|**uniqueidentifier**|GUID (identificador exclusivo) do grupo de disponibilidade.|  
|**ag_resource_id**|**nvarchar(256)**|ID exclusivo do grupo de disponibilidade como um recurso no cluster WSFC.|  
|**ag_group_id**|**nvarchar(256)**|ID do Grupo WSFC exclusivo do grupo de disponibilidade.|  
  
## <a name="permissions"></a>Permissões  
 , é necessário ter permissão VIEW SERVER STATE no servidor.  
  
## <a name="see-also"></a>Consulte Também  
 [Always On funções e exibições de gerenciamento dinâmico de grupos de disponibilidade &#40;&#41;de Transact-SQL ](../../relational-databases/system-dynamic-management-views/always-on-availability-groups-dynamic-management-views-functions.md)   
 [Exibições de catálogo de grupos de disponibilidade AlwaysOn &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/always-on-availability-groups-catalog-views-transact-sql.md)   
 [Monitorar grupos de disponibilidade &#40;&#41;Transact-SQL ](../../database-engine/availability-groups/windows/monitor-availability-groups-transact-sql.md)   
 [Grupos de Disponibilidade AlwaysOn &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/always-on-availability-groups-sql-server.md)  
  
  
