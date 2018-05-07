---
title: sys.dm_os_job_object (banco de dados do SQL Azure) | Microsoft Docs
ms.custom: ''
ms.date: 04/17/2018
ms.prod: ''
ms.prod_service: sql-database
ms.reviewer: ''
ms.service: sql-database
ms.component: dmv's
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.dm_db_resource_stats
- sys.dm_db_resource_stats_TSQL
- dm_db_resource_stats
- dm_db_resource_stats_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_db_resource_stats
- dm_db_resource_stats
ms.assetid: 6e76b39f-236e-4bbf-b0b5-38be190d81e8
caps.latest.revision: 11
author: CarlRabeler
ms.author: carlrab
manager: craigg
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: 1924f6c606d2d07d816409278cf9af56ecd868f8
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2018
---
# <a name="sysdmosjobobject-azure-sql-database"></a>sys.dm_os_job_object (banco de dados do SQL Azure)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

Retorna uma única linha que descreve a configuração do objeto de trabalho que gerencia o processo do SQL Server, bem como algumas estatísticas de consumo de recursos no nível do objeto de trabalho. Retorna um conjunto vazio se o SQL Server não está em execução em um objeto de trabalho. 

Um objeto de trabalho é uma construção Windows que implementa o controle de recursos de CPU, memória e e/s no nível do sistema operacional. Para obter mais informações sobre objetos de trabalho, consulte [objetos de trabalho](https://msdn.microsoft.com/library/windows/desktop/ms684161.aspx). 

> [!NOTE]
> O sys.dm_os_job_object DMV atualmente pode aparecer como sys.dm_job_object. Isso é temporário: `sys.dm_os_job_object` será o nome permanente dessa DMV. 
  
|Colunas|Tipo de Dados|Description|  
|-------------|---------------|-----------------|  
|cpu_rate|**Int**|Especifica a parte de ciclos do processador que os threads do SQL Server podem usar durante cada intervalo de agendamento. O valor será relatado como um percentual de ciclos disponíveis dentro de um intervalo de agendamento do ciclo de 10000. Por exemplo, o valor de 100 significa que os threads podem usar núcleos de CPU é sua capacidade total.|
|cpu_affinity_mask|**bigint**|Uma máscara de bits que descreve quais processadores lógicos processo do SQL Server pode usar dentro do grupo de processador. Por exemplo, cpu_affinity_mask 255 (1111 1111 em binário) significa que os oito primeiros processadores lógicos podem ser usados.|
|cpu_affinity_group|**Int**|O número do grupo de processador que é usado pelo SQL Server.|
|memory_limit_mb|**bigint**|A quantidade máxima de memória confirmada, em MB, que todos os processos no objeto de trabalho, incluindo o SQL Server, podem usar cumulativamente.| 
|process_memory_limit_mb |**bigint**|A quantidade máxima de memória confirmada, em MB, o que pode usar um único processo no objeto de trabalho, como o SQL Server.|
|workingset_limit_mb |**bigint**|A quantidade máxima de memória, em MB, o que pode usar o conjunto de trabalho do SQL Server.|
|non_sos_mem_gap_mb|**bigint**|A quantidade de memória em MB, reservou para pilhas de thread, DLLs e outras alocações de memória não SOS. Memória de destino SOS é a diferença entre `process_memory_limit_mb` e `non_sos_mem_gap_mb`.| 
|low_mem_signal_threshold_mb|**bigint**|Um limite de memória, em MB. Quando a quantidade de memória disponível para o objeto de trabalho estiver abaixo desse limite, um sinal de notificação de memória baixa é enviado para o processo do SQL Server. |
|total_user_time|**bigint**|O número total de tiques de 100 ns threads dentro do objeto de trabalho ter gasto no modo de usuário, desde que o objeto de trabalho foi criado. |
|total_kernel_time |**bigint**|O número total de tiques de 100 ns threads dentro do objeto de trabalho ter gasto no modo de kernel, desde que o objeto de trabalho foi criado. |
|write_operation_count |**bigint**|O número total de operações de gravação e/s em discos locais emitidas pelo SQL Server, desde que o objeto de trabalho foi criado. |
|read_operation_count |**bigint**|O número total de operações de e/s de leitura em discos locais emitidas pelo SQL Server, desde que o objeto de trabalho foi criado. |
|peak_process_memory_used_mb|**bigint**|A quantidade máxima de memória, em MB, o que um único processo no objeto de trabalho, como o SQL Server, foi usado desde que o objeto de trabalho foi criado.| 
|peak_job_memory_used_mb|**bigint**|A quantidade máxima de memória, em MB, que todos os processos no objeto de trabalho usaram cumulativamente desde o objeto de trabalho foi criada.|
  
## <a name="permissions"></a>Permissões  
No SQL banco de dados gerenciado instância requer `VIEW SERVER STATE` permissão. No banco de dados SQL, requer o `VIEW DATABASE STATE` no banco de dados.  
 
## <a name="see-also"></a>Consulte também  

Para obter informações sobre instâncias gerenciadas, consulte [instância gerenciada do banco de dados do SQL](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance).
  
