---
title: MSagentparameterlist (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSagentparameterlist_TSQL
- MSagentparameterlist
dev_langs:
- TSQL
helpviewer_keywords:
- Msagentparameterlist system table
ms.assetid: 4ea571a0-078d-4e13-95ee-f3d4bbd4dfb2
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: e82c9dd6bd2768e997e74508741d047d0155665f
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/05/2020
ms.locfileid: "82832346"
---
# <a name="msagentparameterlist-transact-sql"></a>MSagentparameterlist (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  A tabela **MSagentparameterlist** contém informações de parâmetro do agente de replicação e é usada para especificar os parâmetros que podem ser definidos para um determinado tipo de agente. Essa tabela é armazenada no banco de dados **msdb** .  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**agent_type**|**tinyint**|O tipo de agente:<br /><br /> **1** = agente de instantâneo.<br /><br /> **2** = agente de leitor de log.<br /><br /> **3** = agente de distribuição.<br /><br /> **4** = agente de mesclagem.<br /><br /> **9** = Queue Reader Agent.|  
|**parameter_name**|**sysname**|O nome do parâmetro de agente válido.|  
|**default_value**|**nvarchar(4000)**|O valor padrão para o parâmetro de agente, onde NULL indica que tal valor não existe.|  
|**min_value**|**int**|Define uma associação inferior para o parâmetro de agente, onde NULL indica que tal associação não existe.|  
|**max_value**|**int**|Define uma associação superior para o parâmetro de agente, onde o NULL indica que tal associação não existe.|  
  
## <a name="see-also"></a>Consulte Também  
 [Tabelas de replicação &#40;&#41;Transact-SQL](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Exibições de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
