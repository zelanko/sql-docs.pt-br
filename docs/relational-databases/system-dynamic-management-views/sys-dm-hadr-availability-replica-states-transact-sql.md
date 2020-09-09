---
description: sys.dm_hadr_availability_replica_states (Transact-SQL)
title: sys. dm_hadr_availability_replica_states (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 10/16/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_hadr_availability_replica_states
- sys.dm_hadr_availability_replica_states_TSQL
- sys.dm_hadr_availability_replica_states
- dm_hadr_availability_replica_states_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- Availability Groups [SQL Server], monitoring
- sys.dm_hadr_availability_replica_states dynamic management view
ms.assetid: d2e678bb-51e8-4a61-b223-5c0b8d08b8b1
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 347d05c0bfc37b1c14fddb728df5508e062cb13d
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89546549"
---
# <a name="sysdm_hadr_availability_replica_states-transact-sql"></a>sys.dm_hadr_availability_replica_states (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Retorna uma linha para cada réplica local e uma linha para cada réplica remota no mesmo grupo de disponibilidade Always On que uma réplica local. Cada linha contém informações sobre o estado de uma determinada réplica.  
  
> [!IMPORTANT]  
>  Para obter informações sobre cada réplica em um determinado grupo de disponibilidade, consulte **Sys. dm_hadr_availability_replica_states** na instância do servidor que está hospedando a réplica primária. Quando consultado em uma instância de servidor que está hospedando uma réplica secundária de um grupo de disponibilidade, essa exibição de gerenciamento dinâmico retorna apenas informações locais do grupo de disponibilidade.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**replica_id**|**uniqueidentifier**|Identificador exclusivo da réplica.|  
|**group_id**|**uniqueidentifier**|Identificador exclusivo do grupo de disponibilidade.|  
|**is_local**|**bit**|Se a réplica é local, uma das:<br /><br /> 0 = indica uma réplica secundária remota em um grupo de disponibilidade cuja réplica primária é hospedada pela instância do servidor local. Esse valor ocorre apenas no local da réplica primária.<br /><br /> 1 = indica uma réplica local. Em réplicas secundárias, esse é o único valor disponível para o grupo de disponibilidade ao qual a réplica pertence.|  
|**role**|**tinyint**|[!INCLUDE[ssHADR](../../includes/sshadr-md.md)]Função atual de uma réplica local ou de uma réplica remota conectada, uma das:<br /><br /> 0 = Resolvendo<br /><br /> 1 = Primária<br /><br /> 2 = Secundária<br /><br /> Para obter informações sobre as funções do [!INCLUDE[ssHADR](../../includes/sshadr-md.md)], confira [Visão geral dos grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md).|  
|**role_desc**|**nvarchar(60)**|Descrição da **função**, uma das:<br /><br /> RESOLVING<br /><br /> PRIMARY<br /><br /> SECONDARY|  
|**operational_state**|**tinyint**|Estado operacional atual da réplica, um dos:<br /><br /> 0 = Failover pendente<br /><br /> 1 = pendente<br /><br /> 2 = online<br /><br /> 3 = offline<br /><br /> 4 = falha<br /><br /> 5 = Com falha, sem quorum<br /><br /> NULL = A réplica não é local.<br /><br /> Para obter mais informações, consulte [funções e Estados operacionais](#RolesAndOperationalStates), mais adiante neste tópico.|  
|**\_estado operacional \_ desc**|**nvarchar(60)**|Descrição do ** \_ estado operacional**, uma das:<br /><br /> PENDING_FAILOVER<br /><br /> PENDING<br /><br /> ONLINE<br /><br /> OFFLINE<br /><br /> FAILED<br /><br /> FAILED_NO_QUORUM<br /><br /> NULO|  
|**integridade da recuperação \_**|**tinyint**|Acúmulo da coluna ** \_ estado do banco de dados** da exibição de gerenciamento dinâmico [Sys. dm_hadr_database_replica_states](../../relational-databases/system-dynamic-management-views/sys-dm-hadr-database-replica-states-transact-sql.md) . A seguir estão os possíveis valores e suas descrições.<br /><br /> 0: em andamento.  Pelo menos um banco de dados Unido tem um estado de banco de dados diferente de ONLINE (o** \_ estado do banco de dados** não é 0).<br /><br /> 1: online. Todos os bancos de dados associados têm um estado de banco de dados ONLINE (**database_state** é 0).<br /><br /> NULL: **is_local** = 0|  
|**recovery_health_desc**|**nvarchar(60)**|Descrição de **recovery_health**, uma das:<br /><br /> ONLINE_IN_PROGRESS<br /><br /> ONLINE<br /><br /> NULO|  
|**integridade da sincronização \_**|**tinyint**|Reflete um ROLLUP do estado de sincronização do banco de dados (**synchronization_state**) de todos os bancos de dados de disponibilidade associados (também conhecidos como *réplicas*) e o modo de disponibilidade da réplica (modo de confirmação síncrona ou confirmação de confirmação). O acúmulo refletirá o estado de acumulação mínimo íntegro dos bancos de dados na réplica. Abaixo estão os possíveis valores e suas descrições.<br /><br /> 0: não íntegro.   Pelo menos um banco de dados unido está no estado NOT SYNCHRONIZING.<br /><br /> 1: parcialmente íntegro. Algumas réplicas não estão no estado de sincronização designado: as réplicas de confirmação síncrona devem ser sincronizadas e as réplicas de confirmação assíncrona devem estar sincronizando.<br /><br /> 2: íntegro. Todas as réplicas estão no estado de sincronização designado: as réplicas de confirmação síncrona estão sincronizadas e as réplicas de confirmação assíncrona estão sincronizando.|  
|**synchronization_health_desc**|**nvarchar(60)**|Descrição de **synchronization_health**, uma das:<br /><br /> NOT_HEALTHY<br /><br /> PARTIALLY_HEALTHY<br /><br /> HEALTHY|  
|**connected_state**|**tinyint**|Se uma réplica secundária está conectada atualmente à réplica primária. Os valores possíveis são mostrados abaixo com suas descrições.<br /><br /> 0: desconectado. A resposta de uma réplica de disponibilidade para o estado desconectado depende de sua função: na réplica primária, se uma réplica secundária estiver desconectada, seus bancos de dados secundários serão marcados como não SINCRONIZAdos na réplica primária, o que aguardará que o secundário se reconecte; Em uma réplica secundária, após detectar que ela está desconectada, a réplica secundária tenta se reconectar à réplica primária.<br /><br /> 1: conectado.<br /><br /> Cada réplica primária acompanha o estado da conexão para cada réplica secundária no mesmo grupo de disponibilidade. As réplicas secundárias acompanham o estado da conexão apenas da réplica primária.|  
|**connected_state_desc**|**nvarchar(60)**|Descrição de **connection_state**, uma das:<br /><br /> DISCONNECTED<br /><br /> CONNECTED|  
|**last_connect_error_number**|**int**|O número do último erro de conexão.|  
|**last_connect_error_description**|**nvarchar(1024)**|Texto da mensagem de **last_connect_error_number** .|  
|**last_connect_error_timestamp**|**datetime**|Carimbo de data/hora em que indica quando ocorreu o erro de **last_connect_error_number** .|  
  
##  <a name="roles-and-operational-states"></a><a name="RolesAndOperationalStates"></a> Funções e Estados operacionais  
 A função, **função**, reflete o estado de uma determinada réplica de disponibilidade e o estado operacional, **operational_state**, descreve se a réplica está pronta para processar solicitações de cliente para todo o banco de dados da réplica de disponibilidade. Veja a seguir um resumo dos Estados operacionais que são possíveis para cada função: resolução, primário e secundário.  
  
 **Resolvendo:** Quando uma réplica de disponibilidade está na função de resolução, os Estados operacionais possíveis são mostrados na tabela a seguir.  
  
|Estado Operacional|Descrição|  
|-----------------------|-----------------|  
|PENDING_FAILOVER|Um comando de failover está sendo processado para o grupo de disponibilidade.|  
|OFFLINE|Todos os dados da configuração da réplica de disponibilidade foram atualizados no cluster do WSFC e, também, em metadados locais, mas o grupo de disponibilidade atual não tem uma réplica primária.|  
|FAILED|Ocorreu uma falha de leitura durante uma tentativa de recuperar informações do cluster do WSFC.|  
|FAILED_NO_QUORUM|O nó WSFC local não tem quorum. Esse é um estado inferido.|  
  
 **Primário:** Quando uma réplica de disponibilidade está executando a função primária, ela é a réplica primária no momento. Os Estados operacionais possíveis são os mostrados na tabela a seguir.  
  
|Estado Operacional|Descrição|  
|-----------------------|-----------------|  
|PENDING|Este é um estado transiente, mas uma réplica primária pode ficar neste estado se os trabalhos não estiverem disponíveis para processar solicitações.|  
|ONLINE|O recurso de grupo de disponibilidade está online, e todos os threads de trabalho do banco de dados foram coletados.|  
|FAILED|A réplica de disponibilidade não pode ler e/ou gravar no cluster do WSFC.|  
  
 **Secundário:** Quando uma réplica de disponibilidade está executando a função secundária, ela é atualmente uma réplica secundária. Os Estados operacionais possíveis são os mostrados na tabela a seguir.  
  
|Estado Operacional|Descrição|  
|-----------------------|-----------------|  
|ONLINE|A réplica secundária local está conectada à réplica primária.|  
|FAILED|A réplica secundária local não está disponível para leitura e/ou gravação no cluster do WSFC.|  
|NULO|Em uma réplica primária, esse valor é retornado quando a linha está relacionada a uma réplica secundária.|  
  
## <a name="security"></a>Segurança  
  
### <a name="permissions"></a>Permissões  
 , é necessário ter permissão VIEW SERVER STATE no servidor.  
  
## <a name="see-also"></a>Consulte Também  
 [Visão geral dos grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [Monitorar grupos de disponibilidade &#40;Transact-SQL&#41;](../../database-engine/availability-groups/windows/monitor-availability-groups-transact-sql.md)  
  
  
