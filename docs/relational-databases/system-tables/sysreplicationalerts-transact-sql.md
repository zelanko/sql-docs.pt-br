---
title: sysreplicationalerts (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
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
- sysreplicationalerts_TSQL
- sysreplicationalerts
dev_langs:
- TSQL
helpviewer_keywords:
- sysreplicationalerts system table
ms.assetid: 6ed15828-8cca-4cf0-b2ff-1ecd0d8db11a
caps.latest.revision: 27
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: dbc1aa2be529d00d2dfd453b181a72ea116809a2
ms.sourcegitcommit: a431ca21eac82117492d7b84c398ddb3fced53cc
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/17/2018
ms.locfileid: "39103004"
---
# <a name="sysreplicationalerts-transact-sql"></a>sysreplicationalerts (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Contém informações sobre as condições que fazem um alerta de replicação ser disparado. Essa tabela é armazenada na **msdb** banco de dados.  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**alert_id**|**int**|A ID do alerta.|  
|**status**|**int**|O valor definido pelo usuário:<br /><br /> **0** = não servido.<br /><br /> **1** = atendidas.|  
|**agent_type**|**int**|O tipo de agente:<br /><br /> **1** = o agente de instantâneo.<br /><br /> **2** = log Reader Agent.<br /><br /> **3** = o agente de distribuição.<br /><br /> **4** = o agente de mesclagem.|  
|**agent_id**|**int**|A ID do agente das tabelas **MSsnapshot_agents**, **MSlogreader_agents**, **MSdistribution_agents**, ou **MSmerge_agents**.|  
|**error_id**|**int**|A ID do erro armazenado em **MSrepl_errors**.|  
|**alert_error_code**|**int**|A ID da mensagem do alerta gerado ao registrar esse registro.|  
|**time**|**datetime**|A hora que o registro foi inserido.|  
|**publisher**|**sysname**|O nome do Publicador associado ao agente que disparou esse alerta.|  
|**publisher_db**|**sysname**|O banco de dados Publicador associado ao agente que disparou esse alerta.|  
|**publicação**|**sysname**|A publicação associada ao agente que disparou esse alerta.|  
|**publication_type**|**int**|O tipo de publicação:<br /><br /> **0** = instantâneo.<br /><br /> **1** = transacional.<br /><br /> **2** = mesclagem.|  
|**Assinante**|**sysname**|O nome do Assinante associado ao agente que disparou esse alerta.|  
|**subscriber_db**|**sysname**|O nome do banco de dados do Assinante associado ao agente que disparou esse alerta.|  
|**article**|**sysname**|O nome do artigo associado ao agente que disparou esse alerta.|  
|**destination_object**|**sysname**|O nome tabela de assinatura associada ao alerta.|  
|**source_object**|**sysname**|O nome tabela publicada associada ao alerta.|  
|**alert_error_text**|**ntext**|O texto do alerta.|  
  
## <a name="see-also"></a>Consulte também  
 [Tabelas de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Exibições de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
