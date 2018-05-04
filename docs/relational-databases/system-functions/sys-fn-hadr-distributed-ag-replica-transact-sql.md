---
title: sys.fn_hadr_distributed_ag_replica (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-functions
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.fn_hadr_distributed_ag_replica
- sys.fn_hadr_distributed_ag_replica_TSQL
- fn_hadr_distributed_ag_replica
- fn_hadr_distributed_ag_replica_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.fn_hadr_distributed_ag_replica
ms.assetid: a1e5f9cb-c350-4bb4-a04f-7394f6f25d62
caps.latest.revision: 12
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 52fc3c97e629acc3455cdeae5707429f44d3e2cc
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="sysfnhadrdistributedagreplica-transact-sql"></a>sys.fn_hadr_distributed_ag_replica (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Usado para mapear uma réplica em um grupo de disponibilidade distribuída para o grupo de disponibilidade local.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sys.fn_hadr_distributed_ag_replica( lag_Id, replica_id )  
```  
  
## <a name="arguments"></a>Argumentos  
 '*lag_Id*'  
 É o identificador do grupo de disponibilidade distribuída. *lag_Id* é do tipo **uniqueidentifier**.  
  
 '*replica_id*'  
 É o identificador de uma réplica no grupo de disponibilidade distribuída. *replica_id* é do tipo **uniqueidentifier**.  
  
## <a name="tables-returned"></a>Tabelas retornadas  
 Retorna as informações a seguir.  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**group_id**|**uniqueidentifier**|Identificador exclusivo (GUID) do grupo de disponibilidade local.|  
  
## <a name="examples"></a>Exemplos  
  
### <a name="using-sysfnhadrdistributedagreplica"></a>Usando sys.fn_hadr_distributed_ag_replica  
 O exemplo a seguir retorna uma tabela com o identificador de grupo de disponibilidade local que está associado ao grupo de disponibilidade distribuída especificado e a réplica.  
  
```  
DECLARE @lagId uniqueidentifier = '4A03D1A8-4AE6-B153-E7E9-ED22A546008D'  
DECLARE @replicaId uniqueidentifier = 'D5517513-04A8-FD82-14C6-E684EC913935'  
  
SELECT * FROM sys.fn_hadr_distributed_ag_replica(@lagId, @replicaId)  
GO  
```  
  
## <a name="see-also"></a>Consulte também  
 [Funções de grupos de disponibilidade AlwaysOn &#40;Transact-SQL&#41;](../../relational-databases/system-functions/always-on-availability-groups-functions-transact-sql.md)   
 [Grupos de disponibilidade AlwaysOn & #40; SQL Server & #41;](../../database-engine/availability-groups/windows/always-on-availability-groups-sql-server.md)   
 [Grupos de disponibilidade de Distributed &#40;grupos de disponibilidade AlwaysOn&#41;](../../database-engine/availability-groups/windows/distributed-availability-groups-always-on-availability-groups.md)  
 [CRIAR GRUPO de DISPONIBILIDADE &#40;Transact-SQL&#41;](../../t-sql/statements/create-availability-group-transact-sql.md)   
 [ALTERAR o grupo de disponibilidade & #40; Transact-SQL & #41;](../../t-sql/statements/alter-availability-group-transact-sql.md)  
  
  
