---
title: sys. dm_pdw_nodes (Transact-SQL) | Microsoft Docs
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
ms.openlocfilehash: 9ba367379795408a79b412c5b4c04097484bfd2b
ms.sourcegitcommit: 01297f2487fe017760adcc6db5d1df2c1234abb4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/09/2020
ms.locfileid: "86197213"
---
# <a name="sysdm_pdw_nodes-transact-sql"></a>sys. dm_pdw_nodes (Transact-SQL)
[!INCLUDE[applies-to-version/asa-pdw](../../includes/applies-to-version/asa-pdw.md)]

  Contém informações sobre todos os nós no [!INCLUDE[ssAPS](../../includes/ssaps-md.md)] . Ele lista uma linha por nó no dispositivo.  
  
|Nome da coluna|Tipo de dados|Descrição|Intervalo|  
|-----------------|---------------|-----------------|-----------|  
|pdw_node_id|**int**|ID numérica exclusiva associada ao nó.<br /><br /> Chave para esta exibição.|Exclusivo em todo o dispositivo, independentemente do tipo.|  
|tipo|**nvarchar(32)**|Tipo do nó.|' COMPUTAÇÃO ', ' CONTROLE ', ' GERENCIAMENTO '|  
|name|**nvarchar(32)**|Nome lógico do nó.|Qualquer cadeia de caracteres de comprimento apropriado.|  
|address|**nvarchar(32)**|Endereço IP deste nó.|No formato [0-255]. [0-255]. [0-255]. [0-255].|  
|is_passive|**int**|Indica se a máquina virtual que está executando o nó está em execução no servidor atribuído ou se passou por failover para o servidor sobressalente.|a VM de 0 nó está em execução no servidor original.<br /><br /> a VM de 1 nó está em execução no servidor sobressalente.|  
|region|**nvarchar(32)**|A região em que o nó está sendo executado.|' PDW ', ' HDINSIGHT '|  
  
## <a name="see-also"></a>Consulte Também  
 [Exibições de gerenciamento dinâmico de SQL Data Warehouse e paralelo data warehouse &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
