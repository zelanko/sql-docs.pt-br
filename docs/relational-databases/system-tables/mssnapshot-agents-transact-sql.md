---
title: MSsnapshot_agents (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
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
applies_to:
- SQL Server
f1_keywords:
- MSsnapshot_agents
- MSsnapshot_agents_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSsnapshot_agents system table
ms.assetid: aeae0a2e-4c21-4c45-be65-1e426fa52bdd
caps.latest.revision: 28
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 8dfe60e5ae1ad3443fde1b7655941b70f53663cd
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="mssnapshotagents-transact-sql"></a>MSsnapshot_agents (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  O **MSsnapshot_agents** tabela contém uma linha para cada agente de instantâneo associado com o distribuidor local. Esta tabela é armazenada no banco de dados de distribuição.  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**id**|**Int**|A ID do Snapshot Agent.|  
|**name**|**nvarchar(100)**|O nome do Snapshot Agent.|  
|**publisher_id**|**smallint**|A ID do publicador.|  
|**publisher_db**|**sysname**|O nome do banco de dados Publicador.|  
|**Publicação**|**sysname**|O nome da publicação.|  
|**publication_type**|**Int**|O tipo de publicação:<br /><br /> **0** = transacional.<br /><br /> **1** = instantâneo.<br /><br /> **2** = mesclagem.|  
|**local_job**|**bit**|Indica se há um trabalho do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent no Distribuidor local.|  
|**job_id**|**binary(16)**|O número de identificação do trabalho.|  
|**profile_id**|**Int**|A ID de configuração do [MSagent_profiles &#40;Transact-SQL&#41; ](../../relational-databases/system-tables/msagent-profiles-transact-sql.md) tabela.|  
|**dynamic_filter_login**|**sysname**|O valor usado para avaliar o [SUSER_SNAME &#40;Transact-SQL&#41; ](../../t-sql/functions/suser-sname-transact-sql.md) função em filtros com parâmetros que definem uma partição. Essa coluna é usada para um instantâneo particionado.|  
|**dynamic_filter_hostname**|**sysname**|O valor usado para avaliar o [HOST_NAME &#40;Transact-SQL&#41; ](../../t-sql/functions/host-name-transact-sql.md) função em filtros com parâmetros que definem uma partição. Essa coluna é usada para um instantâneo particionado.|  
|**publisher_security_mode**|**smallint**|O modo de segurança usado pelo agente na conexão com o Publicador que pode ser um dos seguintes:<br /><br /> **0**  =  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] autenticação<br /><br /> **1**  =  [!INCLUDE[msCoName](../../includes/msconame-md.md)] autenticação do Windows.|  
|**publisher_login**|**sysname**|O logon usado na conexão com o Publicador.|  
|**publisher_password**|**nvarchar (524)**|O valor criptografado da senha usada na conexão com o Publicador.|  
|**job_step_uid**|**uniqueidentifier**|A ID exclusiva da etapa de trabalho do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent na qual o agente foi iniciado.|  
  
## <a name="see-also"></a>Consulte também  
 [Tabelas de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Exibições de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
