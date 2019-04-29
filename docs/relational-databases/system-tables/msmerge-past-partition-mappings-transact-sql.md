---
title: MSmerge_past_partition_mappings (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSmerge_past_partition_mappings
- MSmerge_past_partition_mappings_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSmerge_past_partition_mappings system table
ms.assetid: 06d54ff5-4d29-4eeb-b8be-64d032e53134
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 7ad8c5db6a067477e3e4e5d349a8faa2adba5199
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62903601"
---
# <a name="msmergepastpartitionmappings-transact-sql"></a>MSmerge_past_partition_mappings (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  O **MSmerge_past_partition_mappings** tabela armazena uma linha para cada id de partição de uma determinada linha alterada pertencer a, mas não mais pertence. Essa tabela é armazenada no banco de dados de publicação.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**publication_number**|**smallint**|O número da publicação, que é armazenado em **sysmergepublications**.|  
|**tablenick**|**int**|O apelido da tabela publicada.|  
|**rowguid**|**uniqueidentifier**|O identificador para a linha determinada.|  
|**partition_id**|**int**|A ID da partição à qual a linha pertence. O valor é -1 se a alteração de linha for relevante para todos os assinantes.|  
|**generation**|**bigint**|O valor da geração na qual a alteração de partição ocorreu.|  
|**reason**|**tinyint**|Interno-somente para uso.|  
  
## <a name="see-also"></a>Consulte também  
 [Tabelas de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Exibições de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
