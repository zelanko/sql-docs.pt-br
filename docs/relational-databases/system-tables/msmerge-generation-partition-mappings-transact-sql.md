---
title: MSmerge_generation_partition_mappings (T-SQL)
description: Descreve o MSmerge_generation_partition_mappings procedimento armazenado usado para controlar as alterações em partições em uma publicação de mesclagem.
ms.custom: seo-lt-2019
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSmerge_generation_partition_mappings_TSQL
- MSmerge_generation_partition_mappings
dev_langs:
- TSQL
helpviewer_keywords:
- MSmerge_generation_partition_mappings system table
ms.assetid: 443a4024-ce48-4772-9ee5-95bd6fb6476b
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 4ae8e89600a76da91ccf06d0a561319af9bec3f1
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89544506"
---
# <a name="msmerge_generation_partition_mappings-transact-sql"></a>MSmerge_generation_partition_mappings (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  A tabela **MSmerge_generation_partition_mappings** é usada para controlar as alterações em partições em uma publicação de mesclagem. Essa tabela é armazenada nos bancos de dados de publicação e scubscription.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**publication_number**|**smallint**|Identifica a publicação de mesclagem.|  
|**geração**|**bigint**|O valor de geração.|  
|**partition_id**|**int**|Identifica a partição.|  
|**changecount**|**int**|O número de vezes que a partição foi alterada.|  
  
## <a name="see-also"></a>Consulte Também  
 [Tabelas de replicação &#40;&#41;Transact-SQL ](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Exibições de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
