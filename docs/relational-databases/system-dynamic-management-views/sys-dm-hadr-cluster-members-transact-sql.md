---
title: sys. dm_hadr_cluster_members (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/31/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_hadr_cluster_members_TSQL
- sys.dm_hadr_cluster_members
- dm_hadr_cluster_members_TSQL
- dm_hadr_cluster_members
dev_langs:
- TSQL
helpviewer_keywords:
- Availability Groups [SQL Server], monitoring
- Availability Groups [SQL Server], WSFC clusters
- sys.dm_hadr_cluster_members catalog view
ms.assetid: feb20b3a-8835-41d3-9a1c-91d3117bc170
author: CarlRabeler
ms.author: carlrab
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 3ec0ed5aa4ddedd7e3fcfd544d53a270eb9e3372
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85790458"
---
# <a name="sysdm_hadr_cluster_members-transact-sql"></a>sys.dm_hadr_cluster_members (Transact-SQL)
[!INCLUDE [SQL Server Azure SQL Database ](../../includes/applies-to-version/sql-asdb.md)]

  Se o nó WSFC que hospeda uma instância local do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que está habilitada para [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] tiver quorum de WSFC, retornará uma linha para cada um dos membros que constituem o quorum e o estado de cada um deles. Isso inclui todos os nós no cluster (retornados com CLUSTER_ENUM_NODE tipo pela função **ClusterEnum** ) e o disco ou a testemunha de compartilhamento de arquivos, se houver. A linha retornada para um determinado membro contém informações sobre o estado daquele membro. Por exemplo, para um cluster de cinco nós com quorum de nó principal no qual um nó está inoperante, quando **Sys. dm_hadr_cluster_members** é consultado de uma instância de servidor que está habilitada para [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] o que reside em um nó com quorum, **Sys. dm_hadr_cluster_members** reflete o estado do nó para baixo como "NODE_DOWN".  
  
 Se o nó WSFC não tiver nenhum quorum, nenhuma linha será retornada.  
  
 Use essa exibição de gerenciamento dinâmico pode responder às seguintes perguntas:  
  
-   Quais nós estão sendo executados no cluster WSFC atualmente?  
  
-   Quantas falhas mais o cluster WSFC pode tolerar antes de perder o quorum em um caso de maioria de nós?  

 > [!TIP]
 > A partir do [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] , essa exibição de gerenciamento dinâmico dá suporte a Always on instâncias de cluster de failover, além de Always on grupos de disponibilidade.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**member_name**|**nvarchar(128)**|Nome do membro, que pode ser um nome de computador, uma letra de unidade ou um caminho de compartilhamento de arquivos.|  
|**member_type**|**tinyint**|O tipo do membro, um dos seguintes:<br /><br /> 0 = Nó WSFC<br /><br /> 1 = Testemunha de disco<br /><br /> 2 = Testemunha de compartilhamento de arquivos<br /><br /> 3 = testemunha em nuvem|  
|**member_type_desc**|**nvarchar(50)**|Descrição de **MEMBER_TYPE**, uma das:<br /><br /> CLUSTER_NODE<br /><br /> DISK_WITNESS<br /><br /> FILE_SHARE_WITNESS<br /><br /> CLOUD_WITNESS|  
|**member_state**|**tinyint**|O estado do membro, um dos seguintes:<br /><br /> 0 = Offline<br /><br /> 1 = Online|  
|**member_state_desc**|**nvarchar(60)**|Descrição de **member_state**, uma das:<br /><br /> UP<br /><br /> PARA BAIXO|  
|**number_of_quorum_votes**|**tinyint**|Número de votos de quorum possuído por este membro de quorum. Para nenhuma maioria: quorums de somente disco, esse valor é padronizado como 0. Para outros tipos de quorum, este valor é padronizado como 1.|  
  
## <a name="permissions"></a>Permissões  
 , é necessário ter permissão VIEW SERVER STATE no servidor.  
  
## <a name="examples"></a>Exemplos  
  
## <a name="see-also"></a>Consulte Também  
 [Always On funções e exibições de gerenciamento dinâmico de grupos de disponibilidade &#40;&#41;de Transact-SQL](../../relational-databases/system-dynamic-management-views/always-on-availability-groups-dynamic-management-views-functions.md)   
 [Always On exibições de catálogo de grupos de disponibilidade &#40;&#41;Transact-SQL](../../relational-databases/system-catalog-views/always-on-availability-groups-catalog-views-transact-sql.md)   
 [Monitorar grupos de disponibilidade &#40;&#41;Transact-SQL](../../database-engine/availability-groups/windows/monitor-availability-groups-transact-sql.md)   
 [Grupos de Disponibilidade AlwaysOn &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/always-on-availability-groups-sql-server.md)  
  
  
