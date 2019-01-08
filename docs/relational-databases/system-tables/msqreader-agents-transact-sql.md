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
manager: craigg
ms.openlocfilehash: 68bca208f7e199ad65ff93a70f4d6c4a3b97fd8b
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/03/2018
ms.locfileid: "52818818"
---
# <a name="msqreaderagents-transact-sql"></a>MSqreader_agents (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  O **MSqreader_agents** tabela contém uma linha para cada Queue Reader Agent está em execução no distribuidor local. Esta tabela é armazenada no banco de dados de distribuição.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**id**|**int**|A ID do Queue Reader Agent.|  
|**name**|**nvarchar(100)**|O nome do Queue Reader Agent.|  
|**job_id**|**binary(16)**|O número de identificação exclusiva do trabalho do **sysjobs** tabela.|  
|**profile_id**|**int**|A ID de perfil a partir de **MSagent_profiles** tabela.|  
|**job_step_uid**|**uniqueidentifier**|A ID exclusiva da etapa de trabalho do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent na qual o agente foi iniciado.|  
  
## <a name="see-also"></a>Consulte também  
 [Tabelas de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Exibições de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
