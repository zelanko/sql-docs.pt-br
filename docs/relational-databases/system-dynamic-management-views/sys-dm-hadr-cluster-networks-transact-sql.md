---
description: sys.dm_hadr_cluster_networks (Transact-SQL)
title: sys. dm_hadr_cluster_networks (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
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
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 832ade6b7e10eaa2a8bbcddfbdcc685ff7664f96
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89546537"
---
# <a name="sysdm_hadr_cluster_networks-transact-sql"></a>sys.dm_hadr_cluster_networks (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Retorna uma linha para cada membro do cluster do WSFC que está participando da configuração da sub-rede de um grupo de disponibilidade. Você pode usar essa exibição de gerenciamento dinâmico para validar o IP virtual de rede configurado para cada réplica de disponibilidade.  
  
 Chave primária: **member_name**  +  **network_subnet_IP**  +  **network_subnet_prefix_length**  
  
 > [!TIP]
 > A partir do [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] , essa exibição de gerenciamento dinâmico dá suporte a Always on instâncias de cluster de failover, além de Always on grupos de disponibilidade.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**member_name**|**nvarchar(128)**|Um nome de computador de um nó no cluster do WSFC.|  
|**network_subnet_ip**|**nvarchar (48)**|Endereço IP de rede da sub-rede à qual o computador pertence. Esse pode ser um endereço IPv4 ou IPv6.|  
|**network_subnet_ipv4_mask**|**nvarchar (45)**|Máscara de sub-rede da rede que especifica a sub-rede à qual o endereço IP pertence. **network_subnet_ipv4_mask** para especificar o <DHCP network_subnet_option opções de> em uma cláusula WITH DHCP da instrução [Create Availability Group](../../t-sql/statements/create-availability-group-transact-sql.md) ou [ALTER Availability Group](../../t-sql/statements/alter-availability-group-transact-sql.md) [!INCLUDE[tsql](../../includes/tsql-md.md)] .<br /><br /> NULL = Sub-rede IPv6.|  
||||  
|**network_subnet_prefix_length**|**int**|Comprimento do prefixo IP de rede que especifica a sub-rede à qual o computador pertence.|  
|**is_public**|**bit**|Se a rede é privada ou pública no cluster do WSFC, um dos seguintes:<br /><br /> 0 = Privada<br /><br /> 1 = Pública|  
|**is_ipv4**|**bit**|Tipo da sub-rede, um dos seguintes:<br /><br /> 1 = IPv4<br /><br /> 0 = IPv6|  
  
## <a name="security"></a>Segurança  
  
### <a name="permissions"></a>Permissões  
 , é necessário ter permissão VIEW SERVER STATE no servidor.  
  
## <a name="see-also"></a>Consulte Também  
 [Clustering de failover e Grupos de Disponibilidade AlwaysOn &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/failover-clustering-and-always-on-availability-groups-sql-server.md)   
 [Monitorar grupos de disponibilidade &#40;&#41;Transact-SQL ](../../database-engine/availability-groups/windows/monitor-availability-groups-transact-sql.md)   
 [sys. dm_os_cluster_nodes &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-cluster-nodes-transact-sql.md)   
 [Consultando as perguntas frequentes sobre o catálogo do sistema SQL Server](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)   
 [Exibições de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
