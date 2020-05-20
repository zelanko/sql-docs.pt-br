---
title: sys. dm_pdw_os_performance_counters (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.technology: system-objects
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 0673a8f8-8bed-41eb-8959-a9e3e9e03a65
author: CarlRabeler
ms.author: carlrab
monikerRange: '>= aps-pdw-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: a5fdb20b8fe35238e912c302bb57812e8e4791a4
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/05/2020
ms.locfileid: "82819246"
---
# <a name="sysdm_pdw_os_performance_counters-transact-sql"></a>sys. dm_pdw_os_performance_counters (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md.md)]

  Contém informações sobre contadores de desempenho do Windows para os nós no [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] .  
  
|Nome da coluna|Tipo de Dados|Description|Intervalo|  
|-----------------|---------------|-----------------|-----------|  
|pdw_node_id|**int**|A ID do nó que contém o contador.<br /><br /> pdw_node_id e counter_name formate a chave para essa exibição.|Consulte node_id em [Sys. dm_pdw_nodes &#40;&#41;do Transact-SQL ](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-nodes-transact-sql.md).|  
|counter_name|**nvarchar (255)**|Nome do contador de desempenho do Windows.||  
|counter_category|**nvarchar (255)**|Nome da categoria do contador de desempenho do Windows.||  
|instance_name|**nvarchar (255)**|Nome da instância específica do contador.||  
|counter_value|**Decimal (38, 10)**|Valor atual do contador.||  
|last_update_time|**Datetime2 (3)**|Carimbo de data/hora da última vez em que o valor foi atualizado.||  
  
## <a name="see-also"></a>Consulte Também  
 [Exibições de gerenciamento dinâmico de SQL Data Warehouse e paralelo data warehouse &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
