---
title: MSmerge_dynamic_snapshots (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSmerge_dynamic_snapshots_TSQL
- MSmerge_dynamic_snapshots
dev_langs:
- TSQL
helpviewer_keywords:
- MSmerge_dynamic_snapshots system table
ms.assetid: a5592b3c-731b-4fc9-ae4b-2602ed78248e
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: f7e41f604bf9d87b2db0b22749f58ee7fd2acf2b
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/03/2018
ms.locfileid: "52791808"
---
# <a name="msmergedynamicsnapshots-transact-sql"></a>MSmerge_dynamic_snapshots (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  O **MSmerge_dynamic_snapshots** tabela rastreia o local do instantâneo de dados filtrados para cada partição definida para uma publicação de mesclagem com filtros de linha com parâmetros. Essa tabela é armazenada na **publicação** banco de dados.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**partition_id**|**int**|A ID da partição de mesclagem.|  
|**dynamic_snapshot_location**|**nvarchar(255)**|O local do instantâneo de dados filtrado para a partição.|  
|**last_updated**|**datetime**|A data que o instantâneo de dados filtrado foi atualizado.|  
  
## <a name="see-also"></a>Consulte também  
 [Tabelas de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)  
  
  
