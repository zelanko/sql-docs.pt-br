---
title: MSmerge_agents (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSmerge_agents
- MSmerge_agents_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSmerge_agents system table
ms.assetid: 639d2ebb-2c37-4fe0-b14b-1637bc5fc221
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 1053b358a5854febe1147ceb5ec0a374468c5b69
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/03/2018
ms.locfileid: "52785698"
---
# <a name="msmergeagents-transact-sql"></a>MSmerge_agents (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  O **MSmerge_agents** tabela contém uma linha para cada agente de mesclagem em execução no assinante. Esta tabela é armazenada no banco de dados de distribuição.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**id**|**int**|A ID do Merge Agent.|  
|**name**|**nvarchar(100)**|O nome do Merge Agent.|  
|**publisher_id**|**smallint**|A ID do publicador.|  
|**publisher_db**|**sysname**|O nome do banco de dados Publicador.|  
|**publicação**|**sysname**|O nome da publicação.|  
|**subscriber_id**|**smallint**|A ID do assinante.|  
|**subscriber_db**|**sysname**|O nome do banco de dados de assinatura.|  
|**local_job**|**bit**|Indica se há um trabalho do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent no Distribuidor local.|  
|**job_id**|**binary(16)**|O número de identificação do trabalho.|  
|**profile_id**|**int**|A ID de configuração a partir de **MSagent_profiles** tabela.|  
|**anonymous_subid**|**uniqueidentifier**|A ID de um agente anônimo.|  
|**subscriber_name**|**sysname**|O nome do Assinante.|  
|**creation_date**|**datetime**|A data e hora que o Distribution ou Merge Agent foi criado.|  
|**offload_enabled**|**bit**|Especifica que o agente pode ser ativado remotamente.<br /><br /> **0** Especifica o agente não pode ser ativado remotamente.<br /><br /> **1** Especifica o agente será ativado remotamente e no computador remoto especificado na propriedade offload_server.|  
|**offload_server**|**sysname**|Especifica o nome da rede de servidor a ser usado para ativação de agente remota.|  
|**sid**|**varbinary(85)**|O SID (número de identificação de segurança) para o Distribution Agent ou Merge Agent durante sua primeira execução.|  
|**subscriber_security_mode**|**smallint**|O modo de segurança usado pelo agente ao se conectar ao Assinante que pode ser um dos seguintes:<br /><br /> **0**  =  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] autenticação.<br /><br /> **1**  =  [!INCLUDE[msCoName](../../includes/msconame-md.md)] autenticação do Windows.|  
|**subscriber_login**|**sysname**|O logon usado na conexão com o Assinante.|  
|**subscriber_password**|**nvarchar(524)**|O valor criptografado da senha usada na conexão com o Assinante.|  
|**publisher_security_mode**|**smallint**|O modo de segurança usado pelo agente na conexão com o Publicador que pode ser um dos seguintes:<br /><br /> **0**  =  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] autenticação.<br /><br /> **1**  =  [!INCLUDE[msCoName](../../includes/msconame-md.md)] autenticação do Windows.|  
|**publisher_login**|**sysname**|O logon usado na conexão com o Publicador.|  
|**publisher_password**|**nvarchar(524)**|O valor criptografado da senha usada na conexão com o Publicador.|  
|**job_step_uid**|**uniqueidentifier**|A ID exclusiva da etapa de trabalho do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent na qual o agente foi iniciado.|  
  
## <a name="see-also"></a>Consulte também  
 [Tabelas de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Exibições de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
