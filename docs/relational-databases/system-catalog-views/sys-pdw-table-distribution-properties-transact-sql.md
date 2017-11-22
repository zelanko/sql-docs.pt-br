---
title: sys.pdw_table_distribution_properties (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/04/2017
ms.prod: 
ms.prod_service: sql-data-warehouse, pdw
ms.service: sql-data-warehouse
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: TSQL
ms.assetid: 639a7475-7c92-41e0-a8ab-ad630eb5aea3
caps.latest.revision: "9"
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 4b0c8b3b637fbf46edb599e6ab39804ec16bac8b
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="syspdwtabledistributionproperties-transact-sql"></a>sys.pdw_table_distribution_properties (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  Contém informações de distribuição para tabelas.  
  
|Nome da coluna|Tipo de dados|Description|Intervalo|  
|-----------------|---------------|-----------------|-----------|  
|**object_id**|**int**|ID da tabela para qual três propriedades foram especificadas.||  
|**distribution_policy**|**tinyint**|0 = INDEFINIDO<br /><br /> 1 = NENHUM<br /><br /> 2 = HASH<br /><br /> 3 = REPLICAR<br /><br /> 4 = ROUND_ROBIN|REPLICATE só se aplica a [!INCLUDE[ssPDW](../../includes/sspdw-md.md)].|  
|**distribution_policy_desc**|**nvarchar (60)**|INDEFINIDO, NONE, HASH, REPLICAR, SEGMENTED_HEAP|[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]Retorna o HASH ou REPLICATE.|  
  
## <a name="see-also"></a>Consulte também  
 [SQL Data Warehouse e exibições de catálogo do Parallel Data Warehouse](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)  
  
  
