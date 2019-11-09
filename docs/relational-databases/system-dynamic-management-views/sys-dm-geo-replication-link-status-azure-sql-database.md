---
title: sys. dm_geo_replication_link_status
titleSuffix: Azure SQL Database
ms.date: 01/28/2019
ms.service: sql-database
ms.reviewer: ''
ms.topic: conceptual
f1_keywords:
- dm_geo_replication_link_status
- dm_geo_replication_link_status_TSQL
- sys.dm_geo_replication_link_status
- sys.dm_geo_replication_link_status_TSQL
helpviewer_keywords:
- dm_geo_replication_link_status dynamic management view
- sys.dm_geo_replication_link_status dynamic management view
ms.assetid: d763d679-470a-4c21-86ab-dfe98d37e9fd
author: mashamsft
ms.author: mathoma
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.custom: seo-dt-2019
ms.openlocfilehash: e642fada95ddf20e81f9fcb7da8b6267469ef0c9
ms.sourcegitcommit: f688a37bb6deac2e5b7730344165bbe2c57f9b9c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/08/2019
ms.locfileid: "73843893"
---
# <a name="sysdm_geo_replication_link_status-azure-sql-database"></a>sys.dm_geo_replication_link_status (Banco de Dados SQL do Azure)

[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  Contém uma linha para cada link de replicação entre bancos de dados primários e secundários em uma parceria de replicação geográfica. Isso inclui bancos de dados primários e secundários. Se houver mais de um link de replicação contínua para um determinado banco de dados primário, essa tabela conterá uma linha para cada uma das relações. A exibição é criada em todos os bancos de dados, incluindo o mestre lógico. No entanto, a consulta dessa exibição no mestre lógico retorna um conjunto vazio.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|link_guid|**uniqueidentifier**|ID exclusiva do link de replicação.|  
|partner_server|**sysname**|Nome do servidor do banco de dados SQL que contém o banco de dados vinculado.|  
|partner_database|**sysname**|Nome do banco de dados vinculado no servidor do Banco de Dados SQL.|  
|last_replication|**datetimeoffset**|O carimbo de data/hora da última confirmação da transação pelo secundário com base no relógio do banco de dados primário. Esse valor está disponível somente no banco de dados primário.|  
|replication_lag_sec|**int**|Diferença de tempo em segundos entre o valor de last_replication e o carimbo de data/hora da confirmação da transação no primário com base no relógio do banco de dados primário.  Esse valor está disponível somente no banco de dados primário.|  
|replication_state|**tinyint**|O estado de replicação geográfica para este banco de dados, um dos:.<br /><br /> 1 = propagação. O destino de replicação geográfica está sendo propagado, mas os dois bancos de dados ainda não estão sincronizados. Até que a propagação seja concluída, você não poderá se conectar ao banco de dados secundário. Remover o banco de dados secundário do primário cancelará a operação de propagação.<br /><br /> 2 = atualização. O banco de dados secundário está em um estado transacionalmente consistente e está sendo constantemente sincronizado com o banco de dados primário.<br /><br /> 4 = suspenso. Essa não é uma relação de cópia contínua ativa. Esse estado geralmente indica que a largura de banda disponível para o interlink é insuficiente para o nível de atividade da transação no banco de dados primário. No entanto, a relação de cópia contínua ainda permanece intacta.|  
|replication_state_desc|**nvarchar(256)**|PENDING<br /><br /> SEEDING<br /><br /> CATCH_UP|  
|função|**tinyint**|Função de replicação geográfica, uma das:<br /><br /> 0 = primário. O database_id refere-se ao banco de dados primário na parceria de replicação geográfica.<br /><br /> 1 = secundário.  O database_id refere-se ao banco de dados primário na parceria de replicação geográfica.|  
|role_desc|**nvarchar(256)**|PRIMARY<br /><br /> SECONDARY|  
|secondary_allow_connections|**tinyint**|O tipo secundário, um de:<br /><br /> 0 = nenhuma conexão direta é permitida para o banco de dados secundário e o banco de dados não está disponível para acesso de leitura.<br /><br /> 2 = todas as conexões são permitidas para o banco de dados no repl secundário; vo para acesso somente leitura.|  
|secondary_allow_connections_desc|**nvarchar(256)**|Não<br /><br /> Todos|  
|last_commit|**datetimeoffset**|A hora da última transação confirmada no banco de dados. Se for recuperado no banco de dados primário, ele indica a hora da última confirmação no banco de dados primário. Se for recuperado no banco de dados secundário, ele indica a hora da última confirmação no banco de dados secundário. Se for recuperado no banco de dados secundário quando o primário do link de replicação estiver inativo, ele indicará até que ponto o secundário foi pego.|
  
> [!NOTE]  
>  Se a relação de replicação for encerrada com a remoção do banco de dados secundário (seção 4,2), a linha desse banco de dados na exibição **Sys. dm_geo_replication_link_status** desaparecerá.  
  
## <a name="permissions"></a>Permissões  
 Qualquer conta com view_database_state permissão pode consultar **Sys. dm_geo_replication_link_status**.  
  
## <a name="example"></a>Exemplo  
 Mostrar atraso de replicação e tempo da última replicação dos meus bancos de dados secundários.  
  
```  
SELECT   
     link_guid  
   , partner_server  
   , last_replication  
   , replication_lag_sec   
FROM sys.dm_geo_replication_link_status;  
```  
  
## <a name="see-also"></a>Consulte também  
 [ALTER DATABASE &#40;banco de dados&#41; SQL do Azure](../../t-sql/statements/alter-database-azure-sql-database.md)   
 [Sys. geo_replication_links &#40;banco de dados&#41; SQL do Azure](../../relational-databases/system-dynamic-management-views/sys-geo-replication-links-azure-sql-database.md)   
 [sys. dm_operation_status &#40;banco de dados SQL do Azure&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-operation-status-azure-sql-database.md)  
  
  
