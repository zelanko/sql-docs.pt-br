---
description: MSsnapshot_agents (Transact-SQL)
title: MSsnapshot_agents (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSsnapshot_agents
- MSsnapshot_agents_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSsnapshot_agents system table
ms.assetid: aeae0a2e-4c21-4c45-be65-1e426fa52bdd
author: markingmyname
ms.author: maghan
ms.openlocfilehash: c5b83521f64253aaa5d4eb6dfd6d5e49eb5d71b4
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89523880"
---
# <a name="mssnapshot_agents-transact-sql"></a>MSsnapshot_agents (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  A tabela de **MSsnapshot_agents** contém uma linha para cada agente de instantâneo associada ao distribuidor local. Esta tabela é armazenada no banco de dados de distribuição.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**id**|**int**|A ID do Snapshot Agent.|  
|**name**|**nvarchar (100)**|O nome do Snapshot Agent.|  
|**publisher_id**|**smallint**|A ID do Publicador.|  
|**publisher_db**|**sysname**|O nome do banco de dados Publicador.|  
|**documento**|**sysname**|O nome da publicação.|  
|**publication_type**|**int**|O tipo de publicação:<br /><br /> **0** = transacional.<br /><br /> **1** = instantâneo.<br /><br /> **2** = mesclar.|  
|**local_job**|**bit**|Indica se há um trabalho do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent no Distribuidor local.|  
|**job_id**|**binary(16)**|O número de identificação do trabalho.|  
|**profile_id**|**int**|A ID de configuração do [MSagent_profiles &#40;tabela&#41;Transact-SQL ](../../relational-databases/system-tables/msagent-profiles-transact-sql.md) .|  
|**dynamic_filter_login**|**sysname**|O valor usado para avaliar a função de [&#41;de &#40;Transact-SQL SUSER_SNAME ](../../t-sql/functions/suser-sname-transact-sql.md) em filtros com parâmetros que definem uma partição. Essa coluna é usada para um instantâneo particionado.|  
|**dynamic_filter_hostname**|**sysname**|O valor usado para avaliar a função de [&#41;de &#40;Transact-SQL HOST_NAME ](../../t-sql/functions/host-name-transact-sql.md) em filtros com parâmetros que definem uma partição. Essa coluna é usada para um instantâneo particionado.|  
|**publisher_security_mode**|**smallint**|O modo de segurança usado pelo agente na conexão com o Publicador que pode ser um dos seguintes:<br /><br /> **0**  =  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] autenticação<br /><br /> **1**  =  [!INCLUDE[msCoName](../../includes/msconame-md.md)] autenticação do Windows.|  
|**publisher_login**|**sysname**|O logon usado na conexão com o Publicador.|  
|**publisher_password**|**nvarchar (524)**|O valor criptografado da senha usada na conexão com o Publicador.|  
|**job_step_uid**|**uniqueidentifier**|A ID exclusiva da etapa de trabalho do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent na qual o agente foi iniciado.|  
|**job_login**|**sysname**||  
|**job_password**|**nvarchar (524)**||  
  
## <a name="see-also"></a>Consulte Também  
 [Tabelas de replicação &#40;&#41;Transact-SQL ](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Exibições de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
