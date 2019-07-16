---
title: sys. geo_replication_links (banco de dados SQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/28/2019
ms.service: sql-database
ms.reviewer: ''
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
author: mashamsft
ms.author: mathoma
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: 6e768f447cd53321861eae91bbe40e2e34ad12f8
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68043166"
---
# <a name="sysgeoreplicationlinks-azure-sql-database"></a>sys.geo_replication_links (Banco de Dados SQL do Azure)

[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  Contém uma linha para cada link de replicação entre bancos de dados primários e secundários em uma parceria de replicação geográfica. Essa exibição reside no banco de dados mestre lógico.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|database_id|**int**|ID do banco de dados atual no modo de exibição de sys. Databases.|  
|start_date|**datetimeoffset**|Hora UTC em um datacenter regional do banco de dados SQL quando a replicação de banco de dados foi iniciada|  
|modify_date|**datetimeoffset**|Hora do UTC no datacenter regional do banco de dados SQL quando a replicação geográfica do banco de dados foi concluída. O novo banco de dados está sincronizado com o banco de dados primário a partir desse momento. .|  
|link_guid|**uniqueidentifier**|ID exclusiva do link de replicação geográfica.|  
|partner_server|**sysname**|Nome do servidor de banco de dados SQL que contém o banco de dados replicado geograficamente.|  
|partner_database|**sysname**|Nome do banco de dados com replicação geográfica no servidor de banco de dados SQL vinculado.|  
|replication_state|**tinyint**|O estado de replicação geográfica para esse banco de dados, um dos:.<br /><br /> 0 = pendente. A criação do banco de dados secundário ativo está agendada, mas as etapas de preparação necessárias ainda não foram concluídas.<br /><br /> 1 = propagação. O destino de replicação geográfica está sendo propagado, mas os dois bancos de dados ainda não estão sincronizados. Até que a propagação seja concluída, você não pode se conectar ao banco de dados secundário. Remover banco de dados secundário do primário cancelará a operação de propagação.<br /><br /> 2 = recuperar o atraso. O banco de dados secundário está em um estado transacionalmente consistente e está sendo constantemente sincronizado com o banco de dados primário.|  
|replication_state_desc|**nvarchar(256)**|PENDING<br /><br /> SEEDING<br /><br /> CATCH_UP|  
|role|**tinyint**|Função de replicação geográfica, um dos:<br /><br /> 0 = primary. O database_id refere-se ao banco de dados primário na parceria de replicação geográfica.<br /><br /> 1 = secundário.  O database_id refere-se ao banco de dados primário na parceria de replicação geográfica.|  
|role_desc|**nvarchar(256)**|PRIMARY<br /><br /> SECONDARY|  
|secondary_allow_connections|**tinyint**|O tipo de secundário, um dos:<br /><br /> 0 = Não. O banco de dados secundário não está acessível até que o failover.<br /><br /> 1 = somente leitura. O banco de dados secundário é acessível somente para conexões de cliente com ApplicationIntent = ReadOnly.<br /><br /> 2 = Todos. O banco de dados secundário é acessível a qualquer conexão de cliente.|  
|secondary_allow_connections _desc|**nvarchar(256)**|Não<br /><br /> Todos<br /><br /> Somente leitura|  
  
## <a name="permissions"></a>Permissões

Essa exibição só está disponível na **mestre** banco de dados para o logon principal no nível do servidor.  
  
## <a name="example"></a>Exemplo

Mostra todos os bancos de dados com links de replicação geográfica.  

```sql
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
 [DM geo_replication_link_status &#40;banco de dados SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-geo-replication-link-status-azure-sql-database.md)   
 [DM operation_status &#40;banco de dados SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-operation-status-azure-sql-database.md)  
