---
title: sys.pdw_distributions (Transact-SQL) | Microsoft Docs
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
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: a1ff7801ef639ff8b8783296638ae571939ed1ca
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/11/2019
ms.locfileid: "56040199"
---
# <a name="syspdwdistributions-transact-sql"></a>sys.pdw_distributions (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  Contém informações sobre as distribuições no dispositivo. Ele lista uma linha por distribuição de dispositivo.  
  
|Nome da coluna|Tipo de Dados|Descrição|Intervalo|  
|-----------------|---------------|-----------------|-----------|  
|distribution_id|**int**|Id numérico exclusivo associado com a distribuição.<br /><br /> A chave para este modo de exibição.|1 ao número de nós de computação no dispositivo multiplicado pelo número de Distribuições por nó de computação.|  
|pdw_node_id|**int**|ID do nó que essa distribuição é no.|Consulte pdw_node_id na [sys.dm_pdw_nodes &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-nodes-transact-sql.md).|  
|nome|**nvarchar(32)**|Identificador associado com a distribuição, usada como um sufixo de tabelas distribuídas de cadeia de caracteres.|Cadeia de caracteres composta de 'A-Z', 'a-z','0-9', '_','-'.|  
|position|**int**|Posição da distribuição dentro de um nó respectivo para outras distribuições nesse nó.|1 ao número de Distribuições por nó.|  
  
## <a name="see-also"></a>Consulte também  
 [SQL Data Warehouse e Parallel Data Warehouse exibições do catálogo](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)  
  
  
