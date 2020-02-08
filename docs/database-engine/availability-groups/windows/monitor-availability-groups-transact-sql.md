---
title: Monitorar grupos de disponibilidade usando o T-SQL (Transact-SQL)
description: Uma descrição de como monitorar Grupos de Disponibilidade AlwaysOn usando o T-SQL (Transact-SQL).
ms.custom: seodec18
ms.date: 05/17/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- Availability Groups [SQL Server], monitoring
- dynamic management views [SQL Server], AlwaysOn Availability Groups
- Availability Groups [SQL Server], availability replicas
- Availability Groups [SQL Server], listeners
- Availability Groups [SQL Server], databases
- catalog views [SQL Server], AlwaysOn Availability Groups
ms.assetid: 881a34de-8461-4811-8c62-322bf7226bed
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 6a95082cd732b644105c14c4ba598f859f48456e
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/01/2020
ms.locfileid: "68014697"
---
# <a name="monitor-availability-groups-transact-sql"></a>Monitorar grupos de disponibilidade (Transact-SQL)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Para monitorar os grupos de disponibilidade e as réplicas e os bancos de dados associados usando o [!INCLUDE[tsql](../../../includes/tsql-md.md)], o [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] fornece um conjunto de exibições do catálogo e de gerenciamento dinâmico e propriedades de servidor. Usando as instruções SELECT [!INCLUDE[tsql](../../../includes/tsql-md.md)] , é possível usar as exibições para monitorar grupos de disponibilidade e suas réplicas e bancos de dados. As informações retornadas a um determinado grupo de disponibilidade dependem de se você está conectado à instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] que está hospedando a réplica primária ou uma réplica secundária.  
  
> [!TIP]  
>  Muitas dessas exibições podem ser unidas usando suas colunas de ID para retornar informações de várias exibições em uma única consulta.  
  
  
##  <a name="Permissions"></a> Permissões  
 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] exigem a permissão VIEW ANY DEFINITION na instância do servidor. [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] exigem a permissão VIEW SERVER STATE no servidor.  
  
##  <a name="AoAgFeatureOnSI"></a> Monitorando o recurso Grupos de Disponibilidade AlwaysOn em uma instância de servidor  
 Para monitorar o recurso [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] em uma instância de servidor, use a seguinte função interna:  
  
 função[SERVERPROPERTY](../../../t-sql/functions/serverproperty-transact-sql.md)  
 Retorna informações de propriedade de servidor sobre se o [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] está habilitado e, nesse caso, se ele está iniciado na instância de servidor.  
  
 **Nomes de coluna:** IsHadrEnabled, HadrManagerStatus  
  
##  <a name="WSFC"></a> Monitorando grupos de disponibilidade no cluster do WSFC  
 Para monitorar o WSFC (Windows Server Failover Clustering) que hospeda uma instância do servidor local habilitada para [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)], use as exibições a seguir:  
  
 [sys.dm_hadr_cluster](../../../relational-databases/system-dynamic-management-views/sys-dm-hadr-cluster-transact-sql.md)  
 Se o nó do WSFC (Windows Server Failover Clustering) que hospeda uma instância do SQL Server com [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] habilitado tiver quorum do WSFC, **sys.dm_hadr_cluster** retornará uma linha que expõe o nome do cluster e informações sobre o quorum. Se o nó WSFC não tiver nenhum quorum, nenhuma linha será retornada.  
  
 **Nomes de colunas:** cluster_name, quorum_type, quorum_type_desc, quorum_state, quorum_state_desc  
  
 [sys.dm_hadr_cluster_members](../../../relational-databases/system-dynamic-management-views/sys-dm-hadr-cluster-members-transact-sql.md)  
 Se o nó do WSFC que hospeda a instância habilitada para AlwaysOn do SQL Server tiver quorum do WSFC, será retornada uma linha para cada um dos membros que constituem o quorum e o estado de cada um deles.  
  
 **Nomes de colunas:** member_name, member_type, member_type_desc, member_state, member_state_desc, number_of_quorum_votes  
  
 [sys.dm_hadr_cluster_networks](../../../relational-databases/system-dynamic-management-views/sys-dm-hadr-cluster-networks-transact-sql.md)  
 Retorna uma linha para cada membro que está participando da configuração de sub-rede de um grupo de disponibilidade. Você pode usar essa exibição de gerenciamento dinâmico para validar o IP virtual de rede configurado para cada réplica de disponibilidade.  
  
 **Nomes de colunas:** member_name, network_subnet_ip, network_subnet_ipv4_mask, network_subnet_prefix_length, is_public, is_ipv4  
  
 **Chave primária:** nome_membro + sub-rede_rede_IP + tamanho_prefixo_sub-rede_rede  
  
 [sys.dm_hadr_instance_node_map](../../../relational-databases/system-dynamic-management-views/sys-dm-hadr-instance-node-map-transact-sql.md)  
 Para cada instância do SQL Server que hospeda uma réplica de disponibilidade que é ingressada em seu grupo de disponibilidade AlwaysOn, é retornado o nome do nó do WSFC (Windows Server Failover Clustering) que hospeda a instância do servidor. Esta exibição de gerenciamento dinâmico tem os seguintes usos:  
  
-   Esta exibição de gerenciamento dinâmico será útil para detectar um grupo de disponibilidade com várias réplicas de disponibilidade que são hospedadas no mesmo nó do WSFC, que é uma configuração sem suporte que poderá ocorrer depois de um failover de FCI se o grupo de disponibilidade estiver configurado incorretamente.  
  
-   Quando várias instâncias do SQL Server são hospedadas no mesmo nó do WSFC, a DLL de Recurso usa esta exibição de gerenciamento dinâmico para determinar a instância do SQL Server à qual se conectar.  
  
 **Nomes de colunas:** ag_resource_id, instance_name, node_name  
  
 [sys.dm_hadr_name_id_map](../../../relational-databases/system-dynamic-management-views/sys-dm-hadr-name-id-map-transact-sql.md)  
 Mostra o mapeamento de grupos de disponibilidade AlwaysOn nos quais a instância atual do SQL Server ingressou em três IDs exclusivas: uma ID de grupo de disponibilidade, uma ID de recurso do WSFC e uma ID de grupo do WSFC. O objetivo desse mapeamento é manipular o cenário no qual o recurso/grupo WSFC é renomeado.  
  
 **Nomes de colunas:** ag_name, ag_id, ag_resource_id, ag_group_id  
  
> [!NOTE]  
>  Veja também **sys.dm_hadr_availability_replica_cluster_nodes** e **sys.dm_hadr_availability_replica_cluster_states** na seção [Monitorando réplicas de disponibilidade](#AvReplicas) e **sys.availability_databases_cluster** e **sys.dm_hadr_database_replica_cluster_states** na seção [Monitorando bancos de dados de disponibilidade](#AvDbs), mais adiante neste tópico.  
  
 Para obter informações sobre os clusters WSFC e o [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)], veja [Windows Server Failover Clustering &#40;WSFC&#41; with SQL Server](../../../sql-server/failover-clusters/windows/windows-server-failover-clustering-wsfc-with-sql-server.md) e [Clustering de Failover e Grupos de Disponibilidade AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/failover-clustering-and-always-on-availability-groups-sql-server.md).  
  
##  <a name="AvGroups"></a> Monitorando grupos de disponibilidade  
 Para monitorar os grupos de disponibilidade para os quais a instância do servidor hospeda uma réplica de disponibilidade, use as exibições a seguir:  
  
 [sys.availability_groups](../../../relational-databases/system-catalog-views/sys-availability-groups-transact-sql.md)  
 Retorna uma linha para cada grupo de disponibilidade para o qual a instância local do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] hospeda uma réplica de disponibilidade. Cada linha contém uma cópia armazenada em cache dos metadados do grupo de disponibilidade.  
  
 **Nomes de colunas:** group_id, name, resource_id, resource_group_id, failure_condition_level, health_check_timeout, automated_backup_preference, automated_backup_preference_desc  
  
 [sys.availability_groups_cluster](../../../relational-databases/system-catalog-views/sys-availability-groups-cluster-transact-sql.md)  
 Retorna uma linha para cada grupo de disponibilidade no cluster do WSFC. Cada linha contém os metadados do grupo de disponibilidade do cluster do WSFC (Windows Server Failover Clustering).  
  
 **Nomes de colunas:** group_id, name, resource_id, resource_group_id, failure_condition_level, health_check_timeout, automated_backup_preference, automated_backup_preference_desc  
  
 [sys.dm_hadr_availability_group_states](../../../relational-databases/system-dynamic-management-views/sys-dm-hadr-availability-group-states-transact-sql.md)  
 Retorna uma linha para cada grupo de disponibilidade que possui uma réplica de disponibilidade na instância local do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Cada linha exibe os estados que definem a integridade de um determinado grupo de disponibilidade.  
  
 **Nomes de colunas:** group_id, primary_replica, primary_recovery_health, primary_recovery_health_desc, secondary_recovery_health, secondary_recovery_health_desc, synchronization_health, synchronization_health_desc  
  
##  <a name="AvReplicas"></a> Monitorando réplicas de disponibilidade  
 Para monitorar réplicas de disponibilidade, use as seguintes exibições e a função do sistema:  
  
 [sys.availability_replicas](../../../relational-databases/system-catalog-views/sys-availability-replicas-transact-sql.md)  
 Retorna uma linha para cada réplica de disponibilidade em cada grupo de disponibilidade para o qual a instância local do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] hospeda uma réplica de disponibilidade.  
  
 **Nomes de colunas:** replica_id, group_id, replica_metadata_id, replica_server_name, owner_sid, endpoint_url, availability_mode, availability_mode_desc, failover_mode, failover_mode_desc, session_timeout, primary_role_allow_connections, primary_role_allow_connections_desc, secondary_role_allow_connections, secondary_role_allow_connections_desc, create_date, modify_date, backup_priority, read_only_routing_url  
  
 [sys.availability_read_only_routing_lists](../../../relational-databases/system-catalog-views/sys-availability-read-only-routing-lists-transact-sql.md)  
 Retorna uma linha para a lista de roteamento somente leitura de cada réplica de disponibilidade em um grupo de disponibilidade AlwaysOn do cluster de failover WSFC.  
  
 **Nomes de colunas:** replica_id, routing_priority, read_only_replica_id  
  
 [sys.dm_hadr_availability_replica_cluster_nodes](../../../relational-databases/system-dynamic-management-views/sys-dm-hadr-availability-replica-cluster-nodes-transact-sql.md)  
 Retorna uma linha para cada réplica de disponibilidade (independentemente do estado de junção) dos grupos de disponibilidade AlwaysOn no cluster WSFC (Windows Server Failover Clustering).  
  
 **Nomes de colunas:** group_name, replica_server_name, node_name  
  
 [sys.dm_hadr_availability_replica_cluster_states](../../../relational-databases/system-dynamic-management-views/sys-dm-hadr-availability-replica-cluster-states-transact-sql.md)  
 Retorna uma linha para cada réplica (independentemente do estado de junção) de todos os grupos de disponibilidade AlwaysOn (independentemente da localização da réplica) no cluster WSFC (Windows Server Failover Clustering).  
  
 **Nomes de colunas:** replica_id, replica_server_name, group_id, join_state, join_state_desc  
  
 [sys.dm_hadr_availability_replica_states](../../../relational-databases/system-dynamic-management-views/sys-dm-hadr-availability-replica-states-transact-sql.md)  
 Retorna uma linha que mostra o estado de cada réplica de disponibilidade local e uma linha para cada réplica de disponibilidade remota no mesmo grupo de disponibilidade.  
  
 **Nomes de colunas:** replica_id, group_id, is_local, role, role_desc, operational_state, operational_state_desc, connected_state, connected_state_desc, recovery_health, recovery_health_desc, synchronization_health, synchronization_health_desc, last_connect_error_number, last_connect_error_description e last_connect_error_timestamp  
  
 [sys.fn_hadr_backup_is_preferred_replica](../../../relational-databases/system-functions/sys-fn-hadr-backup-is-preferred-replica-transact-sql.md)  
 Determina se a réplica atual é a réplica de backup preferencial.  
  
> [!NOTE]  
>  Para obter informações sobre contadores de desempenho para réplicas de disponibilidade (o objeto de desempenho **SQLServer:Availability Replica**  ), consulte [SQL Server, Réplica de Disponibilidade](../../../relational-databases/performance-monitor/sql-server-availability-replica.md).  
  
##  <a name="AvDbs"></a> Monitorando bancos de dados de disponibilidade  
 Para monitorar bancos de dados de disponibilidade, use as seguintes exibições:  
  
 [sys.availability_databases_cluster](../../../relational-databases/system-catalog-views/sys-availability-databases-cluster-transact-sql.md)  
 Contém uma linha para cada banco de dados na instância do SQL Server que faz parte de todos os Grupos de Disponibilidade AlwaysOn no cluster, independentemente de o banco de dados de cópia local já ter ingressado no grupo de disponibilidade.  
  
> [!NOTE]  
>  Quando um banco de dados é adicionado a um grupo de disponibilidade, o banco de dados primário é unido automaticamente ao grupo. Os bancos de dados secundários deve estar preparados em cada réplica secundária para poderem ser unidos ao grupo de disponibilidade.  
  
 **Nomes de colunas:** group_id, group_database_id, database_name  
  
 [sys.databases](../../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)  
 Contém uma linha por banco de dados na instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Se um banco de dados pertencer a uma réplica de disponibilidade, a linha daquele banco de dados exibirá o GUID da réplica e o identificador exclusivo do banco de dados dentro de seu grupo de disponibilidade.  
  
 **[!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] :** replica_id, group_database_id  
  
 [sys.dm_hadr_auto_page_repair](../../../relational-databases/system-dynamic-management-views/sys-dm-hadr-auto-page-repair-transact-sql.md)  
 Retorna uma linha para cada tentativa de reparo automático de página em qualquer banco de dados de disponibilidade em uma réplica de disponibilidade hospedada para qualquer grupo de disponibilidade pela instância do servidor. Essa exibição contém linhas das últimas tentativas de reparo automático de página em um determinado banco de dados primário ou secundário, com um máximo de 100 linhas por banco de dados. Assim que o banco de dados atinge o máximo, a linha de sua próxima tentativa de conserto de página automático substitui uma das entradas existentes.  
  
 **Nomes de colunas:** database_id, file_id, page_id, error_type, page_status, modification_time  
  
 [sys.dm_hadr_database_replica_states](../../../relational-databases/system-dynamic-management-views/sys-dm-hadr-database-replica-states-transact-sql.md)  
 Retorna uma linha para cada banco de dados que está participando de qualquer grupo de disponibilidade para o qual a instância local do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] hospeda uma réplica de disponibilidade.  
  
 **Nomes de colunas:** database_id, group_id, replica_id, group_database_id, is_local, synchronization_state, synchronization_state_desc, is_commit_participant, synchronization_health, synchronization_health_desc, database_state, database_state_desc, is_suspended, suspend_reason, suspend_reason_desc, recovery_lsn, truncation_lsn, last_sent_lsn, last_sent_time, last_received_lsn, last_received_time, last_hardened_lsn, last_hardened_time, last_redone_lsn, last_redone_time, log_send_queue_size, log_send_rate, redo_queue_size, redo_rate, filestream_send_rate, end_of_log_lsn, last_commit_lsn, last_commit_time, low_water_mark_for_ghosts  
  
 [sys.dm_hadr_database_replica_cluster_states](../../../relational-databases/system-dynamic-management-views/sys-dm-hadr-database-replica-cluster-states-transact-sql.md)  
 Retorna uma linha que contém informações destinadas a fornecer uma visão da integridade dos bancos de dados de disponibilidade em cada grupo de disponibilidade no cluster do WSFC (Windows Server Failover Clustering). Essa exibição de gerenciamento dinâmico é útil ao planejar ou responder a um failover ou para descobrir qual réplica secundária em um grupo de disponibilidade está mantendo truncamento de log em um determinado banco de dados primário.  
  
 **Nomes de colunas:** replica_id, group_database_id, database_name, is_failover_ready, is_pending_secondary_suspend, is_database_joined, recovery_lsn, truncation_lsn  
  
> [!NOTE]  
>  O local da réplica primária é a origem autoritativa de um grupo de disponibilidade.  
  
> [!NOTE]  
>  Para obter informações sobre contadores de desempenho do [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] para réplicas de disponibilidade (o objeto de desempenho **SQLServer:Réplica de Banco de Dados** ), veja [SQL Server, Réplica de Banco de Dados](../../../relational-databases/performance-monitor/sql-server-database-replica.md). Além disso, para monitorar a atividade de log de transações em bancos de dados de disponibilidade, use os seguintes contadores do objeto de desempenho **SQLServer:Databases**: **Tempo de Gravação de Liberação de Log (ms)** , **Liberações de Log/s**, **Perdas no Cache do Pool de Logs/s**, **Leituras de Disco do Pool de Logs/s** e **Solicitações do Pool de Logs/s**. Para obter mais informações, consulte [SQL Server, Databases Object](../../../relational-databases/performance-monitor/sql-server-databases-object.md).  
  
##  <a name="AGlisteners"></a> Monitorando ouvintes de grupo de disponibilidade  
 Para monitorar os ouvintes de grupo de disponibilidade em sub-redes do cluster do WSFC, use as seguintes exibições:  
  
 [sys.availability_group_listener_ip_addresses](../../../relational-databases/system-catalog-views/sys-availability-group-listener-ip-addresses-transact-sql.md)  
 Retorna uma linha para cada endereço IP virtual compatível que está online atualmente para um ouvinte de grupo de disponibilidade.  
  
 **Nomes de colunas:** listener_id, ip_address, ip_subnet_mask, is_dhcp, network_subnet_ip, network_subnet_prefix_length, network_subnet_ipv4_mask, state, state_desc  
  
 [sys.availability_group_listeners](../../../relational-databases/system-catalog-views/sys-availability-group-listeners-transact-sql.md)  
 Para um determinado grupo de disponibilidade, retorna zero linhas indicando que nenhum nome de rede está associado ao grupo de disponibilidade ou retorna uma linha para cada configuração de ouvinte de grupo de disponibilidade no cluster do WSFC.  
  
 **Nomes de colunas:** group_id, listener_id, dns_name, port, is_conformant, ip_configuration_string_from_cluster  
  
 [sys.dm_tcp_listener_states](../../../relational-databases/system-dynamic-management-views/sys-dm-tcp-listener-states-transact-sql.md)  
 Retorna uma linha que contém informações de estado dinâmico para cada ouvinte de TCP.  
  
 **Nomes de colunas:** listener_id, ip_address, is_ipv4, port, type, type_desc, state, state_desc, start_time  
  
 **Chave primária:** listener_id  
  
 Para obter informações sobre ouvintes do grupo de disponibilidade, veja [Ouvintes do grupo de disponibilidade, conectividade de cliente e failover de aplicativos &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/listeners-client-connectivity-application-failover.md).  
  
##  <a name="RelatedTasks"></a> Tarefas relacionadas  
 **Tarefas de monitoramento dos grupos de disponibilidade AlwaysOn:**  
  
-   [Usar os detalhes do Pesquisador de Objetos para monitorar grupos de disponibilidade &#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-object-explorer-details-to-monitor-availability-groups.md)  
  
-   [Exibir as propriedades do grupo de disponibilidade &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/view-availability-group-properties-sql-server.md)  
  
-   [Exibir as propriedades da réplica de disponibilidade &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/view-availability-replica-properties-sql-server.md)  
  
-   [Exibir propriedades do ouvinte do grupo de disponibilidade &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/view-availability-group-listener-properties-sql-server.md)  
  
 **Referência do monitoramento de grupos de disponibilidade AlwaysOn (Transact-SQL):**  
  
-   [SERVERPROPERTY &#40;Transact-SQL&#41;](../../../t-sql/functions/serverproperty-transact-sql.md)  
  
-   [sys.availability_group_listener_ip_addresses &#40;Transact-SQL&#41;](../../../relational-databases/system-catalog-views/sys-availability-group-listener-ip-addresses-transact-sql.md)  
  
-   [sys.availability_group_listeners &#40;Transact-SQL&#41;](../../../relational-databases/system-catalog-views/sys-availability-group-listeners-transact-sql.md)  
  
-   [sys.availability_databases_cluster &#40;Transact-SQL&#41;](../../../relational-databases/system-catalog-views/sys-availability-databases-cluster-transact-sql.md)  
  
-   [sys.availability_groups &#40;Transact-SQL&#41;](../../../relational-databases/system-catalog-views/sys-availability-groups-transact-sql.md)  
  
-   [sys.availability_read_only_routing_lists &#40;Transact-SQL&#41;](../../../relational-databases/system-catalog-views/sys-availability-read-only-routing-lists-transact-sql.md)  
  
-   [sys.availability_replicas &#40;Transact-SQL&#41;](../../../relational-databases/system-catalog-views/sys-availability-replicas-transact-sql.md)  
  
-   [sys.dm_hadr_availability_replica_cluster_nodes &#40;Transact-SQL&#41;](../../../relational-databases/system-dynamic-management-views/sys-dm-hadr-availability-replica-cluster-nodes-transact-sql.md)  
  
-   [sys.dm_hadr_availability_replica_cluster_states &#40;Transact-SQL&#41;](../../../relational-databases/system-dynamic-management-views/sys-dm-hadr-availability-replica-cluster-states-transact-sql.md)  
  
-   [sys.database_mirroring_endpoints &#40;Transact-SQL&#41;](../../../relational-databases/system-catalog-views/sys-database-mirroring-endpoints-transact-sql.md)  
  
-   [sys.dm_hadr_auto_page_repair &#40;Transact-SQL&#41;](../../../relational-databases/system-dynamic-management-views/sys-dm-hadr-auto-page-repair-transact-sql.md)  
  
-   [sys.dm_hadr_availability_group_states &#40;Transact-SQL&#41;](../../../relational-databases/system-dynamic-management-views/sys-dm-hadr-availability-group-states-transact-sql.md)  
  
-   [sys.dm_hadr_availability_replica_cluster_states &#40;Transact-SQL&#41;](../../../relational-databases/system-dynamic-management-views/sys-dm-hadr-availability-replica-cluster-states-transact-sql.md)  
  
-   [sys.dm_hadr_availability_replica_states &#40;Transact-SQL&#41;](../../../relational-databases/system-dynamic-management-views/sys-dm-hadr-availability-replica-states-transact-sql.md)  
  
-   [sys.dm_hadr_database_replica_states &#40;Transact-SQL&#41;](../../../relational-databases/system-dynamic-management-views/sys-dm-hadr-database-replica-states-transact-sql.md)  
  
-   [sys.dm_hadr_database_replica_cluster_states &#40;Transact-SQL&#41;](../../../relational-databases/system-dynamic-management-views/sys-dm-hadr-database-replica-cluster-states-transact-sql.md)  
  
-   [sys.dm_hadr_cluster &#40;Transact-SQL&#41;](../../../relational-databases/system-dynamic-management-views/sys-dm-hadr-cluster-transact-sql.md)  
  
-   [sys.dm_hadr_cluster_members &#40;Transact-SQL&#41;](../../../relational-databases/system-dynamic-management-views/sys-dm-hadr-cluster-members-transact-sql.md)  
  
-   [sys.dm_hadr_cluster_networks &#40;Transact-SQL&#41;](../../../relational-databases/system-dynamic-management-views/sys-dm-hadr-cluster-networks-transact-sql.md)  
  
-   [sys.dm_hadr_database_replica_cluster_states &#40;Transact-SQL&#41;](../../../relational-databases/system-dynamic-management-views/sys-dm-hadr-database-replica-cluster-states-transact-sql.md)  
  
-   [sys.dm_hadr_database_replica_states &#40;Transact-SQL&#41;](../../../relational-databases/system-dynamic-management-views/sys-dm-hadr-database-replica-states-transact-sql.md)  
  
-   [sys.dm_hadr_instance_node_map &#40;Transact-SQL&#41;](../../../relational-databases/system-dynamic-management-views/sys-dm-hadr-instance-node-map-transact-sql.md)  
  
-   [sys.dm_hadr_name_id_map &#40;Transact-SQL&#41;](../../../relational-databases/system-dynamic-management-views/sys-dm-hadr-name-id-map-transact-sql.md)  
  
-   [sys.dm_os_performance_counters &#40;Transact-SQL&#41;](../../../relational-databases/system-dynamic-management-views/sys-dm-os-performance-counters-transact-sql.md)  
  
-   [sys.dm_tcp_listener_states &#40;Transact-SQL&#41;](../../../relational-databases/system-dynamic-management-views/sys-dm-tcp-listener-states-transact-sql.md)  
  
-   [sys.fn_hadr_backup_is_preferred_replica &#40;Transact-SQL&#41;](../../../relational-databases/system-functions/sys-fn-hadr-backup-is-preferred-replica-transact-sql.md)  
  
 **Contadores de desempenho do AlwaysOn:**  
  
-   [SQL Server, Réplica de Disponibilidade](../../../relational-databases/performance-monitor/sql-server-availability-replica.md)  
  
-   [SQL Server, Réplica de Banco de Dados](../../../relational-databases/performance-monitor/sql-server-database-replica.md)  
  
-   [SQL Server, Databases Object](../../../relational-databases/performance-monitor/sql-server-databases-object.md)  
  
 **Gerenciamento baseado em políticas para grupos de disponibilidade AlwaysOn**  
  
-   [Usar as políticas AlwaysOn para exibir a integridade de um grupo de disponibilidade &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/use-always-on-policies-to-view-the-health-of-an-availability-group-sql-server.md)  
  
-   [Usar o Painel AlwaysOn &#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-the-always-on-dashboard-sql-server-management-studio.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Grupos de Disponibilidade AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/always-on-availability-groups-sql-server.md)   
 [Visão geral dos grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [Monitoramento de grupos de disponibilidade &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/monitoring-of-availability-groups-sql-server.md)  
  
  
