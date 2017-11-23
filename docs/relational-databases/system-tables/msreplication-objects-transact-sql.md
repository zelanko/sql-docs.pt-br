---
title: MSreplication_objects (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-tables
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to: SQL Server
f1_keywords:
- MSreplication_objects
- MSreplication_objects_TSQL
dev_langs: TSQL
helpviewer_keywords: MSreplication_objects system table
ms.assetid: 08f9710d-976d-448e-bead-ac9835e87bc5
caps.latest.revision: "21"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: bf9eef9834dca254f153c8f7a984f77a1ad33c0f
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="msreplicationobjects-transact-sql"></a>MSreplication_objects (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  O **MSreplication_objects** tabela contém uma linha para cada objeto que está associado com a replicação do banco de dados do assinante. Essa tabela é armazenada no banco de dados de assinatura.  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**Publicador**|**sysname**|O nome do publicador.|  
|**publisher_db**|**sysname**|O nome do banco de dados Publicador.|  
|**publicação**|**sysname**|O nome da publicação.|  
|**object_name**|**sysname**|O nome do objeto.|  
|**object_type**|**char(2)**|O tipo de objeto:<br /><br /> **u** = tabela.<br /><br /> **t** = gatilho.<br /><br /> **p** = procedimento armazenado.|  
|**artigo**|**sysname**|O nome do artigo com o qual o objeto é associado.|  
  
## <a name="see-also"></a>Consulte também  
 [Tabelas de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)  
  
  
