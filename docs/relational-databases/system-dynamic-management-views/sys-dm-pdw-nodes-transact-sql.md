---
title: sys.dm_pdw_nodes (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: ''
ms.prod_service: sql-data-warehouse, pdw
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 93966909-d758-4d50-950b-f5066d104fa6
author: ronortloff
ms.author: rortloff
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: ff3f6c31389622dc424c42e06bfa78477c70cde2
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47769364"
---
# <a name="sysdmpdwnodes-transact-sql"></a>sys.dm_pdw_nodes (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  Contém informações sobre todos os nós no [!INCLUDE[ssAPS](../../includes/ssaps-md.md)]. Ele lista uma linha por nó no dispositivo.  
  
|Nome da coluna|Tipo de dados|Description|Intervalo|  
|-----------------|---------------|-----------------|-----------|  
|pdw_node_id|**int**|Id numérico exclusivo associado ao nó.<br /><br /> A chave para este modo de exibição.|Exclusivo em todo o dispositivo, independentemente do tipo.|  
|Tipo|**nvarchar(32)**|Tipo de nó.|'GERENCIAMENTO DE COMPUTAÇÃO', 'CONTROL',' '|  
|nome|**nvarchar(32)**|Nome lógico do nó.|Qualquer cadeia de caracteres de tamanho apropriado.|  
|address|**nvarchar(32)**|Endereço IP deste nó.|No formato de [0-255]. [0 a 255]. [0 a 255]. [0 a 255].|  
|is_passive|**int**|Indica se a máquina virtual executando o nó está em execução no servidor atribuído ou realizou o failover para o servidor de reserva.|0 – VM do nó está em execução no servidor original.<br /><br /> 1 – VM do nó está em execução no servidor de reserva.|  
|região|**nvarchar(32)**|A região onde o nó está em execução.|'PDW', 'HDINSIGHT'|  
  
## <a name="see-also"></a>Consulte também  
 [SQL Data Warehouse e Parallel Data Warehouse exibições de gerenciamento dinâmico &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
