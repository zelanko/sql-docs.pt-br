---
title: sys.dm_pdw_node_status (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-non-specified
ms.prod_service: pdw
ms.service: 
ms.component: dmv's
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 8e263b65-81d0-49d0-8873-62ef424369d6
caps.latest.revision: 
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: d7374f3cf3924ad12fc7077ec8fdc46fa91ec295
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/03/2018
---
# <a name="sysdmpdwnodestatus-transact-sql"></a>sys.dm_pdw_node_status (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md.md)]

  Contém informações adicionais (sobre [sys.dm_pdw_nodes &#40; Transact-SQL &#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-nodes-transact-sql.md)) sobre o desempenho e o status de todos os nós de dispositivo. Ele lista uma linha por nó no dispositivo.  
  
|Nome da coluna|Tipo de dados|Description|Intervalo|  
|-----------------|---------------|-----------------|-----------|  
|pdw_node_id|**Int**|Id numérico exclusivo associado ao nó.<br /><br /> Chave para este modo de exibição.|Exclusivo por dispositivo, independentemente do tipo.|  
|process_id|**Int**|[!INCLUDE[ssInfoNA](../../includes/ssinfona-md.md)]||  
|nome_do processo|**nvarchar(255)**|[!INCLUDE[ssInfoNA](../../includes/ssinfona-md.md)]||  
|allocated_memory|**bigint**|Total alocada memória neste nó.||  
|available_memory|**bigint**|Total de memória disponível neste nó.||  
|process_cpu_usage|**bigint**|Uso de CPU total do processo em tiques.||  
|total_cpu_usage|**bigint**|Uso total de CPU, em tiques.||  
|thread_count|**bigint**|Número total de segmentos em uso neste nó.||  
|handle_count|**bigint**|Número total de identificadores em uso neste nó.||  
|total_elapsed_time|**bigint**|Tempo total decorrido desde que o sistema iniciar ou reiniciar.|Tempo total decorrido desde que o sistema iniciar ou reiniciar. Se total_elapsed_time excede o valor máximo para um inteiro (24.8 dias em milissegundos), isso causará falha materialização devido ao estouro.<br /><br /> O valor máximo em milissegundos é equivalente a 24.8 dias.|  
|is_available|**bit**|Sinalizador que indica se este nó estará disponível.||  
|sent_time|**datetime**|Última vez em que um pacote de rede foi enviado por este nó.||  
|received_time|**datetime**|Última vez em que um pacote de rede foi recebido por este nó.||  
|error_id|**nvarchar(36)**|Identificador exclusivo do último erro ocorrido neste nó.||  
  
## <a name="see-also"></a>Consulte também  
 [SQL Data Warehouse e exibições de gerenciamento dinâmico do Parallel Data Warehouse &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
