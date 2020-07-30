---
title: sys. dm_pdw_os_performance_counters (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 0673a8f8-8bed-41eb-8959-a9e3e9e03a65
author: CarlRabeler
ms.author: carlrab
monikerRange: '>= aps-pdw-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 72164d23d8f2dbd27bb30f1341b288c96ab44cc0
ms.sourcegitcommit: df1f0f2dfb9452f16471e740273cd1478ff3100c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/29/2020
ms.locfileid: "87396603"
---
# <a name="sysdm_pdw_os_performance_counters-transact-sql"></a>sys. dm_pdw_os_performance_counters (Transact-SQL)
[!INCLUDE [pdw](../../includes/applies-to-version/pdw.md)]

  Contém informações sobre contadores de desempenho do Windows para os nós no [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] .  
  
|Nome da coluna|Tipo de Dados|DESCRIÇÃO|Intervalo|  
|-----------------|---------------|-----------------|-----------|  
|pdw_node_id|**int**|A ID do nó que contém o contador.<br /><br /> pdw_node_id e counter_name formate a chave para essa exibição.|Consulte node_id em [Sys. dm_pdw_nodes &#40;&#41;do Transact-SQL ](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-nodes-transact-sql.md).|  
|counter_name|**nvarchar(255)**|Nome do contador de desempenho do Windows.||  
|counter_category|**nvarchar(255)**|Nome da categoria do contador de desempenho do Windows.||  
|instance_name|**nvarchar(255)**|Nome da instância específica do contador.||  
|counter_value|**Decimal (38, 10)**|Valor atual do contador.||  
|last_update_time|**Datetime2 (3)**|Carimbo de data/hora da última vez em que o valor foi atualizado.||  
  
## <a name="see-also"></a>Consulte Também  
 [Exibições de gerenciamento dinâmico de SQL Data Warehouse e paralelo data warehouse &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
