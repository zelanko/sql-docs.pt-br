---
title: sys.dm_pdw_node_status (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 8e263b65-81d0-49d0-8873-62ef424369d6
author: stevestein
ms.author: sstein
monikerRange: '>= aps-pdw-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 4cd8788d19b06329d0280efc43a13a9a218e056c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67899366"
---
# <a name="sysdmpdwnodestatus-transact-sql"></a>sys.dm_pdw_node_status (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md.md)]

  Contém informações adicionais (ao longo [sys.dm_pdw_nodes &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-nodes-transact-sql.md)) sobre o desempenho e o status de todos os nós de dispositivo. Ele lista uma linha por nó no dispositivo.  
  
|Nome da coluna|Tipo de dados|Descrição|Intervalo|  
|-----------------|---------------|-----------------|-----------|  
|pdw_node_id|**int**|Id numérico exclusivo associado ao nó.<br /><br /> A chave para este modo de exibição.|Exclusivo em todo o dispositivo, independentemente do tipo.|  
|process_id|**int**|[!INCLUDE[ssInfoNA](../../includes/ssinfona-md.md)]||  
|nome_do processo|**nvarchar(255)**|[!INCLUDE[ssInfoNA](../../includes/ssinfona-md.md)]||  
|allocated_memory|**bigint**|Total alocado de memória neste nó.||  
|available_memory|**bigint**|Total de memória disponível neste nó.||  
|process_cpu_usage|**bigint**|Uso de CPU do processo total, em tiques.||  
|total_cpu_usage|**bigint**|Uso total de CPU, em tiques.||  
|thread_count|**bigint**|Número total de threads em uso neste nó.||  
|handle_count|**bigint**|Número total de identificadores em uso neste nó.||  
|total_elapsed_time|**bigint**|Tempo total decorrido desde que o sistema iniciar ou reiniciar.|Tempo total decorrido desde que o sistema iniciar ou reiniciar. Se total_elapsed_time exceder o valor máximo para um inteiro (24,8 dias em milissegundos), ela causará falha de materialização devido a estouro.<br /><br /> O valor máximo em milissegundos é equivalente a 24,8 dias.|  
|is_available|**bit**|Sinalizador que indica se este nó está disponível.||  
|sent_time|**datetime**|Última vez em um pacote de rede foi enviado por este nó.||  
|received_time|**datetime**|Última vez em um pacote de rede foi recebido por este nó.||  
|error_id|**nvarchar(36)**|Identificador exclusivo do último erro que ocorreu nesse nó.||  
  
## <a name="see-also"></a>Consulte também  
 [SQL Data Warehouse e Parallel Data Warehouse exibições de gerenciamento dinâmico &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
