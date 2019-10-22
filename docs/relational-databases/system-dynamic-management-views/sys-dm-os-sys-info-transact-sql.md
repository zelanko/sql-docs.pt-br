---
title: sys. dm _os_sys_info (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 04/24/2018
ms.prod: sql
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_os_sys_info_TSQL
- dm_os_sys_info
- dm_os_sys_info_TSQL
- sys.dm_os_sys_info
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_os_sys_info dynamic management view
- time [SQL Server], instance started
- starting time
ms.assetid: 20f6bc9c-839a-4fa4-b3f3-a6c47d1b69af
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 60859ebb9ebbdeffd45f4d622382b100ba0d8346
ms.sourcegitcommit: d0e5543e8ebf8627eebdfd1e281adb47d6cc2084
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/22/2019
ms.locfileid: "72717244"
---
# <a name="sysdm_os_sys_info-transact-sql"></a>sys. dm _os_sys_info (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-xxxx-asdw-pdw-md.md)]

  Retorna um conjunto variado de informações úteis sobre o computador e sobre os recursos disponíveis e consumidos pelo [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)].  
  
> **Observação:** Para chamá-lo de [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] ou [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], use o nome **Sys. dm _pdw_nodes_os_sys_info**.  
  
|Nome da coluna|Tipo de dados|Descrição e observações específicas da versão |  
|-----------------|---------------|-----------------|  
|**cpu_ticks**|**bigint**|Especifica a contagem de tiques da CPU atual. As marcações de CPU são obtidas do contador RDTSC do processador. É um número que aumenta de forma monotônico. Não permite valor nulo.|  
|**ms_ticks**|**bigint**|Especifica o número de milissegundos desde que o computador foi iniciado. Não permite valor nulo.|  
|**cpu_count**|**inteiro**|Especifica o número de CPUs lógicas no sistema. Não permite valor nulo.|  
|**hyperthread_ratio**|**inteiro**|Especifica a proporção do número de núcleos lógicos ou físicos que são expostos por um pacote de processador físico. Não permite valor nulo.|  
|**physical_memory_in_bytes**|**bigint**|**Aplica-se a:** [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] por meio de [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)].<br /><br /> Especifica a quantidade total de memória física no computador. Não permite valor nulo.|  
|**physical_memory_kb**|**bigint**|**Aplica-se a:** [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] por meio de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> Especifica a quantidade total de memória física no computador. Não permite valor nulo.|  
|**virtual_memory_in_bytes**|**bigint**|**Aplica-se a:** [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] por meio de [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)].<br /><br /> Quantidade de memória virtual disponível para o processo no modo de usuário. Isso pode ser usado para determinar se SQL Server foi iniciado usando uma opção de 3 GB.|  
|**virtual_memory_kb**|**bigint**|**Aplica-se a:** [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] por meio de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> Especifica a quantidade total de espaço de endereço virtual disponível para o processo no modo de usuário. Não permite valor nulo.|  
|**bpool_commited**|**inteiro**|**Aplica-se a:** [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] por meio de [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)].<br /><br /> Representa a memória confirmada em kilobytes (KB) no Gerenciador de memória. Não inclui memória reservada no Gerenciador de memória. Não permite valor nulo.|  
|**committed_kb**|**inteiro**|**Aplica-se a:** [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] por meio de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> Representa a memória confirmada em kilobytes (KB) no Gerenciador de memória. Não inclui memória reservada no Gerenciador de memória. Não permite valor nulo.|  
|**as**|**inteiro**|**Aplica-se a:** [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] por meio de [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)].<br /><br /> Representa a quantidade de memória, em kilobytes (KB), que pode ser consumida por SQL Server Gerenciador de memória.|  
|**committed_target_kb**|**inteiro**|**Aplica-se a:** [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] por meio de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> Representa a quantidade de memória, em kilobytes (KB), que pode ser consumida por SQL Server Gerenciador de memória. O valor de destino é calculado usando uma variedade de entradas como:<br /><br /> -o estado atual do sistema, incluindo sua carga<br /><br /> -a memória solicitada pelos processos atuais<br /><br /> -a quantidade de memória instalada no computador<br /><br /> -parâmetros de configuração<br /><br /> Se **committed_target_kb** for maior que **committed_kb**, o Gerenciador de memória tentará obter memória adicional. Se **committed_target_kb** for menor que **committed_kb**, o Gerenciador de memória tentará reduzir a quantidade de memória confirmada. O **committed_target_kb** sempre inclui memória roubada e reservada. Não permite valor nulo.|  
|**bpool_visible**|**inteiro**|**Aplica-se a:** [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] por meio de [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)].<br /><br /> Número de buffers de 8 KB no pool de buffers que estão diretamente acessíveis no espaço de endereço virtual do processo. Quando não estiver usando extensões AWE, quando o pool de buffers tiver obtido seu destino de memória (bpool_committed = as), o valor de bpool_visible será igual ao valor de bpool_committed. Ao usar o AWE em uma versão de 32 bits do SQL Server, bpool_visible representa o tamanho da janela de mapeamento do AWE usado para acessar a memória física alocada pelo pool de buffers. O tamanho dessa janela de mapeamento é associado ao espaço de endereço do processo e, portanto, o valor visível será menor do que o valor comprometido e poderá ser mais reduzido por componentes internos que consomem a memória para outros fins que não sejam as páginas do banco de dados. Se o valor de bpool_visible for muito baixo, você poderá receber erros de memória insuficiente.|  
|**visible_target_kb**|**inteiro**|**Aplica-se a:** [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] por meio de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> É o mesmo que **committed_target_kb**. Não permite valor nulo.|  
|**stack_size_in_bytes**|**inteiro**|Especifica o tamanho da pilha de chamadas para cada thread criado por [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Não permite valor nulo.|  
|**os_quantum**|**bigint**|Representa o Quantum para uma tarefa não preemptiva, medida em milissegundos. Quantum (em segundos) = **os_quantum** /velocidade do relógio da CPU. Não permite valor nulo.|  
|**os_error_mode**|**inteiro**|Especifica o modo de erro para o processo de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Não permite valor nulo.|  
|**os_priority_class**|**inteiro**|Especifica a classe de prioridade para o processo de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Anula.<br /><br /> 32 = normal (o log de erros dirá [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está começando na base de prioridade normal (= 7).)<br /><br /> 128 = alta (o log de erros dirá [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está sendo executado em uma base de prioridade alta.  (= 13).)<br /><br /> Para obter mais informações, consulte [Configurar a opção de configuração de servidor Priority Boost](../../database-engine/configure-windows/configure-the-priority-boost-server-configuration-option.md).|  
|**max_workers_count**|**inteiro**|Representa o número máximo de trabalhos que podem ser criados. Não permite valor nulo.|  
|**scheduler_count**|**inteiro**|Representa o número de agendadores de usuário configurados no processo de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Não permite valor nulo.|  
|**scheduler_total_count**|**inteiro**|Representa o número total de agendadores em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Não permite valor nulo.|  
|**deadlock_monitor_serial_number**|**inteiro**|Especifica a ID da sequência do monitor de deadlock atual. Não permite valor nulo.|  
|**sqlserver_start_time_ms_ticks**|**bigint**|Representa o número de **ms_tick** quando [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] foi iniciado pela última vez. Compare com a coluna ms_ticks atual. Não permite valor nulo.|  
|**sqlserver_start_time**|**horário**|Especifica a data e a hora [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] última inicialização. Não permite valor nulo.|  
|**affinity_type**|**inteiro**|**Aplica-se a:** [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] por meio de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> Especifica o tipo de afinidade de processo de CPU de servidor em uso no momento. Não permite valor nulo. Para obter mais informações, consulte [ALTER Server &#40;Configuration Transact-&#41;SQL](../../t-sql/statements/alter-server-configuration-transact-sql.md).<br /><br /> 1 = MANUAL<br /><br /> 2 = AUTOMÁTICO|  
|**affinity_type_desc**|**varchar (60)**|**Aplica-se a:** [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] por meio de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> Descreve a coluna **affinity_type** . Não permite valor nulo.<br /><br /> MANUAL = a afinidade foi definida para pelo menos uma CPU.<br /><br /> AUTO = [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pode mover os threads livremente entre CPUs.|  
|**process_kernel_time_ms**|**bigint**|**Aplica-se a:** [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] por meio de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> Tempo total em milissegundos gasto por todos os threads de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no modo kernel. Esse valor pode ser maior que um único relógio de processador, pois inclui o tempo para todos os processadores no servidor. Não permite valor nulo.|  
|**process_user_time_ms**|**bigint**|**Aplica-se a:** [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] por meio de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> Tempo total em milissegundos gasto por todos os threads de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no modo de usuário. Esse valor pode ser maior que um único relógio de processador, pois inclui o tempo para todos os processadores no servidor. Não permite valor nulo.|  
|**time_source**|**inteiro**|**Aplica-se a:** [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] por meio de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> Indica a API que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está usando para recuperar o tempo do relógio de parede. Não permite valor nulo.<br /><br /> 0 = QUERY_PERFORMANCE_COUNTER<br /><br /> 1 = MULTIMEDIA_TIMER|  
|**time_source_desc**|**nvarchar (60)**|**Aplica-se a:** [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] por meio de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> Descreve a coluna **time_source** . Não permite valor nulo.<br /><br /> QUERY_PERFORMANCE_COUNTER = a API [QueryPerformanceCounter](https://go.microsoft.com/fwlink/?LinkId=163095) recupera o tempo do relógio de parede.<br /><br /> MULTIMEDIA_TIMER = a API de [timer de multimídia](https://go.microsoft.com/fwlink/?LinkId=163094) que recupera o tempo do relógio de parede.|  
|**virtual_machine_type**|**inteiro**|**Aplica-se a:** [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] por meio de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> Indica se [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está em execução em um ambiente virtualizado.  Não permite valor nulo.<br /><br /> 0 = NENHUM<br /><br /> 1 = HIPERVISOR<br /><br /> 2 = OUTRO|  
|**virtual_machine_type_desc**|**nvarchar (60)**|**Aplica-se a:** [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] por meio de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> Descreve a coluna **virtual_machine_type** . Não permite valor nulo.<br /><br /> NENHUM = [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não está em execução dentro de uma máquina virtual.<br /><br /> O HIPERVISOR = [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está sendo executado dentro de uma máquina virtual hospedada por um sistema operacional que executa o hipervisor (um sistema operacional de host que emprega virtualização assistida por hardware).<br /><br /> OUTROS = [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está sendo executado dentro de uma máquina virtual hospedada por um sistema operacional que não emprega o assistente de hardware, como o Microsoft Virtual PC.|  
|**softnuma_configuration**|**inteiro**|**Aplica-se a:** [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] por meio de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> Especifica a maneira como os nós NUMA são configurados. Não permite valor nulo.<br /><br /> 0 = OFF indica o padrão de hardware<br /><br /> 1 = soft-NUMA automatizado<br /><br /> 2 = soft-NUMA manual via registro|  
|**softnuma_configuration_desc**|**nvarchar (60)**|**Aplica-se a:** [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] por meio de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> OFF = o recurso soft-NUMA está desativado<br /><br /> ON = [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] determina automaticamente os tamanhos de nó NUMA para soft-NUMA<br /><br /> MANUAL = soft-NUMA configurado manualmente|
|**process_physical_affinity**|**nvarchar (3072)** |**Aplica-se a:** Começando com [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)].<br /><br />Informações que ainda são fornecidas. |
|**sql_memory_model**|**inteiro**|**Aplica-se a:** [!INCLUDE[sssql11](../../includes/sssql11-md.md)] SP4, [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP1 por meio de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br />Especifica o modelo de memória usado pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para alocar memória. Não permite valor nulo.<br /><br />1 = modelo de memória convencional<br />2 = bloquear páginas na memória<br /> 3 = páginas grandes na memória|
|**sql_memory_model_desc**|**nvarchar (120)**|**Aplica-se a:** [!INCLUDE[sssql11](../../includes/sssql11-md.md)] SP4, [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP1 por meio de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br />Especifica o modelo de memória usado pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para alocar memória. Não permite valor nulo.<br /><br />O  =  **convencional** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está usando o modelo de memória convencional para alocar memória. Esse é o modelo de memória SQL padrão quando [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] conta de serviço não tem páginas de bloqueio em privilégios de memória durante a inicialização.<br />**LOCK_PAGES**  =  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está usando páginas de bloqueio na memória para alocar memória. Esse é o Gerenciador de memória do SQL padrão quando SQL Server conta de serviço possui o privilégio bloquear páginas na memória durante a inicialização SQL Server.<br /> **LARGE_PAGES**  =  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está usando páginas grandes na memória para alocar memória. SQL Server usa o alocador de páginas grandes para alocar memória somente com o Enterprise Edition quando SQL Server conta de serviço possui páginas de bloqueio no privilégio de memória durante a inicialização do servidor e quando o sinalizador de rastreamento 834 está ativado.|
|**pdw_node_id**|**inteiro**|**Aplica-se a:** [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)], [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> O identificador do nó em que essa distribuição está.|  
|**socket_count** |**inteiro** | **Aplica-se a:** [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP2 por meio de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br />Especifica o número de soquetes de processador disponíveis no sistema. |  
|**cores_per_socket** |**inteiro** | **Aplica-se a:** [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP2 por meio de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br />Especifica o número de processadores por soquete disponível no sistema. |  
|**numa_node_count** |**inteiro** | **Aplica-se a:** [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP2 por meio de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br />Especifica o número de nós numa disponíveis no sistema. Essa coluna inclui nós numa físicos, bem como nós numa soft. |  
  
## <a name="permissions"></a>Permissões

No [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], requer a permissão `VIEW SERVER STATE`.   
Em [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] camadas Premium, o requer a permissão `VIEW DATABASE STATE` no banco de dados. Em [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] camadas Standard e Basic, o requer o **administrador do servidor** ou uma conta de **administrador do Azure Active Directory** .   

## <a name="see-also"></a>Consulte também  
 [Exibições de gerenciamento dinâmico &#40;e funções do&#41; Transact-SQL](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)    
 [SQL Server exibições &#40;de gerenciamento dinâmico relacionadas ao sistema operacional&#41;](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)  
  
  



