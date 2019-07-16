---
title: sysreplicationalerts (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sysreplicationalerts_TSQL
- sysreplicationalerts
dev_langs:
- TSQL
helpviewer_keywords:
- sysreplicationalerts system table
ms.assetid: 6ed15828-8cca-4cf0-b2ff-1ecd0d8db11a
author: stevestein
ms.author: sstein
ms.openlocfilehash: 6cbeab4c673390cb80300eb5ced2b4cb5c1bcf1f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68029739"
---
# <a name="sysreplicationalerts-transact-sql"></a>sysreplicationalerts (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Contém informações sobre as condições que fazem um alerta de replicação ser disparado. Essa tabela é armazenada na **msdb** banco de dados.  
  
|Nome da coluna|Tipo de dados|Descrição|  
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
  
  
