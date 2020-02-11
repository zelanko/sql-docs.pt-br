---
title: MSqreader_agents (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSqreader_agents_TSQL
- MSqreader_agents
dev_langs:
- TSQL
helpviewer_keywords:
- MSqreader_agents system table
ms.assetid: dfa1f45e-c531-4385-a097-0a9edd1d7eab
author: stevestein
ms.author: sstein
ms.openlocfilehash: d032552769c32d691a526456cba68aec9ac397e7
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68032567"
---
# <a name="msqreader_agents-transact-sql"></a>MSqreader_agents (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  A tabela **MSqreader_agents** contém uma linha para cada Queue Reader Agent em execução no distribuidor local. Esta tabela é armazenada no banco de dados de distribuição.  
  
|Nome da coluna|Tipo de dados|DESCRIÇÃO|  
|-----------------|---------------|-----------------|  
|**sessão**|**int**|A ID do Queue Reader Agent.|  
|**name**|**nvarchar (100)**|O nome do Queue Reader Agent.|  
|**job_id**|**Binary (16)**|O número de ID de trabalho exclusivo da tabela **sysjobs** .|  
|**profile_id**|**int**|A ID do perfil da tabela de **MSagent_profiles** .|  
|**job_step_uid**|**uniqueidentifier**|A ID exclusiva da etapa de trabalho do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent na qual o agente foi iniciado.|  
  
## <a name="see-also"></a>Consulte Também  
 [Tabelas de replicação &#40;&#41;Transact-SQL](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Exibições de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
