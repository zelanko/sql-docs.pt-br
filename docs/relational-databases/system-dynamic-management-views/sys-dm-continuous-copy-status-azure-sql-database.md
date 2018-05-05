---
title: sys.DM continuous_copy_status (banco de dados do SQL Azure) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: ''
ms.prod_service: sql-database
ms.reviewer: ''
ms.service: sql-database
ms.component: dmv's
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.dm_continuous_copy_status_TSQL
- dm_continuous_copy_status_TSQL
- dm_continuous_copy_status
- sys.dm_continuous_copy_status
dev_langs:
- TSQL
helpviewer_keywords:
- dm_continuous_copy_status
- sys.dm_continuous_copy_status
ms.assetid: 411b2e71-4421-4ef5-900d-5af068750899
caps.latest.revision: 18
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: 2371e16e23b1cbc8caad3170e51bfff592f3ed81
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="sysdmcontinuouscopystatus-azure-sql-database"></a>sys.DM continuous_copy_status (banco de dados do SQL Azure)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  Retorna uma linha para cada banco de dados do usuário (V11) atualmente envolvido em uma relação de cópia contínua de replicação geográfica. Se mais de uma relação de cópia contínua for iniciada para um banco de dados primário, essa tabela conterá uma linha para cada banco de dados secundário ativo.  
  
Se você estiver usando o SQL Database V12 use [sys.dm_geo_replication_link_status](../../relational-databases/system-dynamic-management-views/sys-dm-geo-replication-link-status-azure-sql-database.md) (porque *sys.DM continuous_copy_status* só se aplica a V11).

  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**copy_guid**|**uniqueidentifier**|ID exclusiva do banco de dados de réplica.|  
|**partner_server**|**sysname**|Nome do servidor do Banco de Dados SQL vinculado.|  
|**partner_database**|**sysname**|Nome do banco de dados vinculado no servidor do Banco de Dados SQL.|  
|**last_replication**|**datetimeoffset**|O carimbo de data/hora da última transação replicada aplicada.|  
|**replication_lag_sec**|**Int**|A diferença de tempo, em segundos, entre a hora atual e o carimbo de data/hora da última transação confirmada com êxito no banco de dados primário que não foi reconhecida pelo banco de dados secundário ativo.|  
|**replication_state**|**tinyint**|O estado de replicação de cópia contínua para esse banco de dados. Estes são os valores possíveis e suas descrições.<br /><br /> 1: a propagação. O destino de replicação está sendo propagado e está em um estado transicionalmente inconsistente. Até que a propagação seja concluída, você não pode se conectar ao banco de dados secundário ativo. <br />2: mesmo ritmo. O banco de dados secundário ativo está realizando a captura do banco de dados primário e está em um estado transacionalmente consistente.<br />3: nova propagação. O banco de dados secundário ativo está sendo repropagado automaticamente devido a uma falha de replicação irrecuperável.<br />4: suspenso. Isso não é uma relação de cópia contínua ativa. Esse estado geralmente indica que a largura de banda disponível para o interlink é insuficiente para o nível de atividade da transação no banco de dados primário. No entanto, a relação de cópia contínua ainda permanece intacta.|  
|**replication_state_desc**|**nvarchar(256)**|Descrição do replication_state:<br /><br /> SEEDING<br /><br /> CATCH_UP<br /><br /> RE_SEEDING<br /><br /> SUSPENDED|  
|**is_rpo_limit_reached**|**bit**|Isso sempre será definido como 0|  
|**is_target_role**|**bit**|0 = Origem da relação de cópia<br /><br /> 1 = Destino da relação de cópia|  
|**is_interlink_connected**|**bit**|1 = O interlink está conectado.<br /><br /> 0 = O interlink está desconectado.|  
  
## <a name="permissions"></a>Permissões  
 Para recuperar dados, requer a participação no **db_owner** função de banco de dados. O usuário dbo, membro do **dbmanager** função de banco de dados e o logon sa podem consultar esse modo de exibição.  
  
## <a name="remarks"></a>Remarks  
 O **sys.DM continuous_copy_status** exibição é criada no **recurso** banco de dados e é visível em todos os bancos de dados, incluindo o mestre lógico. No entanto, a consulta dessa exibição no mestre lógico retorna um conjunto vazio.  
  
 Se a relação de cópia contínua é encerrada em um banco de dados, a linha do banco de dados no **sys.DM continuous_copy_status** desaparece da exibição.  
  
 Como o **sys.DM database_copies** exibição, **sys.DM continuous_copy_status** reflete o estado da relação de cópia contínua no qual o banco de dados é um principal ou ativo secundário banco de dados . Ao contrário de **sys.DM database_copies**, **sys.DM continuous_copy_status** contém várias colunas que fornecem detalhes sobre as operações e o desempenho. Essas colunas incluem **last_replication**, e **replication_lag_sec**...  
  
## <a name="see-also"></a>Consulte também  
 [sys.DM database_copies &#40;banco de dados do SQL Azure&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-database-copies-azure-sql-database.md)   
 [Procedimentos armazenados de replicação geográfica ativa &#40;Transact-SQL&#41;](http://msdn.microsoft.com/library/81658ee4-4422-4d73-bf7a-86a07422cb0d)  
  
  
