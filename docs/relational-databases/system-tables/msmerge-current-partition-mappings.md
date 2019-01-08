---
title: MSmerge_current_partition_mappings | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSmerge_current_partition_mappings
- MSmerge_current_partition_mappings_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSmerge_current_partition_mappings system table
ms.assetid: a3088840-5a30-40f5-8e8a-aa03afc4905f
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 98d2b2053fae49ae5beb3c9b7ecd0209dd33f56d
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/03/2018
ms.locfileid: "52791528"
---
# <a name="msmergecurrentpartitionmappings"></a>MSmerge_current_partition_mappings
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  O **MSmerge_current_partition_mappings** tabela armazena uma linha para cada id de partição uma determinada linha alterada pertence. Essa tabela é armazenada no banco de dados de publicação.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**publication_number**|**smallint**|O número da publicação, que é armazenado em **sysmergepublications**.|  
|**tablenick**|**int**|O apelido da tabela publicada.|  
|**ROWGUID**|**uniqueidentifier**|O identificador para a linha determinada.|  
|**partition_id**|**int**|A ID da partição à qual o particionamento pertence. O valor é -1 se a alteração de linha for relevante para todos os assinantes.|  
  
## <a name="see-also"></a>Consulte também  
 [Tabelas de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Exibições de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
