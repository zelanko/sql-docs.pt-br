---
title: Exibições de gerenciamento dinâmico e exibições de catálogo do sistema (Grupos de Disponibilidade Always On – SQL Server) | Microsoft Docs
ms.custom: ag-guide
ms.date: 06/13/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
ms.assetid: 4320a4a4-6183-462b-8bda-e7424e7cb706
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 79318dcd39a91eb8e3b9f570425f73838a1e53a3
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/27/2018
ms.locfileid: "52417007"
---
# <a name="dynamic-management-views-and-system-catalog-views-always-on-availability-groups"></a>Exibições de gerenciamento dinâmico e exibições de catálogo do sistema (Grupos de Disponibilidade Always On)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Este tópico mostra algumas das consultas comuns em DMVs (exibições de gerenciamento dinâmico) do Always On que você pode usar para monitorar e solucionar problemas de grupos de disponibilidade.  
  
> [!TIP]  
>  No Painel Always On, você pode configurar facilmente a GUI para exibir muitas das DMVs das réplicas de disponibilidade e bancos de dados de disponibilidade clicando com o botão direito do mouse no respectivo cabeçalho de tabela e selecionando a DMV que você deseja exibir ou ocultar.  
  
 Para obter mais informações sobre as DMVs do grupo de disponibilidade, veja [Always On Availability Groups dynamic management views and functions &#40;Transact-SQL&#41; (Funções e exibições de gerenciamento dinâmico de Grupos de Disponibilidade Always On &#40;Transact-SQL&#41;)](~/relational-databases/system-dynamic-management-views/always-on-availability-groups-dynamic-management-views-functions.md). Para obter mais informações sobre a as exibições de catálogo de grupos de disponibilidade, veja [Exibições de catálogo de Grupos de Disponibilidade Always On &#40;Transact-SQL&#41;](~/relational-databases/system-catalog-views/always-on-availability-groups-catalog-views-transact-sql.md).  
  
## <a name="check-the-wsfc-cluster-node-configuration"></a>Verifique a configuração de nó de cluster do WSFC  
 A seguinte consulta T-SQL (Transact-SQL) recupera o status de todos os nós no cluster atual do WSFC (Cluster de Failover do Windows Server).  
  
```sql  
use master  
go  
select * from sys.dm_hadr_cluster_members  
go  
```  
  
 Este conjunto de resultados relata o status de cada nó de membro do cluster WSFC atual. Se o quorum for definido como **Nó e maioria do compartilhamento de arquivos**, até mesmo o compartilhamento de arquivos será relatado. Você pode ver o status de cada nó, inclusive o peso de votação de cada nó (o valor [number_of_quorum_votes](~/relational-databases/system-dynamic-management-views/sys-dm-hadr-cluster-members-transact-sql.md)).  
  
## <a name="explore-the-cluster-network"></a>Explorar a rede de cluster  
 A consulta a seguir recupera a configuração de rede do cluster WSFC atual.  
  
```sql  
select * from sys.dm_hadr_cluster_networks  
```  
  
 O conjunto de resultados contém uma linha para cada adaptador de rede no cluster WSFC. Por exemplo, em um cluster de dois nós que contém dois adaptadores de rede em cada nó, essa consulta retorna quatro linhas.  
  
## <a name="explore-the-availability-groups"></a>Explorar os grupos de disponibilidade  
 A consulta a seguir recupera informações sobre um grupo de disponibilidade.  
  
```sql  
select primary_replica, primary_recovery_health_desc, synchronization_health_desc from sys.dm_hadr_availability_group_states  
go  
select * from sys.availability_groups  
go  
select * from sys.availability_groups_cluster  
go  
```  
  
 As DMVs [sys.dm_hadr_availability_group_states &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/sys-dm-hadr-availability-group-states-transact-sql.md), [sys.availability_groups &#40;Transact-SQL&#41;](~/relational-databases/system-catalog-views/sys-availability-groups-transact-sql.md) e [sys.availability_groups_cluster](~/relational-databases/system-catalog-views/sys-availability-groups-cluster-transact-sql.md) retornam informações sobre os grupos de disponibilidade no cluster WSFC atual. Na verdade, [sys.availability_groups &#40;Transact-SQL&#41;](~/relational-databases/system-catalog-views/sys-availability-groups-transact-sql.md) e [sys.availability_groups_cluster](~/relational-databases/system-catalog-views/sys-availability-groups-cluster-transact-sql.md) parecem retornar informações idênticas.  
  
 No entanto, a [sys.availability_groups_cluster](~/relational-databases/system-catalog-views/sys-availability-groups-cluster-transact-sql.md) relata metadados do grupo de disponibilidade armazenado no Cluster WSFC, enquanto a [sys.availability_groups &#40;Transact-SQL&#41;](~/relational-databases/system-catalog-views/sys-availability-groups-transact-sql.md) relata os metadados do grupo de disponibilidade que são armazenados em cache no espaço de processo do SQL Server. Além disso, essas duas DMVs relatam informações de configuração enquanto a [sys.dm_hadr_availability_group_states &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/sys-dm-hadr-availability-group-states-transact-sql.md) relata os status de integridade atual dos grupos de disponibilidade.  
  
> [!IMPORTANT]  
>  Essa nomenclatura é transferida com as DMVs que documentam réplicas de disponibilidade e bancos de dados de disponibilidade.  
  
## <a name="explore-the-availability-replicas"></a>Explorar as réplicas de disponibilidade  
 A consulta a seguir recupera informações sobre as réplicas de disponibilidade definidas em seus grupos de disponibilidade.  
  
```sql  
select replica_id, role_desc, connected_state_desc, synchronization_health_desc from sys.dm_hadr_availability_replica_states  
go  
select replica_server_name, replica_id, availability_mode_desc, endpoint_url from sys.availability_replicas  
go  
select replica_server_name, join_state_desc from sys.dm_hadr_availability_replica_cluster_states  
go  
```  
  
 Assim como nas DMVs de grupos de disponibilidade, você encontra três DMVs que relatam em réplicas de disponibilidade. A [sys.dm_hadr_availability_replica_states](~/relational-databases/system-dynamic-management-views/sys-dm-hadr-availability-replica-states-transact-sql.md) relata informações do estado sobre as réplicas de disponibilidade que são armazenadas localmente em cache no SQL Server, e a [sys.dm_hadr_availability_replica_cluster_states](~/relational-databases/system-dynamic-management-views/sys-dm-hadr-availability-replica-cluster-states-transact-sql.md) relata informações de estado sobre as réplicas de disponibilidade do cluster WSFC. Por fim, a [sys.availability_replicas](~/relational-databases/system-dynamic-management-views/sys-dm-hadr-availability-replica-cluster-states-transact-sql.md) relata dados de configuração sobre as réplicas de disponibilidade, que são armazenadas em cache localmente no SQL Server.  
  
## <a name="explore-availability-replica-health"></a>Explorar a integridade da réplica de disponibilidade  
 A consulta a seguir recupera informações de integridade atuais sobre as réplicas de disponibilidade.  
  
```sql  
select replica_id, role_desc, recovery_health_desc, synchronization_health_desc from sys.dm_hadr_availability_replica_states  
go  
```  
  
 Compare os resultados da consulta na réplica primária e na réplica secundária e observe que, na réplica secundária, as informações de integridade são relatadas somente para essa réplica e não para as outras réplicas do grupo de disponibilidade.  
  
## <a name="explore-the-availability-databases"></a>Explorar os bancos de dados de disponibilidade  
 A consulta a seguir recupera informações sobre as réplicas de disponibilidade definidas em seu grupo de disponibilidade. Você pode observar as alterações nos resultados da consulta antes e depois de suspender a movimentação de dados em um banco de dados de disponibilidade.  
  
```sql
select * from sys.availability_databases_cluster  
go  
select group_database_id, database_name, is_failover_ready  from sys.dm_hadr_database_replica_cluster_states  
go  
select database_id, synchronization_state_desc, synchronization_health_desc, last_hardened_lsn, redo_queue_size, log_send_queue_size from sys.dm_hadr_database_replica_states  
go  
```  
  
 Aqui novamente, três DMVs do Always On apresentam relatórios sobre bancos de dados de disponibilidade. A [sys.availability_databases_cluster](~/relational-databases/system-catalog-views/sys-availability-databases-cluster-transact-sql.md) relata informações de configuração sobre bancos de dados de disponibilidade do cluster WSFC. A [sys.dm_hadr_database_replica_cluster_states](~/relational-databases/system-dynamic-management-views/sys-dm-hadr-database-replica-cluster-states-transact-sql.md) relata informações de estado sobre as réplicas de banco de dados, que são armazenadas em cache localmente no SQL Server. Ela contém algumas informações de estado importantes, como a preparação para failover da réplica de disponibilidade. Por fim, a [sys.dm_hadr_database_replica_states](~/relational-databases/system-dynamic-management-views/sys-dm-hadr-database-replica-states-transact-sql.md) apresenta um conjunto de resultados bastante detalhado que relata informações de identidade e estado de cada banco de dados de disponibilidade, como informações de progresso LSN para os logs das réplicas de banco de dados primária e secundária.  
  
## <a name="explore-availability-database-health"></a>Explorar a integridade do banco de dados de disponibilidade  
 A consulta a seguir recupera informações sobre a integridade de cada banco de dados de disponibilidade nas réplicas. Você pode observar as alterações nos resultados da consulta antes e depois de suspender a movimentação de dados em um banco de dados de disponibilidade.  
  
```sql  
select dc.database_name, dr.database_id, dr.synchronization_state_desc,   
dr.suspend_reason_desc, dr.synchronization_health_desc  
from sys.dm_hadr_database_replica_states dr  join sys.availability_databases_cluster dc  
on dr.group_database_id=dc.group_database_id   
where is_local=1  
go  
```  
  
  
