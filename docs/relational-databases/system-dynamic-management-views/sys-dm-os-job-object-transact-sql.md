---
title: sys.dm_os_job_object (banco de dados SQL) | Microsoft Docs
ms.custom: ''
ms.date: 04/17/2018
ms.service: sql-database
ms.reviewer: ''
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
author: CarlRabeler
ms.author: carlrab
manager: craigg
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: 074981f19f0eb74a7e7c7d4e82466957f0ff98b8
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63047030"
---
# <a name="sysdmosjobobject-azure-sql-database"></a>sys.dm_os_job_object (banco de dados SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

Retorna uma única linha descrevendo a configuração do objeto de trabalho que gerencia o processo do SQL Server, bem como algumas estatísticas de consumo de recursos no nível do objeto de trabalho. Retorna um conjunto vazio se o SQL Server não está em execução em um objeto de trabalho. 

Um objeto de trabalho é uma construção Windows que implementa a governança de recursos de CPU, memória e e/s no nível do sistema operacional. Para obter mais informações sobre objetos de trabalho, consulte [objetos de trabalho](/windows/desktop/ProcThread/job-objects). 
  
|Colunas|Tipo de Dados|Descrição|  
|-------------|---------------|-----------------|  
|cpu_rate|**int**|Especifica a parte de ciclos de processador que os threads do SQL Server podem usar durante cada intervalo de agendamento. O valor é relatado como um percentual de ciclos disponíveis dentro de um intervalo de agendamento do ciclo de 10000. Por exemplo, a valor 100 significa que os threads podem usar núcleos de CPU é sua capacidade total.|
|cpu_affinity_mask|**bigint**|Uma máscara de bits que descreve quais processadores lógicos o processo do SQL Server pode usar dentro do grupo de processador. Por exemplo, cpu_affinity_mask 255 (1111 1111 em binário) significa que os primeiros oito processadores lógicos podem ser usados.|
|cpu_affinity_group|**int**|O número do grupo de processador que é usado pelo SQL Server.|
|memory_limit_mb|**bigint**|A quantidade máxima de memória confirmada, em MB, que todos os processos no objeto de trabalho, incluindo o SQL Server, podem usar de forma cumulativa.| 
|process_memory_limit_mb |**bigint**|A quantidade máxima de memória confirmada, em MB, o que um único processo no objeto de trabalho, como o SQL Server, pode usar.|
|workingset_limit_mb |**bigint**|A quantidade máxima de memória, em MB, o que o conjunto de trabalho do SQL Server pode usar.|
|non_sos_mem_gap_mb|**bigint**|A quantidade de memória em MB, reservar para as pilhas de thread, DLLs e outras alocações de memória não-SOS. Memória de destino do SOS é a diferença entre `process_memory_limit_mb` e `non_sos_mem_gap_mb`.| 
|low_mem_signal_threshold_mb|**bigint**|Um limite de memória, em MB. Quando a quantidade de memória disponível para o objeto de trabalho estiver abaixo desse limite, um sinal de notificação de memória insuficiente é enviado para o processo do SQL Server. |
|total_user_time|**bigint**|O número total de tiques de 100 ns que os threads dentro do objeto de trabalho tê gasto no modo de usuário, desde que o objeto de trabalho foi criado. |
|total_kernel_time |**bigint**|O número total de tiques de 100 ns que os threads dentro do objeto de trabalho tê gasto no modo kernel, desde que o objeto de trabalho foi criado. |
|write_operation_count |**bigint**|O número total de gravar operações de e/s nos discos locais emitidas pelo SQL Server, desde que o objeto de trabalho foi criado. |
|read_operation_count |**bigint**|O número total de operações de e/s de leitura em discos locais emitidas pelo SQL Server, desde que o objeto de trabalho foi criado. |
|peak_process_memory_used_mb|**bigint**|Quantidade máxima de memória, em MB, o que um único processo no objeto de trabalho, como o SQL Server tem usado uma vez que o objeto de trabalho foi criado.| 
|peak_job_memory_used_mb|**bigint**|Quantidade máxima de memória em MB, que todos os processos no objeto de trabalho tenham usado cumulativamente desde o objeto de trabalho foi criada.|
  
## <a name="permissions"></a>Permissões  
Na instância de gerenciada de banco de dados de SQL, requer `VIEW SERVER STATE` permissão. No banco de dados SQL requer o `VIEW DATABASE STATE` permissão no banco de dados.  
 
## <a name="see-also"></a>Consulte também  

Para obter informações sobre instâncias gerenciadas, consulte [instância gerenciada do banco de dados do SQL](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance).
  
