---
title: DM os_schedulers (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/13/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_os_schedulers
- sys.dm_os_schedulers_TSQL
- sys.dm_os_schedulers
- dm_os_schedulers_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_os_schedulers dynamic management view
ms.assetid: 3a09d81b-55d5-416f-9cda-1a3a5492abe0
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 6f167aa6f4572fc1a44db83cfb9f7ea7b7a092b9
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67899839"
---
# <a name="sysdmosschedulers-transact-sql"></a>sys.dm_os_schedulers (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Retorna uma linha por agendador no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], onde cada agendador é mapeado para um processador individual. Use esta exibição para monitorar a condição de um agendador ou para identificar tarefas sem controle.  
  
> [!NOTE]  
>  Chamá-lo partir [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] ou [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], use o nome **sys.dm_pdw_nodes_os_schedulers**.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|scheduler_address|**varbinary(8)**|Endereço de memória do agendador. Não permite valor nulo.|  
|parent_node_id|**int**|ID do nó ao qual o agendador pertence, também conhecido como nó pai. Isso representa um nó NUMA (acesso não uniforme à memória). Não permite valor nulo.|  
|scheduler_id|**int**|ID do agendador. Todos os agendadores que são usados para executar consultas normais têm números de ID menores que 1048576. Os agendadores que tiverem IDs maiores ou iguais a 1048576 serão usados internamente pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], como o agendador da conexão de administrador dedicada. Não permite valor nulo.|  
|cpu_id|**smallint**|A ID da CPU atribuída ao agendador.<br /><br /> Não permite valor nulo.<br /><br /> **Observação:** 255 não indica nenhuma afinidade como fazia no [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]. Ver [DM os_threads &#40;Transact-SQL&#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-os-threads-transact-sql.md) para obter informações de afinidade adicionais.|  
|status|**nvarchar(60)**|Indica o status do agendador. Pode ser um dos seguintes valores:<br /><br /> -OCULTO ONLINE<br />-OCULTO OFFLINE<br />-VISÍVEIS ONLINE<br />-VISÍVEL OFFLINE<br />-ON-LINE VISÍVEL (DAC)<br />-HOT_ADDED<br /><br /> Não permite valor nulo.<br /><br /> Os agendadores HIDDEN são usados para processar solicitações internas do [!INCLUDE[ssDE](../../includes/ssde-md.md)]. Os agendadores VISIBLE são usados para processar solicitações de usuários.<br /><br /> Os agendadores OFFLINE são mapeados para processadores que estão offline na máscara de afinidade e, portanto, não estão sendo usados para processar solicitações. Os agendadores ONLINE são mapeados para processadores que estão online na máscara de afinidade e estão disponíveis para processar threads.<br /><br /> DAC indica que o agendador está sendo executado em uma conexão de administrador dedicada.<br /><br /> HOT ADDED indica que os agendadores foram adicionados em resposta a um evento de CPU de adição a quente.|  
|is_online|**bit**|Se o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] estiver configurado para usar somente alguns dos processadores disponíveis no servidor, essa configuração pode indicar que alguns agendadores estão mapeados para processadores que não estão na máscara de afinidade. Se esse for o caso, essa coluna retornará 0. Esse valor indica que o agendador não está sendo usado para processar consultas ou lotes.<br /><br /> Não permite valor nulo.|  
|is_idle|**bit**|1 = O agendador está ocioso. Nenhum operador está em execução no momento. Não permite valor nulo.|  
|preemptive_switches_count|**int**|Número de vezes que os operadores deste agendador alternaram para o modo preemptivo.<br /><br /> Para executar código fora do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (por exemplo, procedimentos armazenados estendidos e consultas distribuídas), um thread deve ser executado fora do controle de um agendador não preventivo. Para fazer isso, um trabalhador muda para o modo preventivo.|  
|context_switches_count|**int**|Número de alternâncias de contexto ocorridas neste agendador. Não permite valor nulo.<br /><br /> Para permitir que outros trabalhadores sejam executados, o trabalhador em execução no momento precisa abrir mão do controle do agendador ou alternar o contexto.<br /><br /> **Observação:** Se um trabalhador produzir o Agendador e coloca-se na fila executável e, em seguida, não encontra outros operadores, ele selecionará em si. Neste caso, a context_switches_count não será atualizada, mas a yield_count será.|  
|idle_switches_count|**int**|Número de horas que o agendador espera por um evento enquanto está ocioso. Esta coluna é semelhante à context_switches_count. Não permite valor nulo.|  
|current_tasks_count|**int**|Número de tarefas associadas a este agendador no momento. Esta contagem inclui o seguinte:<br /><br /> -Tarefas que estão aguardando um trabalho para executá-los.<br />-Tarefas que estão aguardando ou em execução (no estado SUSPENDED ou RUNNABLE).<br /><br /> Quando uma tarefa é concluída, esta contagem é reduzida. Não permite valor nulo.|  
|runnable_tasks_count|**int**|Número de operadores, com tarefas atribuídas a eles, que esperam para serem agendados na fila executável. Não permite valor nulo.|  
|current_workers_count|**int**|Número de operadores associados a este agendador. Essa contagem inclui operadores que não estão atribuídos a nenhuma tarefa. Não permite valor nulo.|  
|active_workers_count|**int**|Número de operadores ativos. Um operador ativo nunca é preemptivo, deve ter uma tarefa associada e estar em execução, ser executável ou estar suspenso. Não permite valor nulo.|  
|work_queue_count|**bigint**|Número de tarefas na fila pendente. Essas tarefas estão aguardando serem selecionadas por um operador. Não permite valor nulo.|  
|pending_disk_io_count|**int**|Número de E/Ss pendentes que aguardam para serem concluídas. Cada agendador possui uma lista de E/Ss pendentes que são verificadas para determinar se foram concluídas sempre que há uma alternância de contexto. A contagem aumenta quando a solicitação é inserida. Essa contagem diminui quando a solicitação é concluída. O número não indica o estado das E/Ss. Não permite valor nulo.|  
|load_factor|**int**|Valor interno que indica a carga percebida neste agendador. Esse valor é usado para determinar se uma nova tarefa deve ser colocada neste ou em outro agendador. O valor é útil para fins de depuração, quando parece que os agendadores não são carregados de maneira uniforme. A decisão de roteamento é tomada com base na carga do agendador. O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] também usa um fator de carga de nós e agendadores para ajudar a determinar o melhor local para a aquisição de recursos. Quando uma tarefa é enfileirada, o fator de carga aumenta. Quando uma tarefa é concluída, o fator de carga diminui. O uso do fator de carga ajuda o SO do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a equilibrar melhor a carga de trabalho. Não permite valor nulo.|  
|yield_count|**int**|Valor interno que é usado para indicar o progresso neste agendador. Esse valor é usado pelo Scheduler Monitor para determinar se um trabalhador no agendador não está cedendo a outros trabalhadores no momento. O valor não indica que houve transição do operador ou tarefa para um novo operador. Não permite valor nulo.|  
|last_timer_activity|**bigint**|Em tiques de CPU, a última vez que a fila do temporizador do agendador foi verificada pelo agendador. Não permite valor nulo.|  
|failed_to_create_worker|**bit**|Definido como 1 se não foi possível criar um novo operador neste agendador. Isso geralmente ocorre devido a restrições de memória. Permite valor nulo.|  
|active_worker_address|**varbinary(8)**|Endereço de memória do operador que está ativo no momento. Permite valor nulo. Para obter mais informações, consulte [DM os_workers &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-workers-transact-sql.md).|  
|memory_object_address|**varbinary(8)**|Endereço de memória do objeto de memória do agendador. Não é NULLABLE.|  
|task_memory_object_address|**varbinary(8)**|Endereço de memória do objeto de memória da tarefa. Não permite valor nulo. Para obter mais informações, consulte [DM os_memory_objects &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-memory-objects-transact-sql.md).|  
|quantum_length_us|**bigint**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)] Expõe o quantum do agendador usado por SQLOS.|  
| total_cpu_usage_ms |**bigint**|**Aplica-se a**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] e posterior <br><br> Total de CPU consumido por este agendador conforme relatado por trabalhadores não preemptivo. Não permite valor nulo.|
|total_cpu_idle_capped_ms|**bigint**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)] Indica a limitação com base em [objetivo de nível de serviço](/azure/sql-data-warehouse/what-is-a-data-warehouse-unit-dwu-cdwu#service-level-objective), sempre será 0 para não Azure versões do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Permite valor nulo.|
|total_scheduler_delay_ms|**bigint**|**Aplica-se a**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] e posterior <br><br> O tempo entre um trabalho de extração e outra alternância. Pode ser causado por trabalhadores preemptive atrasando o agendamento do trabalho não preemptiva próximo ou devido ao sistema operacional agendar os threads de outros processos. Não permite valor nulo.|
|ideal_workers_limit|**int**|**Aplica-se a**: [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] e posterior <br><br> Quantos trabalhadores devem ser o ideal é que o Agendador. Se as funções de trabalho atuais excederem o limite devido à carga de tarefa desequilibrado, depois que se tornam ociosos, eles serão cortados. Não permite valor nulo.|
|pdw_node_id|**int**|**Aplica-se ao**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)], [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> O identificador para o nó que essa distribuição é no.|  
  
## <a name="permissions"></a>Permissões

Na [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], requer `VIEW SERVER STATE` permissão.   
Em [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)], requer a permissão `VIEW DATABASE STATE` no banco de dados.   

## <a name="examples"></a>Exemplos  
  
### <a name="a-monitoring-hidden-and-nonhidden-schedulers"></a>A. Monitorando agendadores ocultos e não ocultos  
 A consulta a seguir retorna o estado de trabalhadores e tarefas no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em todos os agendadores. Essa consulta foi executada em um sistema de computador que tem o seguinte:  
  
-   Dois processadores (CPUs)  
  
-   Dois nós (NUMA)  
  
-   Uma CPU por nó NUMA  
  
-   Máscara de afinidade definida como `0x03`.  
  
```  
SELECT  
    scheduler_id,  
    cpu_id,  
    parent_node_id,  
    current_tasks_count,  
    runnable_tasks_count,  
    current_workers_count,  
    active_workers_count,  
    work_queue_count  
  FROM sys.dm_os_schedulers;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
scheduler_id cpu_id parent_node_id current_tasks_count  
------------ ------ -------------- -------------------  
0            1      0              9                    
257          255    0              1                    
1            0      1              10                   
258          255    1              1                    
255          255    32             2                    
  
runnable_tasks_count current_workers_count  
-------------------- ---------------------  
0                    11                     
0                    1                      
0                    18                     
0                    1                      
0                    3                      
  
active_workers_count work_queue_count  
-------------------- --------------------  
6                    0  
1                    0  
8                    0  
1                    0  
1                    0  
```  
  
 A saída fornece as seguintes informações:  
  
-   Há cinco agendamentos. Dois agendadores têm uma ID < 1048576 de valor. Agendadores com ID > = 1048576 são conhecidos como agendadores ocultos. O agendador `255` representa a conexão de administrador dedicada (DAC). Há um agendador DAC para cada instância. Monitores de recursos que coordenam a pressão de memória utilizam o agendador `257` e o agendador `258`, um para cada nó NUMA  
  
-   Há 23 tarefas ativas na saída. Essas tarefas incluem solicitações de usuários, bem como tarefas de gerenciamento de recursos que foram iniciadas pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Exemplos de tarefas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] são: RESOURCE MONITOR (uma para cada nó NUMA), LAZY WRITER (uma para cada nó NUMA), LOCK MONITOR, CHECKPOINT e LOG WRITER.  
  
-   `0` de nó NUMA é mapeado para CPU `1` e nó NUMA `1` é mapeado para `0`de CPU. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] inicia normalmente em um nó NUMA diferente de nó 0.  
  
-   Com `runnable_tasks_count` retornando `0`, não há nenhuma tarefa ativamente em execução. Entretanto, pode haver sessões ativas.  
  
-   O agendador `255` representando DAC possui `3` trabalhadores associados. Esses trabalhadores são alocados na inicialização do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e não são alterados. Esses trabalhadores são usados para processar somente consultas DAC. As duas tarefas neste agendador representam um gerenciador de conexões e um trabalhador inativo.  
  
-   `active_workers_count` representa todos os trabalhos que possuem tarefas associadas e são executados no modo não preemptivo. Algumas tarefas, como escutas de rede, são executadas sob planejamento preemptivo.  
  
-   Agendadores ocultos não processam solicitações comuns de usuário. O agendador DAC é a exceção. Ele possui um thread para processar solicitações.  
  
### <a name="b-monitoring-nonhidden-schedulers-in-a-busy-system"></a>B. Monitorando agendadores não ocultos em um sistema ocupado  
 A consulta a seguir mostra o estado de agendadores não ocultos intensamente carregados, onde há mais solicitações do que os trabalhadores disponíveis podem manipular. Neste exemplo, 256 trabalhadores recebem tarefas. Algumas tarefas estão aguardando a atribuição a um trabalhador. A contagem de executáveis mais baixa indica que várias tarefas aguardam um recurso.  
  
> [!NOTE]  
>  Você pode descobrir o estado de trabalhadores consultando sys.dm_os_workers. Para obter mais informações, consulte [DM os_workers &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-workers-transact-sql.md).  
  
 Esta é a consulta:  
  
```  
SELECT  
    scheduler_id,  
    cpu_id,  
    current_tasks_count,  
    runnable_tasks_count,  
    current_workers_count,  
    active_workers_count,  
    work_queue_count  
  FROM sys.dm_os_schedulers  
  WHERE scheduler_id < 255;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
scheduler_id current_tasks_count runnable_tasks_count  
------------ ------------------- --------------------  
0            144                 0                     
1            147                 1                     
  
current_workers_count active_workers_count work_queue_count  
--------------------- -------------------- --------------------  
128                   125                  16  
128                   126                  19  
```  
  
 Por comparação, o resultado a seguir mostra várias tarefas executáveis onde nenhuma delas está esperando para obter um trabalhador. `work_queue_count` é `0` para ambos os agendadores.  
  
```  
scheduler_id current_tasks_count runnable_tasks_count  
------------ ------------------- --------------------  
0            107                 98                    
1            110                 100                   
  
current_workers_count active_workers_count work_queue_count  
--------------------- -------------------- --------------------  
128                   104                  0  
128                   108                  0  
```  
  
## <a name="see-also"></a>Consulte também  
 [Sistema operacional SQL Server relacionados exibições de gerenciamento dinâmico &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)  
  
  


