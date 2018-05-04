---
title: sys.DM hadr_cluster_networks (Transact-SQL) | Microsoft Docs
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
- dm_hadr_cluster_networks
- sys.dm_hadr_cluster_networks_TSQL
- sys.dm_hadr_cluster_networks
- dm_hadr_cluster_networks_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- Availability Groups [SQL Server], monitoring
- Availability Groups [SQL Server], WSFC clusters
- sys.dm_hadr_cluster_networks dynamic management view
ms.assetid: ece32b15-d63f-4f93-92b7-e2930333e97a
caps.latest.revision: 15
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 97a4574761c83377b72e38cee385abd23ebc4c11
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="sysdmhadrclusternetworks-transact-sql"></a>sys.dm_hadr_cluster_networks (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Retorna uma linha para cada membro do cluster do WSFC que está participando da configuração da sub-rede de um grupo de disponibilidade. Você pode usar essa exibição de gerenciamento dinâmico para validar o IP virtual de rede configurado para cada réplica de disponibilidade.  
  
 Chave primária: **member_name** + **network_subnet_IP** + **network_subnet_prefix_length**  
  
 > [!TIP]
 > A partir do [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)], essa exibição de gerenciamento dinâmico oferece suporte a Failover Cluster instâncias AlwaysOn além dos grupos de disponibilidade AlwaysOn.  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**member_name**|**nvarchar(128)**|Um nome de computador de um nó no cluster do WSFC.|  
|**network_subnet_ip**|**nvarchar(48)**|Endereço IP de rede da sub-rede à qual o computador pertence. Esse pode ser um endereço IPv4 ou IPv6.|  
|**network_subnet_ipv4_mask**|**nvarchar(45)**|Máscara de sub-rede da rede que especifica a sub-rede à qual o endereço IP pertence. **network_subnet_ipv4_mask** para especificar as opções de DHCP < network_subnet_option > em uma cláusula WITH DHCP do [criar grupo de disponibilidade](../../t-sql/statements/create-availability-group-transact-sql.md) ou [ALTER AVAILABILITY GROUP](../../t-sql/statements/alter-availability-group-transact-sql.md) [!INCLUDE[tsql](../../includes/tsql-md.md)] instrução.<br /><br /> NULL = Sub-rede IPv6.|  
||||  
|**network_subnet_prefix_length**|**Int**|Comprimento do prefixo IP de rede que especifica a sub-rede à qual o computador pertence.|  
|**is_public**|**bit**|Se a rede é privada ou pública no cluster do WSFC, um dos seguintes:<br /><br /> 0 = Privada<br /><br /> 1 = Pública|  
|**is_ipv4**|**bit**|Tipo da sub-rede, um dos seguintes:<br /><br /> 1 = IPv4<br /><br /> 0 = IPv6|  
  
## <a name="security"></a>Segurança  
  
### <a name="permissions"></a>Permissões  
 , é necessário ter permissão VIEW SERVER STATE no servidor.  
  
## <a name="see-also"></a>Consulte também  
 [Clustering de failover e Grupos de Disponibilidade AlwaysOn &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/failover-clustering-and-always-on-availability-groups-sql-server.md)   
 [Monitorar grupos de disponibilidade & #40; Transact-SQL & #41;](../../database-engine/availability-groups/windows/monitor-availability-groups-transact-sql.md)   
 [sys.dm_os_cluster_nodes &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-cluster-nodes-transact-sql.md)   
 [Consultando o catálogo de sistema do SQL Server perguntas Frequentes](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)   
 [Exibições de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
