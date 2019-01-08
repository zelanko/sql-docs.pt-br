---
title: MSreplication_subscriptions (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSreplication_subscriptions
- MSreplication_subscriptions_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSreplication_subscriptions system table
ms.assetid: fd0c5843-4e9b-4448-8bfb-0a4067d1d8d1
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 0fa68012f419939c3f77980020795f23c4ca4672
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/03/2018
ms.locfileid: "52794528"
---
# <a name="msreplicationsubscriptions-transact-sql"></a>MSreplication_subscriptions (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  O **MSreplication_subscriptions** tabela contém uma linha de informações de replicação para cada agente de distribuição de manutenção de banco de dados do assinante local. Essa tabela é armazenada no banco de dados de assinatura.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**publisher**|**sysname**|O nome do publicador.|  
|**publisher_db**|**sysname**|O nome do banco de dados Publicador.|  
|**publicação**|**sysname**|O nome da publicação.|  
|**independent_agent**|**bit**|Indica se existe um Distribution Agent autônomo para essa publicação.|  
|**subscription_type**|**int**|O tipo de assinatura:<br /><br /> 0 = Push.<br /><br /> 1 = Pull.<br /><br /> 2 = Anônimo.|  
|**distribution_agent**|**sysname**|O nome do Distribution Agent.|  
|**Time**|**smalldatetime**|A hora da última atualização pelo Distribution Agent.|  
|**description**|**nvarchar(255)**|A descrição da assinatura.|  
|**transaction_timestamp**|**varbinary(16)**|Interno-somente para uso.|  
|**update_mode**|**tinyint**|O tipo de atualização.|  
|**agent_id**|**binary(16)**|A ID do agente.|  
|**subscription_guid**|**binary(16)**|O identificador global para a versão da assinatura na publicação.|  
|**subid**|**binary(16)**|O identificador global de uma assinatura anônima.|  
|**immediate_sync**|**bit**|Indica se arquivos de sincronização são criados ou recriados cada vez que o Snapshot Agent é executado.|  
  
## <a name="see-also"></a>Consulte também  
 [Tabelas de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Exibições de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)   
 [sp_helpsubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpsubscription-transact-sql.md)  
  
  
