---
title: sys.dm_pdw_nodes (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: ''
ms.prod_service: sql-data-warehouse, pdw
ms.service: sql-data-warehouse
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 93966909-d758-4d50-950b-f5066d104fa6
caps.latest.revision: 7
author: barbkess
ms.author: barbkess
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 289ac2e7900368b2fd6c86bfa4876292e21a9e6c
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2018
---
# <a name="sysdmpdwnodes-transact-sql"></a>sys.dm_pdw_nodes (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  Contém informações sobre todos os nós no [!INCLUDE[ssAPS](../../includes/ssaps-md.md)]. Ele lista uma linha por nó no dispositivo.  
  
|Nome da coluna|Tipo de dados|Description|Intervalo|  
|-----------------|---------------|-----------------|-----------|  
|pdw_node_id|**Int**|Id numérico exclusivo associado ao nó.<br /><br /> Chave para este modo de exibição.|Exclusivo por dispositivo, independentemente do tipo.|  
|Tipo|**nvarchar(32)**|Tipo do nó.|'COMPUTE', 'CONTROLE', 'MANAGEMENT'|  
|nome|**nvarchar(32)**|Nome lógico do nó.|Qualquer cadeia de caracteres de tamanho apropriado.|  
|address|**nvarchar(32)**|Endereço IP deste nó.|No formato de [0-255]. [0-255]. [0-255]. [0-255].|  
|is_passive|**Int**|Indica se a máquina virtual em execução no nó está em execução no servidor atribuído ou falhou para o servidor de reserva.|0 – VM do nó está em execução no servidor original.<br /><br /> 1 – VM do nó está em execução no servidor de substituição.|  
|região|**nvarchar(32)**|A região onde o nó está em execução.|'PDW', 'HDINSIGHT'|  
  
## <a name="see-also"></a>Consulte também  
 [SQL Data Warehouse Parallel Data Warehouse e exibições de gerenciamento dinâmico &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
