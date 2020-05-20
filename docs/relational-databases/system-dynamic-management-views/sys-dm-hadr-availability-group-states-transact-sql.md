---
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
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: bace0824a7c8411e267186c3e9919ba2eb4be15c
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/05/2020
ms.locfileid: "82811971"
---
# <a name="sysdm_hadr_availability_group_states-transact-sql"></a>sys.dm_hadr_availability_group_states (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

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
 [Monitorar grupos de disponibilidade &#40;&#41;Transact-SQL](../../database-engine/availability-groups/windows/monitor-availability-groups-transact-sql.md)   
 [Always On grupos de disponibilidade &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/always-on-availability-groups-sql-server.md)   
 [Funções e exibições de gerenciamento dinâmico de Grupos de Disponibilidade AlwaysOn &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/always-on-availability-groups-dynamic-management-views-functions.md)  
  
  
