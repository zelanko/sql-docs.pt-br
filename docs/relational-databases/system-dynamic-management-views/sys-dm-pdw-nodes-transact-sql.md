---
title: sys.dm_pdw_nodes (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 93966909-d758-4d50-950b-f5066d104fa6
author: ronortloff
ms.author: rortloff
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 61593522e09ed86ec10f08a6ad8ff7a941a2e10e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67899346"
---
# <a name="sysdmpdwnodes-transact-sql"></a>sys.dm_pdw_nodes (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  Contém informações sobre todos os nós no [!INCLUDE[ssAPS](../../includes/ssaps-md.md)]. Ele lista uma linha por nó no dispositivo.  
  
|Nome da coluna|Tipo de dados|Descrição|Intervalo|  
|-----------------|---------------|-----------------|-----------|  
|pdw_node_id|**int**|Id numérico exclusivo associado ao nó.<br /><br /> A chave para este modo de exibição.|Exclusivo em todo o dispositivo, independentemente do tipo.|  
|type|**nvarchar(32)**|Tipo de nó.|'GERENCIAMENTO DE COMPUTAÇÃO', 'CONTROL',' '|  
|name|**nvarchar(32)**|Nome lógico do nó.|Qualquer cadeia de caracteres de tamanho apropriado.|  
|endereço|**nvarchar(32)**|Endereço IP deste nó.|No formato de [0-255]. [0 a 255]. [0 a 255]. [0 a 255].|  
|is_passive|**int**|Indica se a máquina virtual executando o nó está em execução no servidor atribuído ou realizou o failover para o servidor de reserva.|0 - VM do nó está em execução no servidor original.<br /><br /> 1 - VM do nó está em execução no servidor de reserva.|  
|região|**nvarchar(32)**|A região onde o nó está em execução.|'PDW', 'HDINSIGHT'|  
  
## <a name="see-also"></a>Consulte também  
 [SQL Data Warehouse e Parallel Data Warehouse exibições de gerenciamento dinâmico &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
