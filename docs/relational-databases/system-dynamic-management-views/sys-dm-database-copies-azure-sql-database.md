---
title: sys.DM database_copies (banco de dados do SQL Azure) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: ''
ms.prod_service: sql-database
ms.reviewer: ''
ms.service: sql-database
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- dm_database_copies_TSQL
- sys.dm_database_copies
- dm_database_copies
- sys.dm_database_copies_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- dm_database_copies
- sys.dm_database_copies
ms.assetid: d03d4657-86d1-4496-97e6-cc3bc292e0b1
caps.latest.revision: 25
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: 9b2e5b7b257ea0a22cf847f4e28f58c3c89a2d68
ms.sourcegitcommit: 7019ac41524bdf783ea2c129c17b54581951b515
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/23/2018
---
# <a name="sysdmdatabasecopies-azure-sql-database"></a>sys.dm_database_copies (Banco de Dados SQL do Azure)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  Retorna informações sobre a cópia do banco de dados.  
  
Para retornar informações sobre links de replicação geográfica, use o [sys.geo_replication_links](../../relational-databases/system-dynamic-management-views/sys-geo-replication-links-azure-sql-database.md) ou [sys.dm_geo_replication_link_status](../../relational-databases/system-dynamic-management-views/sys-dm-geo-replication-link-status-azure-sql-database.md) exibições (disponíveis no SQL Database V12).
  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**database_id**|**Int**|A ID do banco de dados atual na exibição de `sys.databases`.|  
|**start_date**|**datetimeoffset**|A hora UTC em um datacenter regional do [!INCLUDE[ssSDS](../../includes/sssds-md.md)] quando a cópia do banco de dados foi iniciada.|  
|**modify_date**|**datetimeoffset**|A hora UTC em um datacenter regional do [!INCLUDE[ssSDS](../../includes/sssds-md.md)] quando a cópia do banco de dados tiver sido concluída. O novo banco de dados é transacionalmente consistente com o banco de dados primário a partir desse momento. As informações de conclusão são atualizadas a cada 1 minuto.<br /><br />Hora UTC refletir a última atualização do campo percent_complete.|  
|**percent_complete**|**real**|O percentual de bytes que foram copiados. Os valores variam de 0 a 100. O [!INCLUDE[ssSDS](../../includes/sssds-md.md)] pode se recuperar automaticamente de alguns erros, como failover, e reiniciar a cópia do banco de dados. Nesse caso, percent_complete reiniciaria a partir de 0.|  
|**error_code**|**Int**|Quando for maior que 0, o código indica o erro ocorrido ao copiar. O valor será igual a 0 se nenhum erro tiver ocorrido.|  
|**error_desc**|**nvarchar(4096)**|A descrição do erro ocorrido ao copiar.|  
|**error_severity**|**Int**|Retornará 16 se a cópia do banco de dados tiver falhado.|  
|**error_state**|**Int**|Retornará 1 se a cópia tiver falhado.|  
|**copy_guid**|**uniqueidentifier**|ID exclusiva da operação de cópia.|  
|**partner_server**|**sysname**|Nome do servidor de banco de dados SQL em que a cópia é criada.|  
|**partner_database**|**sysname**|Nome da cópia do banco de dados no servidor do parceiro.|  
|**replication_state**|**tinyint**|O estado de replicação de cópia contínua para esse banco de dados. Os valores são:<br /><br /> 0 = pendente. Criação da cópia do banco de dados está agendada, mas as etapas de preparação necessárias ainda não foram concluídas ou estão temporariamente bloqueadas pela cota de propagação.<br /><br /> 1 = propagação. O banco de dados de cópia está sendo propagado ainda não está totalmente sincronizado com o banco de dados de origem. Nesse estado, você não pode se conectar a cópia. Para cancelar a operação de propagação em andamento, o banco de dados de cópia deve ser descartado.|  
|**replication_state_desc**|**nvarchar(256)**|Descrição do replication_state:<br /><br /> PENDING<br /><br /> SEEDING<br />|  
|**maximum_lag**|**Int**|Campo reservado.|  
|**is_continuous_copy**|**bit**|0 = retorna 0|  
|**is_target_role**|**bit**|0 = banco de dados de origem<br /><br /> 1 = o banco de dados de cópia|  
|**is_interlink_connected**|bit|Campo reservado.|  
|**is_offline_secondary**|bit|Campo reservado.|  
  
## <a name="permissions"></a>Permissões  
 Essa exibição só está disponível na **mestre** banco de dados para o logon principal no nível de servidor.  
  
## <a name="remarks"></a>Remarks  
 Você pode usar o **sys.DM database_copies** exibir no **mestre** banco de dados de origem ou destino [!INCLUDE[ssSDS](../../includes/sssds-md.md)] server. Quando a cópia do banco de dados é concluída com êxito e o novo banco de dados fica ONLINE, a linha de **sys.DM database_copies** exibição é removida automaticamente.  
  
  
