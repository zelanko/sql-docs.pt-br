---
description: sys.dm_hadr_availability_group_states (Transact-SQL)
title: sys. dm_hadr_availability_group_states (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_hadr_availability_group_states
- sys.dm_hadr_availability_group_states_TSQL
- dm_hadr_availability_group_states_TSQL
- dm_hadr_availability_group_states
dev_langs:
- TSQL
helpviewer_keywords:
- Availability Groups [SQL Server], monitoring
- sys.dm_hadr_availability_group_states dynamic management view
ms.assetid: d18019dd-f8dc-4492-b035-b1a639369b65
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 0ca065be60cbe6514d1da606501ff90f72ac1c69
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89543894"
---
# <a name="sysdm_hadr_availability_group_states-transact-sql"></a>sys.dm_hadr_availability_group_states (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Retorna uma linha para cada grupo de disponibilidade Always On que possui uma réplica de disponibilidade na instância local do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Cada linha exibe os estados que definem a integridade de um determinado grupo de disponibilidade.  
  
> [!NOTE]  
>  Para obter a lista completa de, consulte a exibição do catálogo [Sys. availability_groups](../../relational-databases/system-catalog-views/sys-availability-groups-transact-sql.md) .  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**group_id**|**uniqueidentifier**|Identificador exclusivo do grupo de disponibilidade.|  
|**primary_replica**|**varchar(128)**|O nome da instância do servidor que está hospedando a réplica primária atual.<br /><br /> NULL = Não é a réplica primária ou não pode se comunicar com o cluster de failover do WSFC.|  
|**primary_recovery_health**|**tinyint**|Indica a integridade da recuperação da réplica primária, um dos seguintes:<br /><br /> 0 = em andamento<br /><br /> 1 = Online<br /><br /> NULO<br /><br /> Em réplicas secundárias, a coluna **primary_recovery_health** é nula.|  
|**primary_recovery_health_desc**|**nvarchar(60)**|Descrição de **primary_replica_health**, uma das:<br /><br /> ONLINE_IN_PROGRESS<br /><br /> ONLINE<br /><br /> NULO|  
|**secondary_recovery_health**|**tinyint**|Indica a integridade de recuperação de uma réplica de réplica secundária, uma das:<br /><br /> 0 = em andamento<br /><br /> 1 = Online<br /><br /> NULO<br /><br /> Na réplica primária, a coluna **secondary_recovery_health** é nula.|  
|**secondary_recovery_health_desc**|**nvarchar(60)**|Descrição de **secondary_recovery_health**, uma das:<br /><br /> ONLINE_IN_PROGRESS<br /><br /> ONLINE<br /><br /> NULO|  
|**synchronization_health**|**tinyint**|Reflete um ROLLUP do **synchronization_health** de todas as réplicas de disponibilidade no grupo de disponibilidade. Abaixo estão os possíveis valores e suas descrições.<br /><br /> 0: não íntegro. Nenhuma das réplicas de disponibilidade tem um **synchronization_health** íntegro (2 = íntegro).<br /><br /> 1: parcialmente íntegro. Há integridade de sincronização de algumas, mas não todas, as réplicas de disponibilidade.<br /><br /> 2: íntegro. Há integridade de sincronização de todas as réplicas de disponibilidade.<br /><br /> Para obter informações sobre a integridade da sincronização de réplica, consulte a coluna **synchronization_health** em [sys. dm_hadr_availability_replica_states &#40;&#41;do Transact-SQL ](../../relational-databases/system-dynamic-management-views/sys-dm-hadr-availability-replica-states-transact-sql.md).|  
|**synchronization_health_desc**|**nvarchar(60)**|Descrição de **synchronization_health**, uma das:<br /><br /> NOT_HEALTHY<br /><br /> PARTIALLY_HEALTHY<br /><br /> HEALTHY|  
  
## <a name="security"></a>Segurança  
  
### <a name="permissions"></a>Permissões  
 , é necessário ter permissão VIEW SERVER STATE no servidor.  
  
## <a name="see-also"></a>Consulte Também  
 [Monitorar grupos de disponibilidade &#40;&#41;Transact-SQL ](../../database-engine/availability-groups/windows/monitor-availability-groups-transact-sql.md)   
 [Grupos de Disponibilidade AlwaysOn &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/always-on-availability-groups-sql-server.md)   
 [Funções e exibições de gerenciamento dinâmico de Grupos de Disponibilidade AlwaysOn &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/always-on-availability-groups-dynamic-management-views-functions.md)  
  
  
