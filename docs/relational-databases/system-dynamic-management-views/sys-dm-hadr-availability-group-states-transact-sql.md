---
title: sys.dm_hadr_availability_group_states (Transact-SQL) | Microsoft Docs
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
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: b06ffc7a8400d3b02698009b2452282658cf959e
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47745354"
---
# <a name="sysdmhadravailabilitygroupstates-transact-sql"></a>sys.dm_hadr_availability_group_states (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Retorna uma linha para cada sempre no grupo de disponibilidade que possui uma réplica de disponibilidade na instância local do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Cada linha exibe os estados que definem a integridade de um determinado grupo de disponibilidade.  
  
> [!NOTE]  
>  Para obter a lista completa de, consulte o [sys. availability_groups](../../relational-databases/system-catalog-views/sys-availability-groups-transact-sql.md) exibição do catálogo.  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**group_id**|**uniqueidentifier**|Identificador exclusivo do grupo de disponibilidade.|  
|**primary_replica**|**varchar(128)**|O nome da instância do servidor que está hospedando a réplica primária atual.<br /><br /> NULL = Não é a réplica primária ou não pode se comunicar com o cluster de failover do WSFC.|  
|**primary_recovery_health**|**tinyint**|Indica a integridade da recuperação da réplica primária, um dos seguintes:<br /><br /> 0 = em andamento<br /><br /> 1 = Online<br /><br /> NULL<br /><br /> Em réplicas secundárias a **primary_recovery_health** coluna será NULL.|  
|**primary_recovery_health_desc**|**nvarchar(60)**|Descrição da **primary_replica_health**, um de:<br /><br /> ONLINE_IN_PROGRESS<br /><br /> ONLINE<br /><br /> NULL|  
|**secondary_recovery_health**|**tinyint**|Indica a integridade da recuperação de uma réplica secundária, um dos:<br /><br /> 0 = em andamento<br /><br /> 1 = Online<br /><br /> NULL<br /><br /> Na réplica primária, o **secondary_recovery_health** coluna será NULL.|  
|**secondary_recovery_health_desc**|**nvarchar(60)**|Descrição da **secondary_recovery_health**, um de:<br /><br /> ONLINE_IN_PROGRESS<br /><br /> ONLINE<br /><br /> NULL|  
|**synchronization_health**|**tinyint**|Reflete um rollup do **synchronization_health** de todas as réplicas de disponibilidade no grupo de disponibilidade. Abaixo estão os valores possíveis e suas descrições.<br /><br /> 0: não está íntegro. Nenhuma das réplicas de disponibilidade tem um íntegra **synchronization_health** (2 = HEALTHY).<br /><br /> 1: parcialmente íntegro. Há integridade de sincronização de algumas, mas não todas, as réplicas de disponibilidade.<br /><br /> 2: íntegro. Há integridade de sincronização de todas as réplicas de disponibilidade.<br /><br /> Para obter informações sobre a integridade de sincronização de réplica, consulte o **synchronization_health** coluna em [sys.dm_hadr_availability_replica_states &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-hadr-availability-replica-states-transact-sql.md).|  
|**synchronization_health_desc**|**nvarchar(60)**|Descrição da **synchronization_health**, um de:<br /><br /> NOT_HEALTHY<br /><br /> PARTIALLY_HEALTHY<br /><br /> HEALTHY|  
  
## <a name="security"></a>Segurança  
  
### <a name="permissions"></a>Permissões  
 , é necessário ter permissão VIEW SERVER STATE no servidor.  
  
## <a name="see-also"></a>Consulte também  
 [Monitorar grupos de disponibilidade &#40;Transact-SQL&#41;](../../database-engine/availability-groups/windows/monitor-availability-groups-transact-sql.md)   
 [Grupos de Disponibilidade AlwaysOn &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/always-on-availability-groups-sql-server.md)   
 [Grupos de disponibilidade Always On, funções e exibições de gerenciamento dinâmico &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/always-on-availability-groups-dynamic-management-views-functions.md)  
  
  
