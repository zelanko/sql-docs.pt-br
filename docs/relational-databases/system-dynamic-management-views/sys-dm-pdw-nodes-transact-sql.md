---
description: sys.dm_pdw_nodes (Transact-SQL)
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
ms.openlocfilehash: b758dafadc743ffc6c51c6d1c94ab3a5ea597e2d
ms.sourcegitcommit: 22dacedeb6e8721e7cdb6279a946d4002cfb5da3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/14/2020
ms.locfileid: "92037679"
---
# <a name="sysdm_pdw_nodes-transact-sql"></a>sys.dm_pdw_nodes (Transact-SQL)
[!INCLUDE[applies-to-version/asa-pdw](../../includes/applies-to-version/asa-pdw.md)]

  Contém informações sobre todos os nós no [!INCLUDE[ssAPS](../../includes/ssaps-md.md)] . Ele lista uma linha por nó no dispositivo.  
  
|Nome da coluna|Tipo de Dados|DESCRIÇÃO|Intervalo|  
|-----------------|---------------|-----------------|-----------|  
|pdw_node_id|**int**|ID numérica exclusiva associada ao nó.<br /><br /> Chave para esta exibição.|Exclusivo em todo o dispositivo, independentemente do tipo.|  
|tipo|**nvarchar(32)**|Tipo do nó.|' COMPUTAÇÃO ', ' CONTROLE ', ' GERENCIAMENTO '|  
|name|**nvarchar(32)**|Nome lógico do nó.|Qualquer cadeia de caracteres de comprimento apropriado.|  
|address|**nvarchar(32)**|Endereço IP deste nó.|No formato [0-255]. [0-255]. [0-255]. [0-255].|  
|is_passive|**int**|Indica se a máquina virtual que está executando o nó está em execução no servidor atribuído ou se passou por failover para o servidor sobressalente.|a VM de 0 nó está em execução no servidor original.<br /><br /> a VM de 1 nó está em execução no servidor sobressalente.|  
|region|**nvarchar(32)**|A região em que o nó está sendo executado.|' PDW ', ' HDINSIGHT '|  
  
## <a name="see-also"></a>Consulte Também  
 [Exibições de gerenciamento dinâmico do Azure Synapse Analytics e Parallel data warehouse &#40;&#41;de Transact-SQL ](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
