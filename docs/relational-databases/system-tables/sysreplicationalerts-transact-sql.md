---
description: sysreplicationalerts (Transact-SQL)
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
author: markingmyname
ms.author: maghan
ms.openlocfilehash: cce33fa91f6ea11cda33e622edd39ec764b2c2ce
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89537802"
---
# <a name="sysreplicationalerts-transact-sql"></a>sysreplicationalerts (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Contém informações sobre as condições que fazem um alerta de replicação ser disparado. Essa tabela é armazenada no banco de dados **msdb** .  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**alert_id**|**int**|A ID do alerta.|  
|**status**|**int**|O valor definido pelo usuário:<br /><br /> **0** = não atendido.<br /><br /> **1** = atendido.|  
|**agent_type**|**int**|O tipo de agente:<br /><br /> **1** = agente de instantâneo.<br /><br /> **2** = agente de leitor de log.<br /><br /> **3** = agente de distribuição.<br /><br /> **4** = agente de mesclagem.|  
|**agent_id**|**int**|A ID do agente das tabelas **MSsnapshot_agents**, **MSlogreader_agents**, **MSdistribution_agents**ou **MSmerge_agents**.|  
|**error_id**|**int**|A ID do erro armazenado em **MSrepl_errors**.|  
|**alert_error_code**|**int**|A ID da mensagem do alerta gerado ao registrar esse registro.|  
|**time**|**datetime**|A hora que o registro foi inserido.|  
|**programa**|**sysname**|O nome do Publicador associado ao agente que disparou esse alerta.|  
|**publisher_db**|**sysname**|O banco de dados Publicador associado ao agente que disparou esse alerta.|  
|**documento**|**sysname**|A publicação associada ao agente que disparou esse alerta.|  
|**publication_type**|**int**|O tipo de publicação:<br /><br /> **0** = instantâneo.<br /><br /> **1** = transacional.<br /><br /> **2** = mesclar.|  
|**farão**|**sysname**|O nome do Assinante associado ao agente que disparou esse alerta.|  
|**subscriber_db**|**sysname**|O nome do banco de dados do Assinante associado ao agente que disparou esse alerta.|  
|**artigo**|**sysname**|O nome do artigo associado ao agente que disparou esse alerta.|  
|**destination_object**|**sysname**|O nome tabela de assinatura associada ao alerta.|  
|**source_object**|**sysname**|O nome tabela publicada associada ao alerta.|  
|**alert_error_text**|**ntext**|O texto do alerta.|  
  
## <a name="see-also"></a>Consulte Também  
 [Tabelas de replicação &#40;&#41;Transact-SQL ](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Exibições de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
