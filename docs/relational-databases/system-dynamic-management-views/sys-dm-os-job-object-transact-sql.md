---
title: sys. dm_os_job_object (banco de dados SQL do Azure) | Microsoft Docs
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
author: julieMSFT
ms.author: jrasnick
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: 43063bb56607d1b5a21ae04b40ee4c7a17825521
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67900141"
---
# <a name="sysdm_os_job_object-azure-sql-database"></a>sys.dm_os_job_object (Banco de Dados SQL do Microsoft Azure)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

Retorna uma única linha que descreve a configuração do objeto de trabalho que gerencia o processo de SQL Server, bem como determinadas estatísticas de consumo de recursos no nível do objeto de trabalho. Retorna um conjunto vazio se SQL Server não estiver em execução em um objeto de trabalho. 

Um objeto de trabalho é uma construção do Windows que implementa a CPU, a memória e a governança de recursos de e/s no nível do sistema operacional. Para obter mais informações sobre objetos de trabalho, consulte [objetos de trabalho](/windows/desktop/ProcThread/job-objects). 
  
|Colunas|Tipo de Dados|DESCRIÇÃO|  
|-------------|---------------|-----------------|  
|cpu_rate|**int**|Especifica a parte dos ciclos do processador que o SQL Server threads pode usar durante cada intervalo de agendamento. O valor é relatado como uma porcentagem de ciclos disponíveis dentro de um intervalo de agendamento de ciclo de 10000. Por exemplo, o valor 100 significa que os threads podem usar os núcleos de CPU como sua capacidade total.|
|cpu_affinity_mask|**bigint**|Uma máscara de bits que descreve quais processadores lógicos o processo de SQL Server pode usar dentro do grupo de processadores. Por exemplo, cpu_affinity_mask 255 (1111 1111 em binário) significa que os oito primeiros processadores lógicos podem ser usados.|
|cpu_affinity_group|**int**|O número do grupo de processadores usado pelo SQL Server.|
|memory_limit_mb|**bigint**|A quantidade máxima de memória confirmada, em MB, que todos os processos no objeto de trabalho, incluindo SQL Server, podem usar cumulativamente.| 
|process_memory_limit_mb |**bigint**|A quantidade máxima de memória confirmada, em MB, que um único processo no objeto de trabalho, como SQL Server, pode usar.|
|workingset_limit_mb |**bigint**|A quantidade máxima de memória, em MB, que o conjunto de trabalho SQL Server pode usar.|
|non_sos_mem_gap_mb|**bigint**|A quantidade de memória, em MB, reservada para pilhas de thread, DLLs e outras alocações de memória não SOS. A memória de destino SOS é a `process_memory_limit_mb` diferença `non_sos_mem_gap_mb`entre e.| 
|low_mem_signal_threshold_mb|**bigint**|Um limite de memória, em MB. Quando a quantidade de memória disponível para o objeto de trabalho está abaixo desse limite, um sinal de notificação de memória insuficiente é enviado ao processo de SQL Server. |
|total_user_time|**bigint**|O número total de 100 de tiques ns que os threads dentro do objeto de trabalho gastaram no modo de usuário, desde que o objeto de trabalho foi criado. |
|total_kernel_time |**bigint**|O número total de 100 de tiques ns que os threads dentro do objeto de trabalho gastaram no modo kernel, desde que o objeto de trabalho foi criado. |
|write_operation_count |**bigint**|O número total de operações de e/s de gravação em discos locais emitidos por SQL Server desde que o objeto de trabalho foi criado. |
|read_operation_count |**bigint**|O número total de operações de e/s de leitura em discos locais emitidos por SQL Server desde que o objeto de trabalho foi criado. |
|peak_process_memory_used_mb|**bigint**|A quantidade de pico de memória, em MB, que um único processo no objeto de trabalho, como SQL Server, foi usado desde que o objeto de trabalho foi criado.| 
|peak_job_memory_used_mb|**bigint**|A quantidade de pico de memória, em MB, que todos os processos no objeto de trabalho usaram cumulativamente desde que o objeto de trabalho foi criado.|
  
## <a name="permissions"></a>Permissões  
Em Instância Gerenciada do Banco de Dados SQL, requer `VIEW SERVER STATE` permissão. No Banco de Dados SQL, requer a permissão `VIEW DATABASE STATE` no banco de dados.  
 
## <a name="see-also"></a>Consulte Também  

Para obter informações sobre instâncias gerenciadas, consulte [instância gerenciada do banco de dados SQL](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance).
  
