---
title: MSsubscription_articles (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSsubscription_articles
- MSsubscription_articles_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSsubscription_articles system table
ms.assetid: dbc1737f-261e-4017-b9cd-703b9fc4ac78
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: e0aaa6b412f1ccbbc71e9e5b19f68a518912f333
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/05/2020
ms.locfileid: "82812202"
---
# <a name="mssubscription_articles-transact-sql"></a>MSsubscription_articles (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  A tabela **MSsubscription_articles** contém informações sobre os artigos em uma assinatura enfileirada. Essa tabela só é populada para tipos de replicação de atualização enfileirada e atualização imediata com atualização enfileirada como um failover.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**agent_id**|**int**|A ID do agente que serve a este artigo|  
|**artid**|**int**|A ID do artigo da tabela **sysarticles** .|  
|**artigo**|**sysname**|O nome do artigo da tabela **sysarticles** .|  
|**dest_table**|**sysname**|O nome da tabela de destino da tabela **sysarticles** .|  
|**proprietário**|**sysname**|O proprietário da assinatura.|  
|**cft_table**|**sysname**|O nome da tabela de conflito para este artigo, para tipo de replicação de atualização enfileirada.|  
  
## <a name="see-also"></a>Consulte Também  
 [Tabelas de replicação &#40;&#41;Transact-SQL](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Exibições de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
