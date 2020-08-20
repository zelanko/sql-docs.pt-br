---
description: MSreplication_subscriptions (Transact-SQL)
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
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 1f8af3b4666556e41da1e48917c584e41dbddedd
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88454592"
---
# <a name="msreplication_subscriptions-transact-sql"></a>MSreplication_subscriptions (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  A tabela **MSreplication_subscriptions** contém uma linha de informações de replicação para cada agente de distribuição atendendo ao banco de dados do assinante local. Essa tabela é armazenada no banco de dados de assinatura.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**programa**|**sysname**|O nome do Publicador.|  
|**publisher_db**|**sysname**|O nome do banco de dados Publicador.|  
|**documento**|**sysname**|O nome da publicação.|  
|**independent_agent**|**bit**|Indica se existe um Distribution Agent autônomo para essa publicação.|  
|**subscription_type**|**int**|O tipo de assinatura:<br /><br /> 0 = Push.<br /><br /> 1 = Pull.<br /><br /> 2 = Anônimo.|  
|**distribution_agent**|**sysname**|O nome do Distribution Agent.|  
|**Hora**|**smalldatetime**|A hora da última atualização pelo Distribution Agent.|  
|**descrição**|**nvarchar(255)**|A descrição da assinatura.|  
|**transaction_timestamp**|**varbinary(16)**|Interno-somente uso.|  
|**update_mode**|**tinyint**|O tipo de atualização.|  
|**agent_id**|**binary(16)**|A ID do agente.|  
|**subscription_guid**|**binary(16)**|O identificador global para a versão da assinatura na publicação.|  
|**subid**|**binary(16)**|O identificador global de uma assinatura anônima.|  
|**immediate_sync**|**bit**|Indica se arquivos de sincronização são criados ou recriados cada vez que o Snapshot Agent é executado.|  
  
## <a name="see-also"></a>Consulte Também  
 [Tabelas de replicação &#40;&#41;Transact-SQL ](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Exibições de replicação &#40;&#41;Transact-SQL ](../../relational-databases/system-views/replication-views-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_helpsubscription ](../../relational-databases/system-stored-procedures/sp-helpsubscription-transact-sql.md)  
  
  
