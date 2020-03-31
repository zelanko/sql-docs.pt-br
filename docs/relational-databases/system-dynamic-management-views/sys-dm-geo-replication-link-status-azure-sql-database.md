---
title: sys.dm_geo_replication_link_status
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
ms.openlocfilehash: 8bdf74e6ee774d9a0cc8e3d9128c659b75287511
ms.sourcegitcommit: d1f6da6f0f5e9630261cf733c64958938a3eb859
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/12/2020
ms.locfileid: "79198221"
---
# <a name="sysdm_geo_replication_link_status-azure-sql-database"></a>sys.dm_geo_replication_link_status (Banco de Dados SQL do Azure)

[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  Contém uma linha para cada link de replicação entre bancos de dados primários e secundários em uma parceria de geo-replicação. Isso inclui os bancos de dados primários e secundários. Se houver mais de um link de replicação contínua para um determinado banco de dados primário, essa tabela conterá uma linha para cada uma das relações. A exibição é criada em todos os bancos de dados, incluindo o mestre lógico. No entanto, a consulta dessa exibição no mestre lógico retorna um conjunto vazio.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|link_guid|**Uniqueidentifier**|ID exclusivo do link de replicação.|  
|partner_server|**Sysname**|Nome do servidor SQL Database contendo o banco de dados vinculado.|  
|partner_database|**Sysname**|Nome do banco de dados vinculado no servidor do Banco de Dados SQL.|  
|last_replication|**Datetimeoffset**|O carimbo de data e hora do reconhecimento da última transação pelo secundário com base no relógio de banco de dados primário. Este valor está disponível apenas no banco de dados principal.|  
|replication_lag_sec|**Int**|Diferença de tempo em segundos entre o valor last_replication e o carimbo de tempo do compromisso dessa transação no principal com base no relógio de banco de dados principal.  Este valor está disponível apenas no banco de dados principal.|  
|replication_state|**Tinyint**|O estado de geo-replicação para este banco de dados, um dos mais.<br /><br /> 1 = Semeada. O alvo de geo-replicação está sendo semeado, mas os dois bancos de dados ainda não estão sincronizados. Até que a semeadura seja concluída, você não pode se conectar ao banco de dados secundário. A remoção do banco de dados secundário da primária cancelará a operação de semeação.<br /><br /> 2 = Catch-up. O banco de dados secundário está em um estado transamente consistente e está sendo constantemente sincronizado com o banco de dados principal.<br /><br /> 4 = Suspenso. Esta não é uma relação de cópia contínua ativa. Esse estado geralmente indica que a largura de banda disponível para o interlink é insuficiente para o nível de atividade da transação no banco de dados primário. No entanto, a relação de cópia contínua ainda permanece intacta.|  
|replication_state_desc|**nvarchar(256)**|PENDING<br /><br /> SEEDING<br /><br /> CATCH_UP|  
|função|**Tinyint**|Função de geo-replicação, uma das:<br /><br /> 0 = Primário. O database_id refere-se ao banco de dados primário na parceria de georeplicação.<br /><br /> 1 = Secundário.  O database_id refere-se ao banco de dados primário na parceria de georeplicação.|  
|role_desc|**nvarchar(256)**|PRIMARY<br /><br /> SECONDARY|  
|secondary_allow_connections|**Tinyint**|O tipo secundário, um de:<br /><br /> 0 = Não são permitidas conexões diretas ao banco de dados secundário e o banco de dados não está disponível para acesso à leitura.<br /><br /> 2 = Todas as conexões são permitidas ao banco de dados no repl;ication secundário para acesso somente leitura.|  
|secondary_allow_connections_desc|**nvarchar(256)**|Não<br /><br /> Todos|  
|last_commit|**Datetimeoffset**|O tempo da última transação comprometida com o banco de dados. Se recuperado no banco de dados principal, ele indica o último tempo de confirmação no banco de dados principal. Se recuperado no banco de dados secundário, ele indica o último tempo de confirmação no banco de dados secundário. Se recuperado no banco de dados secundário quando o principal do link de replicação estiver desligado, ele indica até que ponto o secundário foi alcançado.|
  
> [!NOTE]  
>  Se a relação de replicação for encerrada removendo o banco de dados secundário (seção 4.2), a linha para esse banco de dados na exibição **sys.dm_geo_replication_link_status** desaparece.  
  
## <a name="permissions"></a>Permissões  
 Qualquer conta com permissão view_database_state pode consultar **sys.dm_geo_replication_link_status**.  
  
## <a name="example"></a>Exemplo  
 Mostrar atrasos de replicação e o tempo de replicação final dos meus bancos de dados secundários.  
  
```  
SELECT   
     link_guid  
   , partner_server  
   , last_replication  
   , replication_lag_sec   
FROM sys.dm_geo_replication_link_status;  
```  
  
## <a name="see-also"></a>Consulte também  
 [BANCO DE DADOS ALTER &#40;&#41;de banco de dados SQL do Azure](../../t-sql/statements/alter-database-azure-sql-database.md)   
 [sys.geo_replication_links &#40;&#40;&#41;de banco de dados SQL Do Azure](../../relational-databases/system-dynamic-management-views/sys-geo-replication-links-azure-sql-database.md)   
 [sys.dm_operation_status &#40;&#41;de banco de dados SQL Do Azure](../../relational-databases/system-dynamic-management-views/sys-dm-operation-status-azure-sql-database.md)   
 [sp_wait_for_database_copy_sync](../system-stored-procedures/active-geo-replication-sp-wait-for-database-copy-sync.md)
  
