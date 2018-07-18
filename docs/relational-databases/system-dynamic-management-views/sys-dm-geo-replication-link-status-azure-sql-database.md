---
title: DM geo_replication_link_status (banco de dados SQL) | Microsoft Docs
ms.custom: ''
ms.date: 10/13/2016
ms.prod: ''
ms.prod_service: sql-database
ms.reviewer: ''
ms.service: sql-database
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
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
caps.latest.revision: 15
author: CarlRabeler
ms.author: carlrab
manager: craigg
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: ac416ef7d48655e25002646b6e364d04982688b2
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2018
ms.locfileid: "38046044"
---
# <a name="sysdmgeoreplicationlinkstatus-azure-sql-database"></a>DM geo_replication_link_status (banco de dados SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  Contém uma linha para cada link de replicação entre bancos de dados primários e secundários em uma parceria de replicação geográfica. Isso inclui bancos de dados primários e secundários. Se houver mais de um link de replicação contínua para um determinado banco de dados primário, esta tabela contém uma linha para cada uma das relações. A exibição é criada em todos os bancos de dados, incluindo o mestre lógico. No entanto, a consulta dessa exibição no mestre lógico retorna um conjunto vazio.  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|link_guid|**uniqueidentifier**|ID exclusiva do link de replicação.|  
|partner_server|**sysname**|Nome do servidor lógico que contém o banco de dados vinculado.|  
|partner_database|**sysname**|Nome do banco de dados vinculado no servidor lógico vinculado.|  
|last_replication|**datetimeoffset**|O carimbo de hora da confirmação da última transação pelo secundário com base no relógio do banco de dados primário. Esse valor está disponível no banco de dados primário somente.|  
|replication_lag_sec|**int**|Diferença de tempo em segundos entre o valor de last_replication e o carimbo de hora da confirmação da transação na réplica primária com base no relógio do banco de dados primário.  Esse valor está disponível no banco de dados primário somente.|  
|replication_state|**tinyint**|O estado de replicação geográfica para esse banco de dados, um dos:.<br /><br /> 1 = propagação. O destino de replicação geográfica está sendo propagado, mas os dois bancos de dados ainda não estão sincronizados. Até que a propagação seja concluída, você não pode se conectar ao banco de dados secundário. Remover banco de dados secundário do primário cancelará a operação de propagação.<br /><br /> 2 = recuperar o atraso. O banco de dados secundário está em um estado transacionalmente consistente e está sendo constantemente sincronizado com o banco de dados primário.<br /><br /> 4 = Suspended. Isso não é uma relação de cópia contínua ativa. Esse estado geralmente indica que a largura de banda disponível para o interlink é insuficiente para o nível de atividade da transação no banco de dados primário. No entanto, a relação de cópia contínua ainda permanece intacta.|  
|replication_state_desc|**nvarchar(256)**|PENDING<br /><br /> SEEDING<br /><br /> CATCH_UP|  
|função|**tinyint**|Função de replicação geográfica, um dos:<br /><br /> 0 = primary. O database_id refere-se ao banco de dados primário na parceria de replicação geográfica.<br /><br /> 1 = secundário.  O database_id refere-se ao banco de dados primário na parceria de replicação geográfica.|  
|role_desc|**nvarchar(256)**|PRIMARY<br /><br /> SECONDARY|  
|secondary_allow_connections|**tinyint**|O tipo de secundário, um dos:<br /><br /> 0 não = nenhuma direct conexões são permitidas para o banco de dados secundário e o banco de dados não está disponível para acesso de leitura.<br /><br /> 2 = todas as conexões são permitidas no banco de dados no secundário repl; Autent para acesso somente leitura.|  
|secondary_allow_connections_desc|**nvarchar(256)**|não<br /><br /> Todos|  
|last_commit|**datetimeoffset**|A hora da última transação confirmada no banco de dados. Se recuperado no banco de dados primário, ele indica a hora da última confirmação no banco de dados primário. Se recuperado no banco de dados secundário, ele indica a hora da última confirmação no banco de dados secundário. Se recuperado no banco de dados secundário quando o primário do link de replicação está inativo, ele indica até que ponto o secundário for atualizado.|
  
> [!NOTE]  
>  Se a relação de replicação é encerrada, removendo o banco de dados secundário (seção 4.2), a linha desse banco de dados na **DM geo_replication_link_status** desaparece da exibição.  
  
## <a name="permissions"></a>Permissões  
 Qualquer conta com permissão de view_database_state pode consultar **DM geo_replication_link_status**.  
  
## <a name="example"></a>Exemplo  
 Mostra intervalos de replicação e a hora da última replicação dos meus bancos de dados secundários.  
  
```  
SELECT   
     link_guid  
   , partner_server  
   , last_replication  
   , replication_lag_sec   
FROM sys.dm_geo_replication_link_status;  
```  
  
## <a name="see-also"></a>Consulte também  
 [ALTER DATABASE &#40;banco de dados SQL do Azure&#41;](../../t-sql/statements/alter-database-azure-sql-database.md)   
 [sys. geo_replication_links &#40;banco de dados SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-geo-replication-links-azure-sql-database.md)   
 [DM operation_status &#40;banco de dados SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-operation-status-azure-sql-database.md)  
  
  
