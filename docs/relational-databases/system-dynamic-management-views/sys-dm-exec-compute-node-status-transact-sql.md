---
title: DM exec_compute_node_status (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- DM_EXEC_COMPUTE_NODE_STATUS_TSQL
- DM_EXEC_COMPUTE_NODE_STATUS
dev_langs:
- TSQL
helpviewer_keywords:
- PolyBase,views
- PolyBase
- dm_exec_compute_node_status
- sys.dm_exec_compute_node_status management view
ms.assetid: b606f91f-3a08-4a4f-bb57-32ae155b3738
caps.latest.revision: 7
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>=aps-pdw-2016||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017'
ms.openlocfilehash: 8e54bb1e05da7a8575b6b6a9b84abeea7cb9984a
ms.sourcegitcommit: 4cd008a77f456b35204989bbdd31db352716bbe6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/06/2018
ms.locfileid: "39540416"
---
# <a name="sysdmexeccomputenodestatus-transact-sql"></a>sys.dm_exec_compute_node_status (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2016-xxxx-asdw-pdw-md.md)]

  Contém informações adicionais sobre o desempenho e o status de todos os nós PolyBase. Lista uma linha por nó.  
  
|Nome da coluna|Tipo de dados|Description|Intervalo|  
|-----------------|---------------|-----------------|-----------|  
|compute_node_id|**int**|Id numérico exclusivo associado ao nó.|Exclusivo em todo o cluster de escala horizontal, independentemente do tipo.|  
|process_id|**int**|||  
|nome_do processo|**nvarchar(255)**|Nome lógico do nó.|Qualquer cadeia de caracteres de tamanho apropriado.|  
|allocated_memory|**bigint**|Total alocado de memória neste nó.||  
|available_memory|**bigint**|Total de memória disponível neste nó.||  
|process_cpu_usage|**bigint**|Uso de CPU do processo total, em tiques.||  
|total_cpu_usage|**bigint**|Uso total de CPU, em tiques.||  
|thread_count|**bigint**|Número total de threads em uso neste nó.||  
|handle_count|**bigint**|Número total de identificadores em uso neste nó.||  
|total_elapsed_time|**bigint**|Tempo total decorrido desde que o sistema iniciar ou reiniciar.|Tempo total decorrido desde que o sistema iniciar ou reiniciar. Se total_elapsed_time exceder o valor máximo para um inteiro (24,8 dias em milissegundos), ela causará falha de materialização devido a estouro. O valor máximo em milissegundos é equivalente a 24,8 dias.|  
|is_available|**bit**|Sinalizador que indica se este nó está disponível.||  
|sent_time|**datetime**|Última vez em um pacote de rede foi enviado por este||  
|received_time|**datetime**|Última vez em um pacote de rede foi enviado por este nó.||  
|error_id|**nvarchar(36)**|Identificador exclusivo do último erro que ocorreu nesse nó.||  
  
## <a name="see-also"></a>Consulte também  
 [Solução de problemas com exibições de gerenciamento dinâmico do PolyBase](http://msdn.microsoft.com/library/ce9078b7-a750-4f47-b23e-90b83b783d80)   
 [Exibições e funções de gerenciamento dinâmico &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Banco de dados relacionados a exibições de gerenciamento dinâmico &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/database-related-dynamic-management-views-transact-sql.md)  
  
  
