---
title: sys. availability_databases_cluster (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.availability_databases_cluster_TSQL
- sys.availability_databases_cluster
- availability_databases_cluster_TSQL
- availability_databases_cluster
dev_langs:
- TSQL
helpviewer_keywords:
- Availability Groups [SQL Server], monitoring
- Availability Groups [SQL Server], WSFC clusters
- sys.availability_databases_cluster catalog view
- Availability Groups [SQL Server], databases
ms.assetid: 8d9c57e5-7f39-4315-b466-92748231140a
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: c520cf9e836f8db051599ed00735763c85632aab
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85649123"
---
# <a name="sysavailability_databases_cluster-transact-sql"></a>sys.availability_databases_cluster (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Contém uma linha para cada banco de dados de disponibilidade na instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que está hospedando uma réplica de disponibilidade para qualquer Always on grupo de disponibilidade no Cluster WSFC (Windows Server failover clustering), independentemente de o banco de dados de cópia local ter sido ingressado no grupo de disponibilidade ainda.  
  
> [!NOTE]  
>  Quando um banco de dados é adicionado a um grupo de disponibilidade, o banco de dados primário é unido automaticamente ao grupo. Os bancos de dados secundários deve estar preparados em cada réplica secundária para poderem ser unidos ao grupo de disponibilidade.   
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**group_id**|**uniqueidentifier**|Identificador exclusivo do grupo de disponibilidade, se houver, do qual o banco de dados está participando.<br /><br /> NULL = o banco de dados não faz parte de uma réplica de disponibilidade em um grupo de disponibilidade.|  
|**group_database_id**|**uniqueidentifier**|Identificador exclusivo do banco de dados no grupo de disponibilidade, se houver, do qual o banco de dados está participando. **group_database_id** é o mesmo para esse banco de dados na réplica primária e em todas as réplicas secundárias nas quais o banco de dados foi ingressado no grupo de disponibilidade.<br /><br /> NULL = o banco de dados não faz parte de uma réplica de disponibilidade em nenhum grupo de disponibilidade.|  
|**database_name**|**sysname**|O nome do banco de dados que foi adicionado ao grupo de disponibilidade.|  
  
## <a name="permissions"></a>Permissões  
 Se o chamador de **Sys. availability_databases_cluster** não for o proprietário do banco de dados, as permissões mínimas necessárias para ver a linha correspondente são a permissão ALTER ANY DATABASE ou VIEW ANY DATABASE no nível do servidor ou a permissão CREATE DATABASE no banco de dados **mestre** .  
  
## <a name="see-also"></a>Consulte Também  
 [sys.availability_groups &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-availability-groups-transact-sql.md)   
 [sys.databases &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)   
 [sys. dm_hadr_database_replica_states &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-hadr-database-replica-states-transact-sql.md)   
 [sys. dm_hadr_database_replica_cluster_states &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-hadr-database-replica-cluster-states-transact-sql.md)   
 [Visão geral de Always On grupos de disponibilidade &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)  
  
  
