---
description: MSmerge_past_partition_mappings (Transact-SQL)
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
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 6f6725fc632ae132cde37191eda73035f23092d5
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89545618"
---
# <a name="msmerge_past_partition_mappings-transact-sql"></a>MSmerge_past_partition_mappings (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  A tabela **MSmerge_past_partition_mappings** armazena uma linha para cada ID de partição uma determinada linha alterada usada para pertencer a, mas não pertence mais a. Essa tabela é armazenada no banco de dados de publicação.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**publication_number**|**smallint**|O número de publicação, que é armazenado em **sysmergepublications**.|  
|**tablenick**|**int**|O apelido da tabela publicada.|  
|**ROWGUID**|**uniqueidentifier**|O identificador para a linha determinada.|  
|**partition_id**|**int**|A ID da partição à qual a linha pertence. O valor será-1 se a alteração de linha for relevante para todos os assinantes.|  
|**geração**|**bigint**|O valor da geração na qual a alteração de partição ocorreu.|  
|**motivo**|**tinyint**|Interno-somente uso.|  
  
## <a name="see-also"></a>Consulte Também  
 [Tabelas de replicação &#40;&#41;Transact-SQL ](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Exibições de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
