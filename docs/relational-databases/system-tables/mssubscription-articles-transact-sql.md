---
title: MSsubscription_articles (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology:
- replication
ms.topic: language-reference
f1_keywords:
- MSsubscription_articles
- MSsubscription_articles_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSsubscription_articles system table
ms.assetid: dbc1737f-261e-4017-b9cd-703b9fc4ac78
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 767df03bda9a11ce629244b15e83b7dc676894a9
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47691743"
---
# <a name="mssubscriptionarticles-transact-sql"></a>MSsubscription_articles (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  O **MSsubscription_articles** tabela contém informações sobre os artigos em uma assinatura enfileirada. Essa tabela só é populada para tipos de replicação de atualização enfileirada e atualização imediata com atualização enfileirada como um failover.  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**agent_id**|**int**|A ID do agente que serve a este artigo|  
|**artid**|**int**|A ID do artigo do **sysarticles** tabela.|  
|**article**|**sysname**|O nome do artigo dos **sysarticles** tabela.|  
|**dest_table**|**sysname**|O nome da tabela de destino a partir de **sysarticles** tabela.|  
|**Proprietário**|**sysname**|O proprietário da assinatura.|  
|**cft_table**|**sysname**|O nome da tabela de conflito para este artigo, para tipo de replicação de atualização enfileirada.|  
  
## <a name="see-also"></a>Consulte também  
 [Tabelas de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Exibições de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
