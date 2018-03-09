---
title: MSpeer_lsns (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-tables
ms.reviewer: 
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- MSpeer_lsns
- MSpeer_lsns_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSpeer_lsns system table
ms.assetid: 0ba33907-601b-4c3d-8099-2663f680a161
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 31b5b65ff2dd13015e8ec0a53a2c6377d6c8aa58
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="mspeerlsns-transact-sql"></a>MSpeer_lsns (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  O **Mspeer_lsns** tabela é usada para mapear cada transação para uma assinatura em uma topologia de replicação ponto a ponto. Essa tabela é armazenada em cada banco de dados de publicação em uma topologia de replicação ponto a ponto, e no banco de dados de assinatura de todos os Assinantes de uma publicação ponto a ponto. Para obter mais informações sobre esse tipo de topologia de replicação transacional, consulte [replicação transacional ponto a ponto](../../relational-databases/replication/transactional/peer-to-peer-transactional-replication.md). Essa tabela é armazenada no banco de dados de publicação.  
  
## <a name="definition"></a>Definição  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**id**|**int**|Identifica um LSN ponto a ponto.|  
|**last_updated**|**datetime**|O **datetime** no qual foi feita a última atualização de linha.|  
|**originador**|**sysname**|O nome do Publicador que originou a transação.|  
|**originator_db**|**sysname**|O nome do banco de dados de origem da transação.|  
|**originator_publication**|**sysname**|O nome da publicação de origem da transação.|  
|**originator_publication_id**|**int**|O identificador da publicação de origem da transação.|  
|**originator_db_version**|**int**|Identifica o número da versão do banco de dados de origem.|  
|**originator_lsn**|**int**|Identifica o LSN na publicação de origem.|  
|**originator_version**|**int**|Identifica o número da versão do Publicador.|  
|**originator_id**|**smallint**|Identifica cada nó na topologia com a finalidade de detecção de conflito. Para obter mais informações, consulte [Conflict Detection in Peer-to-Peer Replication](../../relational-databases/replication/transactional/peer-to-peer-conflict-detection-in-peer-to-peer-replication.md).|  
  
## <a name="see-also"></a>Consulte também  
 [Tabelas de replicação &#40; Transact-SQL &#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Exibições de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
