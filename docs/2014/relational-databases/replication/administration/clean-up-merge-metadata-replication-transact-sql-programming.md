---
title: Limpar metadados de mesclagem (programação de Transact-SQL de replicação) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
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
caps.latest.revision: 32
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: e1f5c0159c60db0ad8a51842d43293bc8175037a
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36021136"
---
# <a name="clean-up-merge-metadata-replication-transact-sql-programming"></a>Limpar metadados de mesclagem (Programação Transact-SQL de replicação)
  Os metadados de replicação de mesclagem são limpados periodicamente pelo Agente de Mesclagem com base na configuração de retenção para a publicação. Isso acontece no Publicador e Assinante no [MSmerge_genhistory](/sql/relational-databases/system-tables/msmerge-genhistory-transact-sql), [MSmerge_contents](/sql/relational-databases/system-tables/msmerge-contents-transact-sql), [MSmerge_tombstone](/sql/relational-databases/system-tables/msmerge-tombstone-transact-sql), [MSmerge_past_partition_mappings](/sql/relational-databases/system-tables/msmerge-past-partition-mappings-transact-sql)e nas tabelas do sistema [de MSmerge_current_partition_mappings](/sql/relational-databases/system-tables/msmerge-current-partition-mappings) . Também é possível limpar programaticamente os dados nessas tabelas usando procedimentos armazenados de replicação.  
  
### <a name="to-manually-clean-up-merge-metadata"></a>Para limpar os metadados de mesclagem manualmente  
  
1.  No Publicador do banco de dados de publicação, execute [sp_mergemetadataretentioncleanup](/sql/relational-databases/system-stored-procedures/sp-mergemetadataretentioncleanup-transact-sql).  
  
2.  (Opcional) Observe o número de linhas removidas na etapa 1 do [MSmerge_genhistory](/sql/relational-databases/system-tables/msmerge-genhistory-transact-sql), [MSmerge_contents](/sql/relational-databases/system-tables/msmerge-contents-transact-sql)e nas tabelas do sistema [MSmerge_tombstone](/sql/relational-databases/system-tables/msmerge-tombstone-transact-sql) , retornadas respectivamente nos parâmetros de saída **@num_genhistory_rows**, **@num_contents_rows**e nas tabelas do sistema **@num_tombstone_rows** .  
  
3.  Repita as etapas 1 e 2 no Assinante para limpar os metadados no banco de dados de assinatura.  
  
## <a name="see-also"></a>Consulte também  
 [Desativação e expiração de assinatura](../subscription-expiration-and-deactivation.md)  
  
  
