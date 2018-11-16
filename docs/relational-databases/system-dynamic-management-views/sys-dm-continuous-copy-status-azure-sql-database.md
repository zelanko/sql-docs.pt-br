---
title: sys.dm_continuous_copy_status (banco de dados SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: ''
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: system-objects
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
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: 9cbd0997a7d675c0c7630b730d6ba7514070ab8f
ms.sourcegitcommit: 9c6a37175296144464ffea815f371c024fce7032
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/15/2018
ms.locfileid: "51665935"
---
# <a name="sysdmcontinuouscopystatus-azure-sql-database"></a>sys.dm_continuous_copy_status (Banco de Dados SQL do Azure)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  Retorna uma linha para cada banco de dados do usuário (V11) atualmente envolvido em uma relação de cópia contínua replicação geográfica. Se mais de uma relação de cópia contínua for iniciada para um banco de dados primário, essa tabela conterá uma linha para cada banco de dados secundário ativo.  
  
Se você estiver usando a V12 do banco de dados SQL deve usar [DM geo_replication_link_status](../../relational-databases/system-dynamic-management-views/sys-dm-geo-replication-link-status-azure-sql-database.md) (porque *sys.dm_continuous_copy_status* só se aplica a V11).

  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**copy_guid**|**uniqueidentifier**|ID exclusiva do banco de dados de réplica.|  
|**partner_server**|**sysname**|Nome do servidor do Banco de Dados SQL vinculado.|  
|**partner_database**|**sysname**|Nome do banco de dados vinculado no servidor do Banco de Dados SQL.|  
|**last_replication**|**datetimeoffset**|O carimbo de data/hora da última transação replicada aplicada.|  
|**replication_lag_sec**|**int**|A diferença de tempo, em segundos, entre a hora atual e o carimbo de data/hora da última transação confirmada com êxito no banco de dados primário que não foi reconhecida pelo banco de dados secundário ativo.|  
|**replication_state**|**tinyint**|O estado de replicação de cópia contínua deste banco de dados. A seguir estão os valores possíveis e suas descrições.<br /><br /> 1: a propagação. O destino de replicação está sendo propagado e está em um estado transicionalmente inconsistente. Até que a propagação seja concluída, você não pode se conectar ao banco de dados secundário ativo. <br />2: a captura. O banco de dados secundário ativo está realizando a captura do banco de dados primário e está em um estado transacionalmente consistente.<br />3: nova propagação. O banco de dados secundário ativo está sendo repropagado automaticamente devido a uma falha de replicação irrecuperável.<br />4: suspenso. Isso não é uma relação de cópia contínua ativa. Esse estado geralmente indica que a largura de banda disponível para o interlink é insuficiente para o nível de atividade da transação no banco de dados primário. No entanto, a relação de cópia contínua ainda permanece intacta.|  
|**replication_state_desc**|**nvarchar(256)**|Descrição do replication_state:<br /><br /> SEEDING<br /><br /> CATCH_UP<br /><br /> RE_SEEDING<br /><br /> SUSPENDED|  
|**is_rpo_limit_reached**|**bit**|Isso sempre será definido como 0|  
|**is_target_role**|**bit**|0 = Origem da relação de cópia<br /><br /> 1 = Destino da relação de cópia|  
|**is_interlink_connected**|**bit**|1 = O interlink está conectado.<br /><br /> 0 = O interlink está desconectado.|  
  
## <a name="permissions"></a>Permissões  
 Para recuperar dados, requer associação na **db_owner** função de banco de dados. O usuário dbo, os membros de **dbmanager** função de banco de dados e o logon sa podem consultar essa exibição também.  
  
## <a name="remarks"></a>Comentários  
 O **sys.dm_continuous_copy_status** modo de exibição é criado na **recursos** de banco de dados e é visível em todos os bancos de dados, incluindo o mestre lógico. No entanto, a consulta dessa exibição no mestre lógico retorna um conjunto vazio.  
  
 Se a relação de cópia contínua é encerrada em um banco de dados, a linha desse banco de dados na **sys.dm_continuous_copy_status** desaparece da exibição.  
  
 Como o **DM database_copies** exibição, **sys.dm_continuous_copy_status** reflete o estado da relação de cópia contínua no qual o banco de dados é um primário ou ativo secundário banco de dados . Diferentemente **DM database_copies**, **sys.dm_continuous_copy_status** contém várias colunas que fornecem detalhes sobre as operações e desempenho. Essas colunas incluem **last_replication**, e **replication_lag_sec**...  
  
## <a name="see-also"></a>Consulte também  
 [DM database_copies &#40;banco de dados SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-database-copies-azure-sql-database.md)   
 [Procedimentos armazenados de replicação geográfica ativa &#40;Transact-SQL&#41;](https://msdn.microsoft.com/library/81658ee4-4422-4d73-bf7a-86a07422cb0d)  
  
  
