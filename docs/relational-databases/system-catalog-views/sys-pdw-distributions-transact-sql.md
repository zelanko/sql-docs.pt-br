---
description: sys. pdw_distributions (Transact-SQL)
title: sys. pdw_distributions (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 572b5187-9753-4063-adf8-65dea87d11f8
author: ronortloff
ms.author: rortloff
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 826a484a1a488b71806525fbeb4b6fd36f283ab5
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88377012"
---
# <a name="syspdw_distributions-transact-sql"></a>sys. pdw_distributions (Transact-SQL)
[!INCLUDE[applies-to-version/asa-pdw](../../includes/applies-to-version/asa-pdw.md)]

  Contém informações sobre as distribuições no dispositivo. Ele lista uma linha por distribuição de dispositivo.  
  
|Nome da coluna|Tipo de Dados|DESCRIÇÃO|Intervalo|  
|-----------------|---------------|-----------------|-----------|  
|distribution_id|**int**|ID numérica exclusiva associada à distribuição.<br /><br /> Chave para esta exibição.|1 para o número de nós de computação no dispositivo multiplicado pelo número de distribuições por nó de computação.|  
|pdw_node_id|**int**|ID do nó em que esta distribuição está.|Consulte pdw_node_id em [Sys. dm_pdw_nodes &#40;&#41;do Transact-SQL ](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-nodes-transact-sql.md).|  
|name|**nvarchar(32)**|Identificador de cadeia de caracteres associado à distribuição, usado como um sufixo em tabelas distribuídas.|Cadeia de caracteres composta de ' A-Z ', ' a-z ', ' 0-9 ', ' _ ', '-'.|  
|position|**int**|Posição da distribuição em um nó correspondente a outras distribuições nesse nó.|1 para o número de distribuições por nó.|  
  
## <a name="see-also"></a>Consulte Também  
 [Exibições de Catálogo do SQL Data Warehouse e Parallel Data Warehouse](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)  
  
  
