---
description: sys. dm_pdw_node_status (Transact-SQL)
title: sys. dm_pdw_node_status (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 8e263b65-81d0-49d0-8873-62ef424369d6
author: CarlRabeler
ms.author: carlrab
monikerRange: '>= aps-pdw-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: b93d177ad3f73982386407e019629401d70ec57f
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88447479"
---
# <a name="sysdm_pdw_node_status-transact-sql"></a>sys. dm_pdw_node_status (Transact-SQL)
[!INCLUDE [pdw](../../includes/applies-to-version/pdw.md)]

  Contém informações adicionais (sobre [Sys. dm_pdw_nodes &#40;&#41;Transact-SQL ](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-nodes-transact-sql.md)) sobre o desempenho e o status de todos os nós do dispositivo. Ele lista uma linha por nó no dispositivo.  
  
|Nome da coluna|Tipo de Dados|DESCRIÇÃO|Intervalo|  
|-----------------|---------------|-----------------|-----------|  
|pdw_node_id|**int**|ID numérica exclusiva associada ao nó.<br /><br /> Chave para esta exibição.|Exclusivo em todo o dispositivo, independentemente do tipo.|  
|process_id|**int**|[!INCLUDE[ssInfoNA](../../includes/ssinfona-md.md)]||  
|process_name|**nvarchar(255)**|[!INCLUDE[ssInfoNA](../../includes/ssinfona-md.md)]||  
|allocated_memory|**bigint**|Memória total alocada neste nó.||  
|available_memory|**bigint**|Memória total disponível neste nó.||  
|process_cpu_usage|**bigint**|Uso total da CPU do processo, em tiques.||  
|total_cpu_usage|**bigint**|Uso total da CPU, em tiques.||  
|thread_count|**bigint**|Número total de threads em uso neste nó.||  
|handle_count|**bigint**|Número total de identificadores em uso neste nó.||  
|total_elapsed_time|**bigint**|Tempo total decorrido desde a inicialização ou reinicialização do sistema.|Tempo total decorrido desde a inicialização ou reinicialização do sistema. Se total_elapsed_time exceder o valor máximo de um inteiro (24,8 dias em milissegundos), isso causará falha de materialização devido ao estouro.<br /><br /> O valor máximo em milissegundos é equivalente a 24,8 dias.|  
|is_available|**bit**|Sinalizador que indica se esse nó está disponível.||  
|sent_time|**datetime**|Última vez que um pacote de rede foi enviado por este nó.||  
|received_time|**datetime**|Última vez que um pacote de rede foi recebido por este nó.||  
|error_id|**nvarchar (36)**|Identificador exclusivo do último erro que ocorreu neste nó.||  
  
## <a name="see-also"></a>Consulte Também  
 [Exibições de gerenciamento dinâmico de SQL Data Warehouse e paralelo data warehouse &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
