---
title: MSreplication_options (Transact-SQL) | Microsoft Docs
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
- MSreplication_options
- MSreplication_options_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSreplication_options system table
ms.assetid: 23cf10d7-8bc1-4368-b5eb-e5576421e776
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 5711a1f0de3f335867c3b5162a4ec77f52d79dfc
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="msreplicationoptions-transact-sql"></a>MSreplication_options (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  O **MSreplication_options** tabela armazena metadados que é usado internamente pela replicação. Essa tabela é armazenada no **mestre** banco de dados.  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**optname**|**sysname**|Somente para uso interno.|  
|**valor**|**bit**|Somente para uso interno.|  
|**versão_principal**|**int**|Somente para uso interno.|  
|**versão_secundária**|**int**|Somente para uso interno.|  
|**revisão**|**int**|Somente para uso interno.|  
|**install_failures**|**int**|Somente para uso interno.|  
  
## <a name="see-also"></a>Consulte também  
 [Tabelas de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)  
  
  
