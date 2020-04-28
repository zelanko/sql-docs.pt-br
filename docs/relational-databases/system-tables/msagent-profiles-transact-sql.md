---
title: MSagent_profiles (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSagent_profiles
- MSagent_profiles_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSagent_profiles system table
ms.assetid: 4ab1b2ae-b6d9-42b7-9b31-98547dbb7f99
author: stevestein
ms.author: sstein
ms.openlocfilehash: 5147ef1f482850b55a5d01a476b1981dfa012e5e
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68021051"
---
# <a name="msagent_profiles-transact-sql"></a>MSagent_profiles (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  A tabela **MSagent_profiles** contém uma linha para cada perfil de agente de replicação definido. Essa tabela é armazenada no banco de dados **msdb** .  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**profile_id**|**int**|A ID do perfil.|  
|**profile_name**|**sysname**|O nome de perfil exclusivo para tipo de agente.|  
|**agent_type**|**int**|O tipo de agente:<br /><br /> **1** = agente de instantâneo<br /><br /> **2** = agente de leitor de log<br /><br /> **3** = agente de distribuição<br /><br /> **4** = agente de mesclagem<br /><br /> **9** = Queue Reader Agent|  
|**type**|**int**|O tipo de perfil:<br /><br /> **0** = sistema**1** = personalizado|  
|**ndescrição**|**nvarchar (3000)**|A descrição do perfil.|  
|**def_profile**|**bit**|Especifica se este perfil será o padrão para esse tipo de agente.|  
  
## <a name="see-also"></a>Consulte Também  
 [Tabelas de replicação &#40;&#41;Transact-SQL](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Exibições de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
