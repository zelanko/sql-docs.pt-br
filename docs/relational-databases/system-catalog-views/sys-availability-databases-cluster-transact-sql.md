---
title: sys. availability_databases_cluster (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
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
caps.latest.revision: 14
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 5b0c0cd91b58c4e59cba2440d8f02cd01a93c870
ms.sourcegitcommit: 2d93cd115f52bf3eff3069f28ea866232b4f9f9e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/01/2018
ms.locfileid: "33179182"
---
# <a name="sysavailabilitydatabasescluster-transact-sql"></a>sys.availability_databases_cluster (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Contém uma linha para cada banco de dados de disponibilidade na instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que está hospedando uma réplica de disponibilidade para qualquer grupo de disponibilidade AlwaysOn do cluster do Windows Server Failover Clustering (WSFC), independentemente se o local copiar o banco de dados foi unido ao grupo de disponibilidade ainda.  
  
> [!NOTE]  
>  Quando um banco de dados é adicionado a um grupo de disponibilidade, o banco de dados primário é unido automaticamente ao grupo. Os bancos de dados secundários deve estar preparados em cada réplica secundária para poderem ser unidos ao grupo de disponibilidade.   
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**group_id**|**uniqueidentifier**|Identificador exclusivo do grupo de disponibilidade, se houver, do qual o banco de dados está participando.<br /><br /> NULL = o banco de dados não faz parte de uma réplica de disponibilidade em um grupo de disponibilidade.|  
|**group_database_id**|**uniqueidentifier**|Identificador exclusivo do banco de dados no grupo de disponibilidade, se houver, do qual o banco de dados está participando. **group_database_id** é o mesmo para este banco de dados na réplica primária e em cada réplica secundária na qual o banco de dados foi unido ao grupo de disponibilidade.<br /><br /> NULL = o banco de dados não faz parte de uma réplica de disponibilidade em nenhum grupo de disponibilidade.|  
|**database_name**|**sysname**|O nome do banco de dados que foi adicionado ao grupo de disponibilidade.|  
  
## <a name="permissions"></a>Permissões  
 Se o chamador de **sys. availability_databases_cluster** não é o proprietário do banco de dados, as permissões mínimas necessárias para ver a linha correspondente serão ALTER ANY DATABASE ou permissão de nível de servidor de qualquer modo de exibição de banco de dados ou criar Permissão de banco de dados no **mestre** banco de dados.  
  
## <a name="see-also"></a>Consulte também  
 [sys.availability_groups &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-availability-groups-transact-sql.md)   
 [sys.databases &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)   
 [sys.dm_hadr_database_replica_states &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-hadr-database-replica-states-transact-sql.md)   
 [sys.dm_hadr_database_replica_cluster_states &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-hadr-database-replica-cluster-states-transact-sql.md)   
 [Visão geral dos grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)  
  
  
