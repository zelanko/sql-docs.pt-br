---
title: sys.geo_replication_links (banco de dados do SQL Azure) | Microsoft Docs
ms.custom: ''
ms.date: 10/18/2016
ms.prod: ''
ms.prod_service: sql-database
ms.reviewer: ''
ms.service: sql-database
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- dm_geo_replication_links_TSQL
- dm_geo_replication_links
- sys.dm_geo_replication_links
- sys.dm_geo_replication_links_TSQL
helpviewer_keywords:
- sys.dm_geo_replication_links dynamic management view
- dm_geo_replication_links dynamic management view
ms.assetid: 58911798-1d60-4f28-87ab-2def2bfc3de7
caps.latest.revision: 14
author: CarlRabeler
ms.author: carlrab
manager: craigg
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: 5e59dcd6550c006b5a1e0f3e3be6440669e05021
ms.sourcegitcommit: 7019ac41524bdf783ea2c129c17b54581951b515
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/23/2018
---
# <a name="sysgeoreplicationlinks-azure-sql-database"></a>sys.geo_replication_links (banco de dados do SQL Azure)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  Contém uma linha para cada link de replicação entre bancos de dados primários e secundários em uma parceria de replicação geográfica. Essa exibição reside no banco de dados mestre lógico.  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|database_id|**Int**|ID do banco de dados atual no modo de exibição de sys. Databases.|  
|start_date|**datetimeoffset**|Hora UTC em um datacenter regional do banco de dados SQL quando a replicação de banco de dados foi iniciada|  
|modify_date|**datetimeoffset**|Hora UTC no datacenter regional do banco de dados SQL quando a replicação geográfica do banco de dados foi concluída. O novo banco de dados está sincronizado com o banco de dados primário a partir desse momento. .|  
|link_guid|**uniqueidentifier**|ID exclusiva do link de replicação geográfica.|  
|partner_server|**sysname**|Nome do servidor lógico que contém o banco de dados replicada geograficamente.|  
|partner_database|**sysname**|Nome do banco de dados replicada geograficamente no servidor lógico vinculado.|  
|replication_state|**tinyint**|O estado de replicação geográfica para este banco de dados, um de:.<br /><br /> 0 = pendente. Criação de banco de dados secundário ativo está agendada, mas as etapas de preparação necessárias ainda não foram concluídas.<br /><br /> 1 = propagação. O destino de replicação geográfica está sendo propagado mas dois bancos de dados ainda não estão sincronizados. Até que a propagação seja concluída, você não pode se conectar ao banco de dados secundário. Remover o banco de dados secundário do primário cancelará a operação de propagação.<br /><br /> 2 = varredura. O banco de dados secundário está em um estado transacionalmente consistente e está sendo constantemente sincronizado com o banco de dados primário.|  
|replication_state_desc|**nvarchar(256)**|PENDING<br /><br /> SEEDING<br /><br /> CATCH_UP|  
|função|**tinyint**|Função de replicação geográfica, um de:<br /><br /> 0 = primário. O database_id refere-se ao banco de dados primário na parceria de replicação geográfica.<br /><br /> 1 = secundário.  O database_id refere-se ao banco de dados primário na parceria de replicação geográfica.|  
|role_desc|**nvarchar(256)**|PRIMARY<br /><br /> SECONDARY|  
|secondary_allow_connections|**tinyint**|O tipo de secundário, um de:<br /><br /> 0 = Não. O banco de dados secundário não está acessível até que o failover.<br /><br /> 1 = somente leitura. O banco de dados secundário é acessível somente para conexões de cliente com ApplicationIntent = ReadOnly.<br /><br /> 2 = Todos. O banco de dados secundário é acessível para qualquer conexão de cliente.|  
|secondary_allow_connections _desc|**nvarchar(256)**|não<br /><br /> Todos<br /><br /> Somente leitura|  
  
## <a name="permissions"></a>Permissões  
 Essa exibição só está disponível na **mestre** banco de dados para o logon principal no nível de servidor.  
  
## <a name="example"></a>Exemplo  
 Mostre todos os bancos de dados com links de replicação geográfica.  
  
```  
SELECT   
     database_id  
   , start_date  
   , partner_server  
   , partner_database  
   , replication_state  
   , role_desc  
   , secondary_allow_connections_desc   
FROM sys.geo_replication_links;  
```  
  
## <a name="see-also"></a>Consulte também  
 [ALTER DATABASE (Banco de Dados SQL do Azure)](../../t-sql/statements/alter-database-azure-sql-database.md)   
 [sys.dm_geo_replication_link_status &#40;banco de dados do SQL Azure&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-geo-replication-link-status-azure-sql-database.md)   
 [sys.DM operation_status &#40;banco de dados do SQL Azure&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-operation-status-azure-sql-database.md)  
  
  
