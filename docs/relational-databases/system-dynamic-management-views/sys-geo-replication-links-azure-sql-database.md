---
title: sys. geo_replication_links (banco de dados SQL do Azure) | Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68043166"
---
# <a name="sysgeo_replication_links-azure-sql-database"></a>sys.geo_replication_links (Banco de Dados SQL do Azure)

[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  Contém uma linha para cada link de replicação entre bancos de dados primários e secundários em uma parceria de replicação geográfica. Essa exibição reside no banco de dados mestre lógico.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|database_id|**int**|ID do banco de dados atual na exibição sys. databases.|  
|start_date|**datetimeoffset**|Hora UTC em um datacenter de banco de dados SQL regional quando a replicação de banco de dados foi iniciada|  
|modify_date|**datetimeoffset**|Hora UTC no datacenter do banco de dados SQL regional quando a replicação geográfica do banco de dados for concluída. O novo banco de dados é sincronizado com o banco de dados primário a partir deste momento. .|  
|link_guid|**uniqueidentifier**|ID exclusiva do link de replicação geográfica.|  
|partner_server|**sysname**|Nome do servidor do banco de dados SQL que contém o banco de dados replicado geograficamente.|  
|partner_database|**sysname**|Nome do banco de dados replicado geograficamente no servidor de banco de dados SQL vinculado.|  
|replication_state|**tinyint**|O estado de replicação geográfica para este banco de dados, um dos:.<br /><br /> 0 = pendente. A criação do banco de dados secundário ativo está agendada, mas as etapas de preparação necessárias ainda não foram concluídas.<br /><br /> 1 = propagação. O destino de replicação geográfica está sendo propagado, mas os dois bancos de dados ainda não estão sincronizados. Até que a propagação seja concluída, você não poderá se conectar ao banco de dados secundário. Remover o banco de dados secundário do primário cancelará a operação de propagação.<br /><br /> 2 = atualização. O banco de dados secundário está em um estado transacionalmente consistente e está sendo constantemente sincronizado com o banco de dados primário.|  
|replication_state_desc|**nvarchar(256)**|PENDING<br /><br /> SEEDING<br /><br /> CATCH_UP|  
|função|**tinyint**|Função de replicação geográfica, uma das:<br /><br /> 0 = primário. O database_id refere-se ao banco de dados primário na parceria de replicação geográfica.<br /><br /> 1 = secundário.  O database_id refere-se ao banco de dados primário na parceria de replicação geográfica.|  
|role_desc|**nvarchar(256)**|PRIMARY<br /><br /> SECONDARY|  
|secondary_allow_connections|**tinyint**|O tipo secundário, um de:<br /><br /> 0 = Não. O banco de dados secundário não estará acessível até o failover.<br /><br /> 1 = ReadOnly. O banco de dados secundário é acessível somente para conexões de cliente com ApplicationIntent = ReadOnly.<br /><br /> 2 = Todos. O banco de dados secundário pode ser acessado por qualquer conexão de cliente.|  
|secondary_allow_connections _desc|**nvarchar(256)**|Não<br /><br /> Todos<br /><br /> Somente leitura|  
  
## <a name="permissions"></a>Permissões

Essa exibição só está disponível no banco de dados **mestre** para o logon da entidade de segurança no nível do servidor.  
  
## <a name="example"></a>Exemplo

Mostrar todos os bancos de dados com links de replicação geográfica.  

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

## <a name="see-also"></a>Consulte Também

 [ALTER DATABASE (banco de dados SQL do Azure)](../../t-sql/statements/alter-database-azure-sql-database.md)   
 [sys. dm_geo_replication_link_status &#40;banco de dados SQL do Azure&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-geo-replication-link-status-azure-sql-database.md)   
 [sys. dm_operation_status &#40;banco de dados SQL do Azure&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-operation-status-azure-sql-database.md)  
