---
title: MSmerge_partition_groups (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSmerge_partition_groups_TSQL
- MSmerge_partition_groups
dev_langs:
- TSQL
helpviewer_keywords:
- MSmerge_partition_groups system table
ms.assetid: 5d56d780-ee40-4afc-9c2a-d1723d86e430
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: cb8c77ba54e25c574d5f751febe8bdac3ba1dfbf
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/03/2018
ms.locfileid: "52775338"
---
# <a name="msmergepartitiongroups-transact-sql"></a>MSmerge_partition_groups (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  O **MSmerge_partition_groups** tabela armazena uma linha para cada partição pré-computada em um determinado banco de dados. Além das colunas listadas, uma coluna é adicionada a essa tabela, para cada função usada em um filtro de linha com parâmetros. Por exemplo, uma coluna denominada **HOST_NAME_FN** é adicionada à tabela, se um filtro usa o [HOST_NAME](../../t-sql/functions/host-name-transact-sql.md) função. Uma linha é armazenada para cada conjunto exclusivo de valores de função, que sincronizaram com esse Publicador. Dois ou mais Assinantes sincronizando com o mesmo valor exatamente, para todas essas funções, compartilharão a mesma linha nessa tabela e, portanto, compartilharão a mesma ID de partição. Essa tabela é armazenada no banco de dados de publicação.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**partition_id**|**int**|Coluna de identidade que fornece um número de ID exclusivo para a partição pré-computada.|  
|**publication_number**|**smallint**|O número da publicação, que é armazenado em **sysmergepublications**.|  
|**maxgen_whenadded**|**bigint**|A geração mais alta conhecida no Publicador no momento em que a linha é inserida nessa tabela.|  
|**using_partition_groups**|**bit**|Indica se a partição pertence a uma publicação que usa partição pré-computada e pode ser um destes valores:<br /><br /> **0** = publicação usa partições pré-computadas.<br /><br /> **1** = publicação usa partições pré-computadas<br /><br /> Para obter mais informações, consulte [Optimize Parameterized Filter Performance with Precomputed Partitions](../../relational-databases/replication/merge/parameterized-filters-optimize-for-precomputed-partitions.md) (Otimizar o desempenho do filtro parametrizado com partições pré-computadas).|  
|**HOST_NAME_FN**|**nvarchar(128)**|O valor fornecido ao usar filtros de linha com parâmetros para gerar partições. Para obter mais informações, consulte [Filtros de linha com parâmetros](../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md).|  
  
## <a name="see-also"></a>Consulte também  
 [Tabelas de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Exibições de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
