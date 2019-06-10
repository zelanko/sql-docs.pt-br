---
title: Referência de objeto do sistema de grupo de disponibilidade Always On | Microsoft Docs
ms.custom: ''
ms.date: 04/03/2010
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
author: MashaMSFT
ms.author: mathoma
manager: jroth
monikerRange: '>=sql-server-2014||=sqlallproducts-allversions'
ms.openlocfilehash: 8eff161c24275ee86938bf5d57bbe39473ac19cc
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/07/2019
ms.locfileid: "66800162"
---
# <a name="always-on-availability-group-system-object-reference"></a>Referência de objeto do sistema de grupo de disponibilidade Always On

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]
    
Este tópico serve como uma página de referência para todos os vários objetos do sistema que podem ser usados ao trabalhar com grupos de disponibilidade Always On. 

## <a name="system-catalog-views"></a>Exibições de catálogo do sistema

| Exibição de catálogo do sistema | Descrição|
| :------ | :----------------------------- |
| [sys.availability_databases_cluster](../../../relational-databases/system-catalog-views/sys-availability-databases-cluster-transact-sql.md)   | Contém uma linha para cada banco de dados de disponibilidade na instância do SQL Server que está hospedando uma réplica de disponibilidade para qualquer grupo de disponibilidade Always On no cluster do WSFC (Windows Server Failover Clustering), independentemente de se o banco de dados de cópia local foi unido ao grupo de disponibilidade. |
| [sys.availability_group_listener_ip_addresses](../../../relational-databases/system-catalog-views/sys-availability-group-listener-ip-addresses-transact-sql.md)  | Retorna uma linha para cada endereço IP associado a qualquer ouvinte de grupo de disponibilidade Always On no cluster do WSFC (Windows Server Failover Clustering). |
| [sys.availability_group_listeners](../../../relational-databases/system-catalog-views/sys-availability-group-listeners-transact-sql.md)    | Para cada grupo de disponibilidade Always On, retorna zero linhas indicando que nenhum nome de rede está associado ao grupo de disponibilidade ou retorna uma linha para cada configuração de ouvinte de grupo de disponibilidade no cluster do WSFC (Windows Server Failover Clustering).  |
| [sys.availability_groups](../../../relational-databases/system-catalog-views/sys-availability-groups-transact-sql.md)   | Retorna uma linha para cada grupo de disponibilidade para o qual a instância local do SQL Server hospeda uma réplica de disponibilidade. Cada linha contém uma cópia armazenada em cache dos metadados do grupo de disponibilidade. |
| [sys.availability_groups_cluster](../../../relational-databases/system-catalog-views/sys-availability-groups-cluster-transact-sql.md)    | Retorna uma linha para cada grupo de disponibilidade Always On no WSFC (Windows Server Failover Clustering). Cada linha contém os metadados do grupo de disponibilidade do cluster do WSFC. |
| [sys.availability_read_only_routing_lists](../../../relational-databases/system-catalog-views/sys-availability-read-only-routing-lists-transact-sql.md)    | Retorna uma linha para a lista de roteamento somente leitura de cada réplica de disponibilidade em um grupo de disponibilidade AlwaysOn do cluster de failover WSFC. |
| [sys.availability_replicas](../../../relational-databases/system-catalog-views/sys-availability-replicas-transact-sql.md)    | Retorna uma linha para cada uma das réplicas de disponibilidade que pertence a um grupo de disponibilidade Always On no cluster de failover WSFC. |
| &nbsp; | &nbsp; |

## <a name="system-dynamic-management-views"></a>Exibições de gerenciamento dinâmico do sistema


| Exibição de gerenciamento dinâmico do sistema | Descrição|
| :------ | :----------------------------- |
| [sys.dm_hadr_auto_page_repair](../../../relational-databases/system-dynamic-management-views/sys-dm-hadr-auto-page-repair-transact-sql.md)   | Retorna uma linha para cada tentativa de reparo automático de página em qualquer banco de dados de disponibilidade em uma réplica de disponibilidade hospedada para qualquer grupo de disponibilidade pela instância do servidor.  |
| [sys.dm_hadr_availability_group_states](../../../relational-databases/system-dynamic-management-views/sys-dm-hadr-availability-group-states-transact-sql.md)    | Retorna uma linha para cada grupo de disponibilidade Always On que possui uma réplica de disponibilidade na instância local do SQL Server. Cada linha exibe os estados que definem a integridade de um determinado grupo de disponibilidade. |
| [sys.dm_hadr_availability_replica_cluster_nodes](../../../relational-databases/system-dynamic-management-views/sys-dm-hadr-availability-replica-cluster-nodes-transact-sql.md)     | Retorna uma linha para cada réplica de disponibilidade (independentemente do estado de junção) dos grupos de disponibilidade Always On no cluster WSFC (Windows Server Failover Clustering) |
| [sys.dm_hadr_availability_replica_cluster_states](../../../relational-databases/system-dynamic-management-views/sys-dm-hadr-availability-replica-cluster-states-transact-sql.md)     | Retorna uma linha para cada réplica de disponibilidade Always On (independentemente de seu estado de junção) de todos os grupos de disponibilidade Always On (independentemente do local da réplica) no cluster do WSFC (Windows Server Failover Clustering). |
| [sys.dm_hadr_availability_replica_states](../../../relational-databases/system-dynamic-management-views/sys-dm-hadr-availability-replica-states-transact-sql.md)    | Retorna uma linha para cada réplica local e uma linha para cada réplica remota no mesmo grupo de disponibilidade Always On que uma réplica local. Cada linha contém informações sobre o estado de uma determinada réplica. |
| [sys.dm_hadr_cluster](../../../relational-databases/system-dynamic-management-views/sys-dm-hadr-cluster-transact-sql.md)    | Retorna uma linha que expõe o nome do cluster e as informações sobre o quorum |
| [sys.dm_hadr_cluster_members](../../../relational-databases/system-dynamic-management-views/sys-dm-hadr-cluster-members-transact-sql.md)    | Retorna uma linha para cada um dos membros que constituem o quorum e o estado de cada um deles |
| [sys.dm_hadr_cluster_networks](../../../relational-databases/system-dynamic-management-views/sys-dm-hadr-cluster-networks-transact-sql.md)    | Retorna uma linha para cada membro do cluster do WSFC que está participando da configuração da sub-rede de um grupo de disponibilidade.  |
| [sys.dm_hadr_database_replica_cluster_states](../../../relational-databases/system-dynamic-management-views/sys-dm-hadr-database-replica-cluster-states-transact-sql.md)     | Retorna uma linha que contém informações destinadas a fornecer uma visão da integridade dos bancos de dados de disponibilidade nos grupos de disponibilidade Always On em cada grupo de disponibilidade Always On no cluster do WSFC (Windows Server Failover Clustering).  |
| [sys.dm_hadr_database_replica_states](../../../relational-databases/system-dynamic-management-views/sys-dm-hadr-database-replica-states-transact-sql.md)    | Retorna uma linha para cada banco de dados que está participando de um grupo de disponibilidade Always On para o qual a instância local do SQL Server hospeda uma réplica de disponibilidade. |
| [sys.dm_hadr_instance_node_map](../../../relational-databases/system-dynamic-management-views/sys-dm-hadr-instance-node-map-transact-sql.md)    | Para cada instância do SQL Server que hospeda uma réplica de disponibilidade que é ingressada em seu grupo de disponibilidade Always On, é retornado o nome do nó do WSFC (Windows Server Failover Cluster) que hospeda a instância do servidor. |
| [sys.dm_hadr_name_id_map](../../../relational-databases/system-dynamic-management-views/sys-dm-hadr-name-id-map-transact-sql.md)    | Mostra o mapeamento de grupos de disponibilidade AlwaysOn nos quais a instância atual do SQL Server ingressou em três IDs exclusivas: uma ID de grupo de disponibilidade, uma ID de recurso do WSFC e uma ID de grupo do WSFC. |
| [sys.dm_tcp_listener_states](../../../relational-databases/system-dynamic-management-views/sys-dm-tcp-listener-states-transact-sql.md)    | Retorna uma linha que contém informações de estado dinâmico para cada ouvinte de TCP. |
| &nbsp; | &nbsp; |

## <a name="system-functions"></a>Funções do sistema


| Função do sistema | Descrição|
| :------ | :----------------------------- |
| [sys.fn_hadr_is_primary_replica](../../../relational-databases/system-functions/sys-fn-hadr-is-primary-replica-transact-sql.md)  | Usado para determinar se a réplica atual for a réplica primária. |
| [sys.fn_hadr_backup_is_preferred_replica](../../../relational-databases/system-functions/sys-fn-hadr-backup-is-preferred-replica-transact-sql.md)    | Usado para determinar se a réplica atual for a réplica de backup preferencial. |
| [sys.fn_hadr_distributed_ag_replica](../../../relational-databases/system-functions/sys-fn-hadr-distributed-ag-replica-transact-sql.md)    | Usado para mapear uma réplica em um grupo de disponibilidade distribuído para o grupo de disponibilidade local. |
| &nbsp; | &nbsp; |


  
## <a name="see-also"></a>Consulte Também  
 [Visão geral dos grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   

  
