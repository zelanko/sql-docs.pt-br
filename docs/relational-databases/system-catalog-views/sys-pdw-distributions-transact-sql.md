---
title: sys.pdw_distributions (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: ''
ms.prod_service: sql-data-warehouse, pdw
ms.service: sql-data-warehouse
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 572b5187-9753-4063-adf8-65dea87d11f8
caps.latest.revision: 7
author: ronortloff
ms.author: rortloff
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 49c439e4d3b210025dfd28f45cd63b9bfcb5620d
ms.sourcegitcommit: d2573a8dec2d4102ce8882ee232cdba080d39628
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/07/2018
---
# <a name="syspdwdistributions-transact-sql"></a>sys.pdw_distributions (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  Contém informações sobre as distribuições no dispositivo. Ele lista uma linha por distribuição de dispositivo.  
  
|Nome da coluna|Tipo de dados|Description|Intervalo|  
|-----------------|---------------|-----------------|-----------|  
|distribution_id|**Int**|Id numérico exclusivo associado com a distribuição.<br /><br /> Chave para este modo de exibição.|1 para o número de nós de computação no dispositivo multiplicado pelo número de Distribuições por nó de computação.|  
|pdw_node_id|**Int**|ID do nó que essa distribuição é no.|Consulte pdw_node_id em [sys.dm_pdw_nodes &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-nodes-transact-sql.md).|  
|nome|**nvarchar(32)**|Cadeia de caracteres associada à distribuição, usada como um sufixo de tabelas distribuídas de identificador.|Cadeia de caracteres composta de 'A-Z', 'a-z','0-9', '_','-'.|  
|position|**Int**|Posição da distribuição em um nó respectivo para outras distribuições nesse nó.|1 para o número de Distribuições por nó.|  
  
## <a name="see-also"></a>Consulte também  
 [SQL Data Warehouse e exibições de catálogo do Parallel Data Warehouse](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)  
  
  
