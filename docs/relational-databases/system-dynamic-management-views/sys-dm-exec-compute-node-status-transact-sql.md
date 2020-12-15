---
description: sys.dm_exec_compute_node_status (Transact-SQL)
title: sys.dm_exec_compute_node_status (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2019
ms.prod: sql
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
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
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: c8a6f223faf5933843be00d689abb4234c61013b
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97428036"
---
# <a name="sysdm_exec_compute_node_status-transact-sql"></a>sys.dm_exec_compute_node_status (Transact-SQL)
[!INCLUDE [sqlserver2016-asa-pdw](../../includes/applies-to-version/sqlserver2016-asa-pdw.md)]

  Contém informações adicionais sobre o desempenho e o status de todos os nós do polybase. Lista uma linha por nó.  
  
|Nome da coluna|Tipo de Dados|DESCRIÇÃO|Intervalo|  
|-----------------|---------------|-----------------|-----------|  
|compute_node_id|`int`|ID numérica exclusiva associada ao nó.|Exclusivo entre o cluster de escala horizontal, independentemente do tipo.|  
|process_id|`int`|||  
|process_name|`nvarchar(255)`|Nome lógico do nó.|Qualquer cadeia de caracteres de comprimento apropriado.|  
|allocated_memory|`bigint`|Memória total alocada neste nó.||  
|available_memory|`bigint`|Memória total disponível neste nó.||  
|process_cpu_usage|`bigint`|Uso total da CPU do processo, em tiques.||  
|total_cpu_usage|`bigint`|Uso total da CPU, em tiques.||  
|thread_count|`bigint`|Número total de threads em uso neste nó.||  
|handle_count|`bigint`|Número total de identificadores em uso neste nó.||  
|total_elapsed_time|`bigint`|Tempo total decorrido desde a inicialização ou reinicialização do sistema.|Tempo total decorrido desde a inicialização ou reinicialização do sistema. Se total_elapsed_time exceder o valor máximo de um inteiro (24,8 dias em milissegundos), isso causará falha de materialização devido ao estouro. O valor máximo em milissegundos é equivalente a 24,8 dias.|  
|is_available|`bit`|Sinalizador que indica se esse nó está disponível.||  
|sent_time|`datetime`|Última vez que um pacote de rede foi enviado por este||  
|received_time|`datetime`|Última vez que um pacote de rede foi enviado por este nó.||  
|error_id|`nvarchar(36)`|Identificador exclusivo do último erro que ocorreu neste nó.||
|compute_pool_id|`int`|Identificador exclusivo do pool.|

## <a name="see-also"></a>Consulte Também  
 [Solução de problemas do polybase com exibições de gerenciamento dinâmico](/previous-versions/sql/sql-server-2016/mt146389(v=sql.130))   
 [Exibições e funções de gerenciamento dinâmico &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Exibições de gerenciamento dinâmico relacionadas ao banco de dados &#40;&#41;Transact-SQL ](../../relational-databases/system-dynamic-management-views/database-related-dynamic-management-views-transact-sql.md)  
  
