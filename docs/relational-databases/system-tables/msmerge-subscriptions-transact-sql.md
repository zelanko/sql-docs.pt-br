---
title: MSmerge_subscriptions (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology:
- replication
ms.topic: language-reference
f1_keywords:
- MSmerge_subscriptions
- MSmerge_subscriptions_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSmerge_subscriptions system table
ms.assetid: cafd954a-92f8-44cb-a5d0-dce9aafa5ee1
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: e023fc4554ab738e3a72f2113075c1fe682d30c0
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47644074"
---
# <a name="msmergesubscriptions-transact-sql"></a>MSmerge_subscriptions (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  O **MSmerge_subscriptions** tabela contém uma linha para cada assinatura servida pelo Merge Agent no assinante. Esta tabela é armazenada no banco de dados de distribuição.  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**publisher_id**|**smallint**|A ID do publicador.|  
|**publisher_db**|**sysname**|O nome do banco de dados Publicador.|  
|**publication_id**|**int**|A ID da publicação.|  
|**subscriber_id**|**smallint**|A ID do assinante.|  
|**subscriber_db**|**sysname**|O nome do banco de dados de assinatura.|  
|**subscription_type**|**int**|O tipo de assinatura:<br /><br /> 0 = Push.<br /><br /> 1 = Pull.<br /><br /> 2 = Anônimo.|  
|**sync_type**|**tinyint**|O tipo de sincronização:<br /><br /> 1 = Automático.<br /><br /> 2 = Nenhuma sincronização.|  
|**status**|**tinyint**|O status da assinatura.|  
|**subscription_time**|**datetime**|A hora que a assinatura foi adicionada.|  
  
## <a name="see-also"></a>Consulte também  
 [Tabelas de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Exibições de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
