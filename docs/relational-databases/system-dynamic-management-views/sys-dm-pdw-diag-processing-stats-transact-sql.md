---
title: sys. dm_pdw_diag_processing_stats (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: df659c55-4f63-45f8-8afe-ce300031bc5b
author: CarlRabeler
ms.author: carlrab
monikerRange: '>= aps-pdw-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: aac1c35f86b0d7f9d12405cb25136015afb5a52b
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/05/2020
ms.locfileid: "82811281"
---
# <a name="sysdm_pdw_diag_processing_stats-transact-sql"></a>sys. dm_pdw_diag_processing_stats (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md.md)]

  Exibe informações relacionadas a todos os eventos de diagnóstico internos que podem ser incorporados em sessões de diagnóstico definidas pelo administrador. Consulte esta exibição para entender as estatísticas por trás dos subsistemas de diagnóstico e eventos que orientam a população de todas as outras DMVs. Há um grupo de filas para cada processo em cada nó.  
  
|Nome da coluna|Tipo de Dados|Description|  
|-----------------|---------------|-----------------|  
|**pdw_node_id**|**int**|Nó do dispositivo do qual este log se encontra.|  
|**process_id**|**int**|Identificador do processo que executa o envio dessa estatística.|  
|**target_name**|**nvarchar (255)**|O nome da fila.|  
|**queue_size**|**int**|O número de itens na fila de processos. O tamanho da fila geralmente é 0. Um número positivo indica que o sistema está sob estresse e está criando a pendência de eventos. Uma contagem positiva nas outras colunas significa que o sistema se tornou corrompido para essa fila específica e quaisquer DMVs relacionados.|  
|**lost_events_count**|**bigint**|O número de eventos perdidos.|  
  
## <a name="see-also"></a>Consulte Também  
 [Exibições de gerenciamento dinâmico de SQL Data Warehouse e paralelo data warehouse &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
