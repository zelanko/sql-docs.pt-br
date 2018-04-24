---
title: Limpar metadados de mesclagem (programação de Transact-SQL de replicação) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: replication
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: article
dev_langs:
- TSQL
helpviewer_keywords:
- metadata [SQL Server replication]
- sp_mergemetadataretentioncleanup
ms.assetid: 9b88baea-b7c6-4e5d-88f9-93d6a0ff0368
caps.latest.revision: 33
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: e070a61220b8ea2dcf5c5351c352b92a9309b99b
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="clean-up-merge-metadata-replication-transact-sql-programming"></a>Limpar metadados de mesclagem (Programação Transact-SQL de replicação)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Os metadados de replicação de mesclagem são limpados periodicamente pelo Agente de Mesclagem com base na configuração de retenção para a publicação. Isso acontece no Publicador e Assinante no [MSmerge_genhistory](../../../relational-databases/system-tables/msmerge-genhistory-transact-sql.md), [MSmerge_contents](../../../relational-databases/system-tables/msmerge-contents-transact-sql.md), [MSmerge_tombstone](../../../relational-databases/system-tables/msmerge-tombstone-transact-sql.md), [MSmerge_past_partition_mappings](../../../relational-databases/system-tables/msmerge-past-partition-mappings-transact-sql.md)e nas tabelas do sistema [de MSmerge_current_partition_mappings](../../../relational-databases/system-tables/msmerge-current-partition-mappings.md) . Também é possível limpar programaticamente os dados nessas tabelas usando procedimentos armazenados de replicação.  
  
### <a name="to-manually-clean-up-merge-metadata"></a>Para limpar os metadados de mesclagem manualmente  
  
1.  No Publicador do banco de dados de publicação, execute [sp_mergemetadataretentioncleanup](../../../relational-databases/system-stored-procedures/sp-mergemetadataretentioncleanup-transact-sql.md).  
  
2.  (Opcional) Observe o número de linhas removidas na etapa 1 do [MSmerge_genhistory](../../../relational-databases/system-tables/msmerge-genhistory-transact-sql.md), [MSmerge_contents](../../../relational-databases/system-tables/msmerge-contents-transact-sql.md)e nas tabelas do sistema [MSmerge_tombstone](../../../relational-databases/system-tables/msmerge-tombstone-transact-sql.md) , retornadas respectivamente nos parâmetros de saída **@num_genhistory_rows**, **@num_contents_rows**e nas tabelas do sistema **@num_tombstone_rows** .  
  
3.  Repita as etapas 1 e 2 no Assinante para limpar os metadados no banco de dados de assinatura.  
  
## <a name="see-also"></a>Consulte Também  
 [Desativação e expiração de assinatura](../../../relational-databases/replication/subscription-expiration-and-deactivation.md)  
  
  
