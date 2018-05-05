---
title: MSreplication_subscriptions (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-tables
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- MSreplication_subscriptions
- MSreplication_subscriptions_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSreplication_subscriptions system table
ms.assetid: fd0c5843-4e9b-4448-8bfb-0a4067d1d8d1
caps.latest.revision: 27
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 91f5679147c6432fd5f76574272b8b2cf15f3d0c
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="msreplicationsubscriptions-transact-sql"></a>MSreplication_subscriptions (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  O **MSreplication_subscriptions** tabela contém uma linha de informações de replicação para cada agente de distribuição de manutenção de banco de dados de assinante local. Essa tabela é armazenada no banco de dados de assinatura.  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**publisher**|**sysname**|O nome do publicador.|  
|**publisher_db**|**sysname**|O nome do banco de dados Publicador.|  
|**Publicação**|**sysname**|O nome da publicação.|  
|**independent_agent**|**bit**|Indica se existe um Distribution Agent autônomo para essa publicação.|  
|**subscription_type**|**Int**|O tipo de assinatura:<br /><br /> 0 = Push.<br /><br /> 1 = Pull.<br /><br /> 2 = Anônimo.|  
|**distribution_agent**|**sysname**|O nome do Distribution Agent.|  
|**Hora**|**smalldatetime**|A hora da última atualização pelo Distribution Agent.|  
|**Descrição**|**nvarchar(255)**|A descrição da assinatura.|  
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
  
  
