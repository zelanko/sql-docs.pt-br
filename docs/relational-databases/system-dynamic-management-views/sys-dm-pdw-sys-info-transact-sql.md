---
title: sys. dm_pdw_sys_info (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 686976b4-2d5d-4d64-bf12-56eba1dc59b1
author: ronortloff
ms.author: rortloff
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 93e0020fb0da67538b37c171b3252ba029184554
ms.sourcegitcommit: 01297f2487fe017760adcc6db5d1df2c1234abb4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/09/2020
ms.locfileid: "86197017"
---
# <a name="sysdm_pdw_sys_info-transact-sql"></a>sys. dm_pdw_sys_info (Transact-SQL)
[!INCLUDE[applies-to-version/asa-pdw](../../includes/applies-to-version/asa-pdw.md)]

  Fornece um conjunto de contadores de nível de dispositivo que refletem a atividade geral no dispositivo.  
  
|Nome da coluna|Tipo de dados|Descrição|Intervalo|  
|-----------------|---------------|-----------------|-----------|  
|total_sessions|**int**|Número de sessões atualmente no sistema.|0 para max_active_sessions (veja abaixo).|  
|idle_sessions|**int**|Número de sessões ociosas no momento.||  
|active_requests|**int**|Número de solicitações ativas em execução no momento.||  
|queued_requests|**int**|Número de solicitações enfileiradas no momento.||  
|active_loads|**int**|Número de cargas em execução no momento no sistema.||  
|queued_loads|**int**|Número de carregamentos na fila aguardando execução.||  
|active_backups|**int**|Número de backups em execução no momento.||  
|active_restores|**int**|Número de restaurações de backup em execução no momento.||  
  
## <a name="see-also"></a>Consulte Também  
 [Exibições de gerenciamento dinâmico de SQL Data Warehouse e paralelo data warehouse &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
