---
title: MSreplication_objects (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSreplication_objects
- MSreplication_objects_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSreplication_objects system table
ms.assetid: 08f9710d-976d-448e-bead-ac9835e87bc5
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: f0098cd55f03a7103345407e566615e10a63b2ac
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/03/2018
ms.locfileid: "52757878"
---
# <a name="msreplicationobjects-transact-sql"></a>MSreplication_objects (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  O **MSreplication_objects** tabela contém uma linha para cada objeto que está associado com a replicação no banco de dados do assinante. Essa tabela é armazenada no banco de dados de assinatura.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**publisher**|**sysname**|O nome do publicador.|  
|**publisher_db**|**sysname**|O nome do banco de dados Publicador.|  
|**publicação**|**sysname**|O nome da publicação.|  
|**object_name**|**sysname**|O nome do objeto.|  
|**object_type**|**char(2)**|O tipo de objeto:<br /><br /> **u** = tabela.<br /><br /> **t** = gatilho.<br /><br /> **p** = procedimento armazenado.|  
|**article**|**sysname**|O nome do artigo com o qual o objeto é associado.|  
  
## <a name="see-also"></a>Consulte também  
 [Tabelas de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)  
  
  
