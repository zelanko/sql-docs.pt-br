---
title: MSpeer_lsns (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSpeer_lsns
- MSpeer_lsns_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSpeer_lsns system table
ms.assetid: 0ba33907-601b-4c3d-8099-2663f680a161
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 38efa38b53a089f960311e415d42972599872fcc
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/05/2020
ms.locfileid: "82832266"
---
# <a name="mspeer_lsns-transact-sql"></a>MSpeer_lsns (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  A tabela **MSpeer_lsns** é usada para mapear cada transação para uma assinatura em uma topologia de replicação ponto a ponto. Essa tabela é armazenada em cada banco de dados de publicação em uma topologia de replicação ponto a ponto, e no banco de dados de assinatura de todos os Assinantes de uma publicação ponto a ponto. Para obter mais informações sobre esse tipo de topologia de replicação transacional, consulte [replicação transacional ponto a ponto](../../relational-databases/replication/transactional/peer-to-peer-transactional-replication.md). Essa tabela é armazenada no banco de dados de publicação.  
  
## <a name="definition"></a>Definição  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**id**|**int**|Identifica um LSN ponto a ponto.|  
|**last_updated**|**datetime**|O **DateTime** no qual a última atualização de linha foi feita.|  
|**autor**|**sysname**|O nome do Publicador que originou a transação.|  
|**originator_db**|**sysname**|O nome do banco de dados de origem da transação.|  
|**originator_publication**|**sysname**|O nome da publicação de origem da transação.|  
|**originator_publication_id**|**int**|O identificador da publicação de origem da transação.|  
|**originator_db_version**|**int**|Identifica o número da versão do banco de dados de origem.|  
|**originator_lsn**|**int**|Identifica o LSN na publicação de origem.|  
|**originator_version**|**int**|Identifica o número da versão do Publicador.|  
|**originator_id**|**smallint**|Identifica cada nó na topologia com a finalidade de detecção de conflito. Para obter mais informações, consulte [Conflict Detection in Peer-to-Peer Replication](../../relational-databases/replication/transactional/peer-to-peer-conflict-detection-in-peer-to-peer-replication.md).|  
  
## <a name="see-also"></a>Consulte Também  
 [Tabelas de replicação &#40;&#41;Transact-SQL](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Exibições de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
