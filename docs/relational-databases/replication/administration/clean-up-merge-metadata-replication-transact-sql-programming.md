---
title: "Limpar metadados de mesclagem (Programa&#231;&#227;o Transact-SQL de replica&#231;&#227;o) | Microsoft Docs"
ms.custom: ""
ms.date: "03/03/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "TSQL"
helpviewer_keywords: 
  - "metadados [replicação do SQL Server]"
  - "sp_mergemetadataretentioncleanup"
ms.assetid: 9b88baea-b7c6-4e5d-88f9-93d6a0ff0368
caps.latest.revision: 33
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 33
---
# Limpar metadados de mesclagem (Programa&#231;&#227;o Transact-SQL de replica&#231;&#227;o)
  Os metadados de replicação de mesclagem são limpados periodicamente pelo Agente de Mesclagem com base na configuração de retenção para a publicação. Isso ocorre no publicador e assinante no [MSmerge_genhistory](../../../relational-databases/system-tables/msmerge-genhistory-transact-sql.md), [MSmerge_contents](../../../relational-databases/system-tables/msmerge-contents-transact-sql.md), [MSmerge_tombstone](../../../relational-databases/system-tables/msmerge-tombstone-transact-sql.md), [MSmerge_past_partition_mappings](../../../relational-databases/system-tables/msmerge-past-partition-mappings-transact-sql.md), e [MSmerge_current_partition_mappings](../../../relational-databases/system-tables/msmerge-current-partition-mappings.md) tabelas do sistema. Também é possível limpar programaticamente os dados nessas tabelas usando procedimentos armazenados de replicação.  
  
### Para limpar os metadados de mesclagem manualmente  
  
1.  No publicador do banco de dados de publicação, execute [sp_mergemetadataretentioncleanup](../../../relational-databases/system-stored-procedures/sp-mergemetadataretentioncleanup-transact-sql.md).  
  
2.  (Opcional) Observe que o número de linhas removidas na etapa 1 do [MSmerge_genhistory](../../../relational-databases/system-tables/msmerge-genhistory-transact-sql.md), [MSmerge_contents](../../../relational-databases/system-tables/msmerge-contents-transact-sql.md), e [MSmerge_tombstone](../../../relational-databases/system-tables/msmerge-tombstone-transact-sql.md) tabelas do sistema, retornadas respectivamente no **@num_genhistory_rows**, **@num_contents_rows**, e **@num_tombstone_rows** parâmetros de saída.  
  
3.  Repita as etapas 1 e 2 no Assinante para limpar os metadados no banco de dados de assinatura.  
  
## Consulte também  
 [Validade e desativação de assinatura](../../../relational-databases/replication/subscription-expiration-and-deactivation.md)  
  
  