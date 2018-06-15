---
title: sys.DM hadr_availability_replica_states (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 10/16/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
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
caps.latest.revision: 65
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: e04fa466f018e114fe66686b81c5e5899dd2371e
ms.sourcegitcommit: 7019ac41524bdf783ea2c129c17b54581951b515
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/23/2018
ms.locfileid: "34466462"
---
# <a name="sysdmhadravailabilityreplicastates-transact-sql"></a>sys.dm_hadr_availability_replica_states (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Retorna uma linha para cada réplica local e uma linha para cada réplica remota no mesmo sempre no grupo de disponibilidade como uma réplica local. Cada linha contém informações sobre o estado de uma determinada réplica.  
  
> [!IMPORTANT]  
>  Para obter informações sobre cada réplica em um determinado grupo de disponibilidade, consulte **sys.DM hadr_availability_replica_states** na instância do servidor que está hospedando a réplica primária. Quando consultado em uma instância de servidor que está hospedando uma réplica secundária de um grupo de disponibilidade, essa exibição de gerenciamento dinâmico retorna apenas informações locais do grupo de disponibilidade.  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**replica_id**|**uniqueidentifier**|Identificador exclusivo da réplica.|  
|**group_id**|**uniqueidentifier**|Identificador exclusivo do grupo de disponibilidade.|  
|**is_local**|**bit**|Se a réplica é local, um de:<br /><br /> 0 = indica uma réplica secundária remota em um grupo de disponibilidade cuja réplica primária é hospedada pela instância do servidor local. Esse valor ocorre apenas no local da réplica primária.<br /><br /> 1 = indica uma réplica local. Em réplicas secundárias, esse é o único valor disponível para o grupo de disponibilidade ao qual a réplica pertence.|  
|**role**|**tinyint**|Atual [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] função de uma réplica local ou uma réplica remota conectada, um destes:<br /><br /> 0 = Resolvendo<br /><br /> 1 = Primária<br /><br /> 2 = Secundária<br /><br /> Para obter informações sobre as funções do [!INCLUDE[ssHADR](../../includes/sshadr-md.md)], confira [Visão geral dos grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md).|  
|**role_desc**|**nvarchar(60)**|Descrição do **função**, um de:<br /><br /> RESOLVING<br /><br /> PRIMARY<br /><br /> SECONDARY|  
|**operational_state**|**tinyint**|Estado operacional atual da réplica, um de:<br /><br /> 0 = Failover pendente<br /><br /> 1 = pendente<br /><br /> 2 = Online<br /><br /> 3 = off-line<br /><br /> 4 = Falha<br /><br /> 5 = Com falha, sem quorum<br /><br /> NULL = A réplica não é local.<br /><br /> Para obter mais informações, consulte [funções e estados operacionais](#RolesAndOperationalStates), mais adiante neste tópico.|  
|**operational\_state\_desc**|**nvarchar(60)**|Descrição do **operacionais\_estado**, um de:<br /><br /> PENDING_FAILOVER<br /><br /> PENDING<br /><br /> ONLINE<br /><br /> OFFLINE<br /><br /> FAILED<br /><br /> FAILED_NO_QUORUM<br /><br /> NULL|  
|**recuperação\_integridade**|**tinyint**|Pacote cumulativo de atualizações do **banco de dados\_estado** coluna o [sys.DM hadr_database_replica_states](../../relational-databases/system-dynamic-management-views/sys-dm-hadr-database-replica-states-transact-sql.md) exibição de gerenciamento dinâmico. Estes são os valores possíveis e suas descrições.<br /><br /> 0: em andamento.  Pelo menos um banco de dados Unido tem um estado de banco de dados diferente de ONLINE (**banco de dados\_estado** é não a 0).<br /><br /> 1: on-line. Bancos de dados Unidos têm um estado de banco de dados de ONLINE (**database_state** é 0).<br /><br /> NULL: **is_local** = 0|  
|**recovery_health_desc**|**nvarchar(60)**|Descrição do **recovery_health**, um de:<br /><br /> ONLINE_IN_PROGRESS<br /><br /> ONLINE<br /><br /> NULL|  
|**sincronização\_integridade**|**tinyint**|Reflete um rollup do estado de sincronização de banco de dados (**synchronization_state**) de todos os bancos de dados de disponibilidade de associado (também conhecido como *réplicas*) e o modo de (a réplica de disponibilidade confirmação síncrona ou assíncrona modo de confirmação). Pacote cumulativo de atualizações refletirá o estado acumulado mais íntegro dos bancos de dados na réplica. Abaixo estão os valores possíveis e suas descrições.<br /><br /> 0: não está íntegro.   Pelo menos um banco de dados unido está no estado NOT SYNCHRONIZING.<br /><br /> 1: parcialmente íntegro. Algumas réplicas não estão no estado de sincronização designado: as réplicas de confirmação síncrona devem ser sincronizadas e as réplicas de confirmação assíncrona devem estar sincronizando.<br /><br /> 2: íntegro. Todas as réplicas estão no estado de sincronização designado: as réplicas de confirmação síncrona estão sincronizadas e as réplicas de confirmação assíncrona estão sincronizando.|  
|**synchronization_health_desc**|**nvarchar(60)**|Descrição do **synchronization_health**, um de:<br /><br /> NOT_HEALTHY<br /><br /> PARTIALLY_HEALTHY<br /><br /> HEALTHY|  
|**connected_state**|**tinyint**|Se uma réplica secundária está conectada atualmente à réplica primária. Os valores possíveis são mostrados abaixo e suas descrições.<br /><br /> 0: desconectado. A resposta de uma réplica de disponibilidade para o estado desconectado depende de sua função: na réplica primária, se uma réplica secundária estiver desconectada, seus bancos de dados secundários são marcados como NOT SYNCHRONIZED na réplica primária, que aguarda o secundário reconectar; Em uma réplica secundária, ao detectar que está desconectada, a réplica secundária tentará reconectar-se à réplica primária.<br /><br /> 1: conectado.<br /><br /> Cada réplica primária acompanha o estado da conexão para cada réplica secundária no mesmo grupo de disponibilidade. As réplicas secundárias acompanham o estado da conexão apenas da réplica primária.|  
|**connected_state_desc**|**nvarchar(60)**|Descrição do **connection_state**, um de:<br /><br /> DISCONNECTED<br /><br /> CONNECTED|  
|**last_connect_error_number**|**Int**|O número do último erro de conexão.|  
|**last_connect_error_description**|**nvarchar(1024)**|Texto do **last_connect_error_number** mensagem.|  
|**last_connect_error_timestamp**|**datetime**|Carimbo de data e hora que indica quando o **last_connect_error_number** erro.|  
  
##  <a name="RolesAndOperationalStates"></a> Funções e estados operacionais  
 A função **função**, reflete o estado de uma determinada réplica de disponibilidade e o estado operacional, **operational_state**, descreve se a réplica está pronta para processar solicitações de cliente para todos os banco de dados da réplica de disponibilidade. A seguir está um resumo dos estados operacionais possíveis para cada função: RESOLVENDO, primário e SECUNDÁRIO.  
  
 **RESOLUÇÃO:** quando uma réplica de disponibilidade está na função RESOLVING, os estados operacionais possíveis são conforme mostrado na tabela a seguir.  
  
|Estado Operacional|Description|  
|-----------------------|-----------------|  
|PENDING_FAILOVER|Um comando de failover está sendo processado para o grupo de disponibilidade.|  
|OFFLINE|Todos os dados da configuração da réplica de disponibilidade foram atualizados no cluster do WSFC e, também, em metadados locais, mas o grupo de disponibilidade atual não tem uma réplica primária.|  
|FAILED|Ocorreu uma falha de leitura durante uma tentativa de recuperar informações do cluster do WSFC.|  
|FAILED_NO_QUORUM|O nó WSFC local não tem quorum. Esse é um estado inferido.|  
  
 **PRIMARY:** quando uma réplica de disponibilidade está executando a função primária, atualmente é a réplica primária. Os estados operacionais possíveis são conforme mostrado na tabela a seguir.  
  
|Estado Operacional|Description|  
|-----------------------|-----------------|  
|PENDING|Este é um estado transiente, mas uma réplica primária pode ficar neste estado se os trabalhos não estiverem disponíveis para processar solicitações.|  
|ONLINE|O recurso de grupo de disponibilidade está online, e todos os threads de trabalho do banco de dados foram coletados.|  
|FAILED|A réplica de disponibilidade não pode ler e/ou gravar no cluster do WSFC.|  
  
 **SECONDARY:** quando uma réplica de disponibilidade está executando a função SECUNDÁRIA, ele é atualmente uma réplica secundária. Os estados operacionais possíveis são conforme mostrado na tabela a seguir.  
  
|Estado Operacional|Description|  
|-----------------------|-----------------|  
|ONLINE|A réplica secundária local está conectada à réplica primária.|  
|FAILED|A réplica secundária local não está disponível para leitura e/ou gravação no cluster do WSFC.|  
|NULL|Em uma réplica primária, esse valor é retornado quando a linha está relacionada a uma réplica secundária.|  
  
## <a name="security"></a>Segurança  
  
### <a name="permissions"></a>Permissões  
 , é necessário ter permissão VIEW SERVER STATE no servidor.  
  
## <a name="see-also"></a>Consulte também  
 [Visão geral dos grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [Monitorar grupos de disponibilidade &#40;Transact-SQL&#41;](../../database-engine/availability-groups/windows/monitor-availability-groups-transact-sql.md)  
  
  
