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
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 59adf719aa4647e8382b8c06fa838d7acf2b3feb
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85736764"
---
# <a name="msmerge_generation_partition_mappings-transact-sql"></a>MSmerge_generation_partition_mappings (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  A tabela **MSmerge_generation_partition_mappings** é usada para controlar as alterações em partições em uma publicação de mesclagem. Essa tabela é armazenada nos bancos de dados de publicação e scubscription.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**publication_number**|**smallint**|Identifica a publicação de mesclagem.|  
|**geração**|**bigint**|O valor de geração.|  
|**partition_id**|**int**|Identifica a partição.|  
|**changecount**|**int**|O número de vezes que a partição foi alterada.|  
  
## <a name="see-also"></a>Consulte Também  
 [Tabelas de replicação &#40;&#41;Transact-SQL](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Exibições de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
