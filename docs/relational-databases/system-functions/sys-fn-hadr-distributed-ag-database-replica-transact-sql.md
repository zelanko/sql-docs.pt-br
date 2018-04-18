---
title: sys.fn_hadr_distributed_ag_database_replica (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2016
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
- sys.fn_hadr_distributed_ag_database_replica
- sys.fn_hadr_distributed_ag_database_replica_TSQL
- fn_hadr_distributed_ag_database_replica
- fn_hadr_distributed_ag_database_replica_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.fn_hadr_distributed_ag_database_replica
ms.assetid: 0e6202a1-e872-4f53-99d7-c16b6f712efc
caps.latest.revision: 9
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: e828d50f9ed35dbec3bb72db9f52a3c6d5242f82
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="sysfnhadrdistributedagdatabasereplica-transact-sql"></a>sys.fn_hadr_distributed_ag_database_replica (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Usado para mapear um banco de dados em um grupo de disponibilidade distribuída para o banco de dados no grupo de disponibilidade local.  
   
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sys.fn_hadr_distributed_ag_database_replica( lag_Id, database_id )  
```  
  
## <a name="arguments"></a>Argumentos  
 '*lag_Id*'  
 É o identificador do grupo de disponibilidade distribuída. *lag_Id* é do tipo **uniqueidentifier**.  
  
 '*database_id*'  
 É o identificador do banco de dados em um grupo de disponibilidade distribuída. *database_id* é do tipo **uniqueidentifier**.  
  
## <a name="tables-returned"></a>Tabelas retornadas  
 Retorna as informações a seguir.  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**group_database_id**|**uniqueidentifier**|ID do banco de dados no grupo de disponibilidade local.|  
  
## <a name="examples"></a>Exemplos  
  
### <a name="using-sysfnhadrdistributedagdatabasereplica"></a>Usando sys.fn_hadr_distributed_ag_database_replica  
 O exemplo a seguir passa a ID de banco de dados em um grupo de disponibilidade distribuída. Retorna uma tabela com a ID de banco de dados associada ao grupo de disponibilidade local.  
  
```  
DECLARE @lagId uniqueidentifier = '4A03D1A8-4AE6-B153-E7E9-ED22A546008D'  
DECLARE @databaseId uniqueidentifier = '3FFA882A-C4C3-5B9E-A203-8F44BD9659F7'  
  
SELECT * FROM sys.fn_hadr_distributed_ag_database_replica(@lagId, @databaseId)  
GO  
```  
  
## <a name="see-also"></a>Consulte também  
 [Funções de grupos de disponibilidade sempre &#40;Transact-SQL&#41;](../../relational-databases/system-functions/always-on-availability-groups-functions-transact-sql.md)   
 [Grupos de Disponibilidade AlwaysOn &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/always-on-availability-groups-sql-server.md)   
 [Grupos de disponibilidade de Distributed &#40;em grupos de disponibilidade AlwaysOn&#41;](../../database-engine/availability-groups/windows/distributed-availability-groups-always-on-availability-groups.md)   
 [CRIAR GRUPO de DISPONIBILIDADE &#40;Transact-SQL&#41;](../../t-sql/statements/create-availability-group-transact-sql.md)   
 [ALTERAR o grupo de disponibilidade & #40; Transact-SQL & #41;](../../t-sql/statements/alter-availability-group-transact-sql.md)  
  
  
