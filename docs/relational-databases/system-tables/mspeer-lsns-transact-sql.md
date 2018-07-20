---
title: MSpeer_lsns (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-tables
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
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
caps.latest.revision: 33
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: de37f4de25bef419c67af1ff858251bec4b5e543
ms.sourcegitcommit: a431ca21eac82117492d7b84c398ddb3fced53cc
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/17/2018
ms.locfileid: "39101994"
---
# <a name="mspeerlsns-transact-sql"></a>MSpeer_lsns (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  O **Mspeer_lsns** tabela é usada para mapear cada transação para uma assinatura em uma topologia de replicação ponto a ponto. Essa tabela é armazenada em cada banco de dados de publicação em uma topologia de replicação ponto a ponto, e no banco de dados de assinatura de todos os Assinantes de uma publicação ponto a ponto. Para obter mais informações sobre esse tipo de topologia de replicação transacional, consulte [a replicação transacional ponto a ponto](../../relational-databases/replication/transactional/peer-to-peer-transactional-replication.md). Essa tabela é armazenada no banco de dados de publicação.  
  
## <a name="definition"></a>Definição  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**id**|**int**|Identifica um LSN ponto a ponto.|  
|**last_updated**|**datetime**|O **datetime** no qual foi feita a última atualização de linha.|  
|**originator**|**sysname**|O nome do Publicador que originou a transação.|  
|**originator_db**|**sysname**|O nome do banco de dados de origem da transação.|  
|**originator_publication**|**sysname**|O nome da publicação de origem da transação.|  
|**originator_publication_id**|**int**|O identificador da publicação de origem da transação.|  
|**originator_db_version**|**int**|Identifica o número da versão do banco de dados de origem.|  
|**originator_lsn**|**int**|Identifica o LSN na publicação de origem.|  
|**originator_version**|**int**|Identifica o número da versão do Publicador.|  
|**originator_id**|**smallint**|Identifica cada nó na topologia com a finalidade de detecção de conflito. Para obter mais informações, consulte [Conflict Detection in Peer-to-Peer Replication](../../relational-databases/replication/transactional/peer-to-peer-conflict-detection-in-peer-to-peer-replication.md).|  
  
## <a name="see-also"></a>Consulte também  
 [Tabelas de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Exibições de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
