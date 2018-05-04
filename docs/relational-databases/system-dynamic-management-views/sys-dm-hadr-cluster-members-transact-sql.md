---
title: sys.DM hadr_cluster_members (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/23/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
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
caps.latest.revision: 23
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 8cfb014bdd78bf410215ecbdf1bf343a2f0018a8
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="sysdmhadrclustermembers-transact-sql"></a>sys.dm_hadr_cluster_members (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  Se o nó WSFC que hospeda uma instância local do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que está habilitada para [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] tiver quorum de WSFC, retornará uma linha para cada um dos membros que constituem o quorum e o estado de cada um deles. Isso inclui todos os nós do cluster (retornados com o tipo CLUSTER_ENUM_NODE o **Clusterenum** função) e a testemunha de disco ou compartilhamento de arquivos, se houver. A linha retornada para um determinado membro contém informações sobre o estado daquele membro. Por exemplo, para um cluster de cinco nós com quorum da maioria do nó em que um nó estiver inativo, quando **sys.DM hadr_cluster_members** é consultado em uma instância de servidor que está habilitado para [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] que reside em um nó com quorum, **sys.DM hadr_cluster_members** reflete o estado do nó inativo como "NODE_DOWN".  
  
 Se o nó WSFC não tiver nenhum quorum, nenhuma linha será retornada.  
  
 Use essa exibição de gerenciamento dinâmico pode responder às seguintes perguntas:  
  
-   Quais nós estão sendo executados no cluster WSFC atualmente?  
  
-   Quantas falhas mais o cluster WSFC pode tolerar antes de perder o quorum em um caso de maioria de nós?  

 > [!TIP]
 > A partir do [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)], essa exibição de gerenciamento dinâmico oferece suporte a Failover Cluster instâncias AlwaysOn além dos grupos de disponibilidade AlwaysOn.  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**member_name**|**nvarchar(128)**|Nome do membro, que pode ser um nome de computador, uma letra de unidade ou um caminho de compartilhamento de arquivos.|  
|**member_type**|**tinyint**|O tipo do membro, um dos seguintes:<br /><br /> 0 = Nó WSFC<br /><br /> 1 = Testemunha de disco<br /><br /> 2 = Testemunha de compartilhamento de arquivos|  
|**member_type_desc**|**nvarchar(50)**|Descrição do **member_type**, um de:<br /><br /> CLUSTER_NODE<br /><br /> DISK_WITNESS<br /><br /> FILE_SHARE_WITNESS|  
|**member_state**|**tinyint**|O estado do membro, um dos seguintes:<br /><br /> 0 = Offline<br /><br /> 1 = Online|  
|**member_state_desc**|**nvarchar(60)**|Descrição do **member_state**, um de:<br /><br /> UP<br /><br /> PARA BAIXO|  
|**number_of_quorum_votes**|**tinyint**|Número de votos de quorum possuído por este membro de quorum. Para nenhuma maioria: quorums de somente disco, esse valor é padronizado como 0. Para outros tipos de quorum, este valor é padronizado como 1.|  
  
## <a name="permissions"></a>Permissões  
 , é necessário ter permissão VIEW SERVER STATE no servidor.  
  
## <a name="examples"></a>Exemplos  
  
## <a name="see-also"></a>Consulte também  
 [Funções e exibições de gerenciamento dinâmico de Grupos de Disponibilidade AlwaysOn &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/always-on-availability-groups-dynamic-management-views-functions.md)   
 [Exibições de catálogo de grupos de disponibilidade AlwaysOn &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/always-on-availability-groups-catalog-views-transact-sql.md)   
 [Monitorar grupos de disponibilidade & #40; Transact-SQL & #41;](../../database-engine/availability-groups/windows/monitor-availability-groups-transact-sql.md)   
 [Grupos de disponibilidade AlwaysOn & #40; SQL Server & #41;](../../database-engine/availability-groups/windows/always-on-availability-groups-sql-server.md)  
  
  
