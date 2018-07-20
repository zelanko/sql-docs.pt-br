---
title: MSsubscription_articles (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
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
- MSsubscription_articles
- MSsubscription_articles_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSsubscription_articles system table
ms.assetid: dbc1737f-261e-4017-b9cd-703b9fc4ac78
caps.latest.revision: 26
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: ff060482ddd1b9a678cdd37a9f4f2d1f26077272
ms.sourcegitcommit: a431ca21eac82117492d7b84c398ddb3fced53cc
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/17/2018
ms.locfileid: "39103154"
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
  
  
