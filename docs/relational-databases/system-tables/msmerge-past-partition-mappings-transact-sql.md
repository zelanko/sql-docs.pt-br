---
title: MSmerge_past_partition_mappings (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
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
- MSmerge_past_partition_mappings
- MSmerge_past_partition_mappings_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSmerge_past_partition_mappings system table
ms.assetid: 06d54ff5-4d29-4eeb-b8be-64d032e53134
caps.latest.revision: 25
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: dd96435535dec6413e135015563d3f83fe8b5d05
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="msmergepastpartitionmappings-transact-sql"></a>MSmerge_past_partition_mappings (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  O **MSmerge_past_partition_mappings** tabela armazena uma linha para cada id de partição de uma determinada linha alterada pertencia, mas não mais pertence. Essa tabela é armazenada no banco de dados de publicação.  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**publication_number**|**smallint**|O número da publicação, que é armazenado em **sysmergepublications**.|  
|**tablenick**|**Int**|O apelido da tabela publicada.|  
|**ROWGUID**|**uniqueidentifier**|O identificador para a linha determinada.|  
|**partition_id**|**Int**|A ID da partição à qual a linha pertence. O valor será –1 se a alteração de linha for relevante para todos os Assinantes.|  
|**Geração**|**bigint**|O valor da geração na qual a alteração de partição ocorreu.|  
|**reason**|**tinyint**|Interno-somente para uso.|  
  
## <a name="see-also"></a>Consulte também  
 [Tabelas de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Exibições de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
