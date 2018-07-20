---
title: MSagent_profiles (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
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
- MSagent_profiles
- MSagent_profiles_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSagent_profiles system table
ms.assetid: 4ab1b2ae-b6d9-42b7-9b31-98547dbb7f99
caps.latest.revision: 23
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: e3b246b0c174838529dd5e0c6c38bd633c0a90b8
ms.sourcegitcommit: a431ca21eac82117492d7b84c398ddb3fced53cc
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/17/2018
ms.locfileid: "39101374"
---
# <a name="msagentprofiles-transact-sql"></a>MSagent_profiles (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  O **MSagent_profiles** tabela contém uma linha para cada perfil de agente de replicação definido. Essa tabela é armazenada na **msdb** banco de dados.  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**profile_id**|**int**|A ID do perfil.|  
|**profile_name**|**sysname**|O nome de perfil exclusivo para tipo de agente.|  
|**agent_type**|**int**|O tipo de agente:<br /><br /> **1** = o agente de instantâneo<br /><br /> **2** = log Reader Agent<br /><br /> **3** = o agente de distribuição<br /><br /> **4** = o agente de mesclagem<br /><br /> **9** = queue Reader Agent|  
|**type**|**int**|O tipo de perfil:<br /><br /> **0** = system**1** = personalizado|  
|**Descrição**|**nvarchar(3000)**|A descrição do perfil.|  
|**def_profile**|**bit**|Especifica se este perfil será o padrão para esse tipo de agente.|  
  
## <a name="see-also"></a>Consulte também  
 [Tabelas de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Exibições de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
