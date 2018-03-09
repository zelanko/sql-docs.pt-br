---
title: MSagentparameterlist (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-tables
ms.reviewer: 
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- MSagentparameterlist_TSQL
- MSagentparameterlist
dev_langs:
- TSQL
helpviewer_keywords:
- Msagentparameterlist system table
ms.assetid: 4ea571a0-078d-4e13-95ee-f3d4bbd4dfb2
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 60f13f390ec499a3cc6f8add79538ea6d2cb133d
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="msagentparameterlist-transact-sql"></a>MSagentparameterlist (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  O **MSagentparameterlist** tabela contém informações de parâmetro do agente de replicação e é usada para especificar os parâmetros que podem ser definidos para um determinado tipo de agente. Essa tabela é armazenada no **msdb** banco de dados.  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**agent_type**|**tinyint**|O tipo de agente:<br /><br /> **1** = o agente de instantâneo.<br /><br /> **2** = o log Reader Agent.<br /><br /> **3** = o agente de distribuição.<br /><br /> **4** = o agente de mesclagem.<br /><br /> **9** = queue Reader Agent.|  
|**parameter_name**|**sysname**|O nome do parâmetro de agente válido.|  
|**default_value**|**nvarchar(4000)**|O valor padrão para o parâmetro de agente, onde NULL indica que tal valor não existe.|  
|**MIN_VALUE**|**int**|Define uma associação inferior para o parâmetro de agente, onde NULL indica que tal associação não existe.|  
|**MAX_VALUE**|**int**|Define uma associação superior para o parâmetro de agente, onde o NULL indica que tal associação não existe.|  
  
## <a name="see-also"></a>Consulte também  
 [Tabelas de replicação &#40; Transact-SQL &#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Exibições de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
