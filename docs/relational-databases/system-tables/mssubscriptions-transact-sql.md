---
title: MSsubscriptions (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
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
- MSsubscriptions_TSQL
- MSsubscriptions
dev_langs:
- TSQL
helpviewer_keywords:
- MSsubscriptions system table
ms.assetid: b7e8301d-d115-41f6-8d4f-e0d25f453b25
caps.latest.revision: 18
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 05f5100843227093cd11909adede12f449cf0051
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="mssubscriptions-transact-sql"></a>MSsubscriptions (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  O **MSsubscriptions** tabela contém uma linha para cada artigo publicado em uma assinatura servida pelo distribuidor local. Esta tabela é armazenada no banco de dados de distribuição.  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**publisher_database_id**|**Int**|A ID do banco de dados Publicador.|  
|**publisher_id**|**smallint**|A ID do publicador.|  
|**publisher_db**|**sysname**|O nome do banco de dados Publicador.|  
|**publication_id**|**Int**|A ID da publicação.|  
|**article_id**|**Int**|A ID do artigo.|  
|**subscriber_id**|**smallint**|A ID do assinante.|  
|**subscriber_db**|**sysname**|O nome do banco de dados de assinatura.|  
|**subscription_type**|**Int**|O tipo de assinatura:<br /><br /> **0** = push.<br /><br /> **1** = pull.<br /><br /> **2** = anônimo.|  
|**sync_type**|**tinyint**|O tipo de sincronização:<br /><br /> **1** = automático.<br /><br /> **2** não = nenhuma sincronização.|  
|**status**|**tinyint**|O status da assinatura:<br /><br /> **0** = inativo.<br /><br /> **1** = assinado.<br /><br /> **2** = ativo.|  
|**subscription_seqno**|**varbinary(16)**|O número de sequência de transação de instantâneo.|  
|**snapshot_seqno_flag**|**bit**|Indica a fonte do número de sequência da transação de instantâneo, onde um valor de **1** significa que **subscription_seqno** é o número de sequência do instantâneo.|  
|**independent_agent**|**bit**|Indica se existe um Distribution Agent autônomo para essa publicação.|  
|**subscription_time**|**datetime**|Somente para uso interno.|  
|**loopback_detection**|**bit**|Aplica-se a assinaturas que fazem parte de uma topologia de replicação transacional bidirecional. A detecção de loopback determina se o Distribution Agent envia transações originadas no Assinante de volta para o Assinante:<br /><br /> **1** = não envia de volta.<br /><br /> **0** = envia de volta.<br /><br /> Observação: Esta coluna tem suporte somente para compatibilidade com versões anteriores com a funcionalidade de replicação bidirecional no [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)]. Para versões posteriores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], deve ser usada replicação ponto a ponto. Para obter mais informações, consulte [Peer-to-Peer Transactional Replication](../../relational-databases/replication/transactional/peer-to-peer-transactional-replication.md).|  
|**agent_id**|**Int**|A ID do agente.|  
|**update_mode**|**tinyint**|O tipo de atualização.|  
|**publisher_seqno**|**varbinary(16)**|O número de sequência da transação no Publicador para esta assinatura.|  
|**ss_cplt_seqno**|**varbinary(16)**|O número de sequência usado para significar a conclusão do processamento de instantâneo simultâneo.|  
  
## <a name="see-also"></a>Consulte também  
 [Tabelas de replicação](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Exibições de replicação](../../relational-databases/system-views/replication-views-transact-sql.md)   
 [sp_helpsubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpsubscription-transact-sql.md)  
  
  
