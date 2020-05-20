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
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 58aa7d6bb0789adcca406ac9733759c4d9762301
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/05/2020
ms.locfileid: "82832289"
---
# <a name="msmerge_dynamic_snapshots-transact-sql"></a>MSmerge_dynamic_snapshots (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  A tabela **MSmerge_dynamic_snapshots** rastreia o local do instantâneo de dados filtrados para cada partição definida para uma publicação de mesclagem com filtros de linha com parâmetros. Essa tabela é armazenada no banco de dados de **publicação** .  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**partition_id**|**int**|A ID da partição de mesclagem.|  
|**dynamic_snapshot_location**|**nvarchar (255)**|O local do instantâneo de dados filtrado para a partição.|  
|**last_updated**|**datetime**|A data que o instantâneo de dados filtrado foi atualizado.|  
  
## <a name="see-also"></a>Consulte Também  
 [Tabelas de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)  
  
  
