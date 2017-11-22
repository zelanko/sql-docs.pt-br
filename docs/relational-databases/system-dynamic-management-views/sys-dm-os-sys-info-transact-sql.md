---
title: sys.DM os_sys_info (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 04/24/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.service: 
ms.component: dmv's
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.dm_os_sys_info_TSQL
- dm_os_sys_info
- dm_os_sys_info_TSQL
- sys.dm_os_sys_info
dev_langs: TSQL
helpviewer_keywords:
- sys.dm_os_sys_info dynamic management view
- time [SQL Server], instance started
- starting time
ms.assetid: 20f6bc9c-839a-4fa4-b3f3-a6c47d1b69af
caps.latest.revision: "57"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 7cc99a6d0f31d19909d41bde4dcd354d1e045215
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="sysdmossysinfo-transact-sql"></a>sys.dm_os_sys_info (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-xxxx-asdw-pdw-md.md)]

  Retorna um conjunto diverso de informações úteis sobre o computador e sobre os recursos disponíveis e consumidos pelo [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)].  
  
> **Observação:** chamá-la de [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] ou [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], use o nome **sys.dm_pdw_nodes_os_sys_info**.  
  
|Nome da coluna|Tipo de dados|Descrição e notas de versão específica |  
|-----------------|---------------|-----------------|  
|**cpu_ticks**|**bigint**|Especifica a contagem de tiques da CPU. Os tiques da CPU são obtidos do contador RDTSC do processador. É um número que aumenta de forma monotônica. Não permite valor nulo.|  
|**ms_ticks**|**bigint**|Especifica o número de milissegundos desde que o computador foi iniciado. Não permite valor nulo.|  
|**cpu_count**|**int**|Especifica o número de CPUs lógicas no sistema. Não permite valor nulo.|  
|**hyperthread_ratio**|**int**|Especifica a taxa do número de cores lógicas ou físicas que são expostas por um pacote de processador físico. Não permite valor nulo.|  
|**physical_memory_in_bytes**|**bigint**|**Aplica-se a: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] por meio de [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]** .<br /><br /> Especifica a quantidade total de memória física no computador. Não permite valor nulo.|  
|**physical_memory_kb**|**bigint**|**Aplica-se a: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] por meio de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]** .<br /><br /> Especifica a quantidade total de memória física no computador. Não permite valor nulo.|  
|**virtual_memory_in_bytes**|**bigint**|**Aplica-se a: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] por meio de [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]** .<br /><br /> Quantidade de memória virtual disponível ao processo em modo de usuário. Isso pode ser usado para determinar se o SQL Server foi iniciado usando um switch de 3 GB.|  
|**virtual_memory_kb**|**bigint**|**Aplica-se a: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] por meio de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]** .<br /><br /> Especifica a quantidade de espaço de endereço virtual disponível ao processo em modo de usuário. Não permite valor nulo.|  
|**bpool_commited**|**int**|**Aplica-se a: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] por meio de [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]** .<br /><br /> Representa a memória confirmada em KB (quilobytes) no gerenciador de memória. Não inclui a memória reservada no gerenciador de memória. Não permite valor nulo.|  
|**committed_kb**|**int**|**Aplica-se a: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] por meio de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]** .<br /><br /> Representa a memória confirmada em KB (quilobytes) no gerenciador de memória. Não inclui a memória reservada no gerenciador de memória. Não permite valor nulo.|  
|**bpool_commit_target**|**int**|**Aplica-se a: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] por meio de [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]** .<br /><br /> Representa a quantidade de memória, em KB (quilobytes), que pode ser consumida pelo gerenciador de memória do SQL Server.|  
|**committed_target_kb**|**int**|**Aplica-se a: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] por meio de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]** .<br /><br /> Representa a quantidade de memória, em KB (quilobytes), que pode ser consumida pelo gerenciador de memória do SQL Server. A quantidade de destino é calculada por meio de uma variedade de entradas, como:<br /><br /> -o estado atual do sistema, inclusive seu carregamento<br /><br /> -a memória solicitada pelos processos atuais<br /><br /> -a quantidade de memória instalada no computador<br /><br /> -parâmetros de configuração<br /><br /> Se **committed_target_kb** é maior do que **committed_kb**, o Gerenciador de memória tentará obter memória adicional. Se **committed_target_kb** é menor do que **committed_kb**, o Gerenciador de memória tentará reduzir a quantidade de memória confirmada. O **committed_target_kb** sempre inclui memória reservada e roubada. Não permite valor nulo.|  
|**bpool_visible**|**int**|**Aplica-se a: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] por meio de [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]** .<br /><br /> Número de buffers de 8 KB no pool de buffers que é diretamente acessível no espaço do endereço virtual do processo. Ao não usar o AWE (Address Windowing Extensions), quando o pool de buffers tiver obtido seu destino de memória (bpool_committed = bpool_commit_target), o valor de bpool_visible se igualará ao valor de bpool_committed. Ao usar o AWE em uma versão de 32 bits do SQL Server, bpool_visible representará o tamanho da janela de mapeamento do AWE usada para acessar a memória física alocada pelo pool de buffers. O tamanho dessa janela de mapeamento é limitado pelo espaço de endereço do processo e, portanto, a quantidade visível será menor do que a quantidade confirmada, e pode ser ainda mais reduzida por componentes internos que consomem a memória para fins que não sejam as páginas do banco de dados. Se o valor de bpool_visible for baixo demais, você pode receber erros de memória insuficiente.|  
|**visible_target_kb**|**int**|**Aplica-se a: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] por meio de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]** .<br /><br /> É o mesmo que **committed_target_kb**. Não permite valor nulo.|  
|**stack_size_in_bytes**|**int**|Especifica o tamanho da pilha de chamadas para cada thread criado pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Não permite valor nulo.|  
|**os_quantum**|**bigint**|Representa o Quantum para uma tarefa não preemptiva, medido em milissegundos. Quantum (em segundos) = **os_quantum** / velocidade de clock da CPU. Não permite valor nulo.|  
|**os_error_mode**|**int**|Especifica o modo de erro do processo do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Não permite valor nulo.|  
|**os_priority_class**|**int**|Especifica a classe de prioridade do processo do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Anulável.<br /><br /> 32 = normal (o log de erros dirá que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está iniciando na base de prioridade normal (= 7).)<br /><br /> 128 = Alta (o log de erros dirá que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está sendo executado em uma base de prioridade alta.  (=13).)<br /><br /> Para obter mais informações, consulte [Configure the priority boost Server Configuration Option](../../database-engine/configure-windows/configure-the-priority-boost-server-configuration-option.md).|  
|**max_workers_count**|**int**|Representa o número máximo de operadores que podem ser criados. Não permite valor nulo.|  
|**scheduler_count**|**int**|Representa o número de agendadores de usuário configurados no processo do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Não permite valor nulo.|  
|**scheduler_total_count**|**int**|Representa o número total de agendadores no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Não permite valor nulo.|  
|**deadlock_monitor_serial_number**|**int**|Especifica a ID da sequência do monitor de deadlock atual. Não permite valor nulo.|  
|**sqlserver_start_time_ms_ticks**|**bigint**|Representa o **ms_tick** número quando [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] iniciado pela última vez. Compare com a coluna ms_ticks atual. Não permite valor nulo.|  
|**sqlserver_start_time**|**datetime**|Especifica a data e a hora em que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] foi iniciado pela última vez. Não permite valor nulo.|  
|**affinity_type**|**int**|**Aplica-se a: [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]**  por meio de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> Especifica o tipo de afinidade do processo da CPU do servidor em uso atualmente. Não permite valor nulo. Para obter mais informações, consulte [ALTER SERVER CONFIGURATION &#40; Transact-SQL &#41; ](../../t-sql/statements/alter-server-configuration-transact-sql.md).<br /><br /> 1 = MANUAL<br /><br /> 2 = AUTO|  
|**affinity_type_desc**|**varchar(60)**|**Aplica-se a: [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] por meio de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]** .<br /><br /> Descreve o **affinity_type** coluna. Não permite valor nulo.<br /><br /> MANUAL = a afinidade foi definida para pelo menos uma CPU.<br /><br /> AUTO = o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pode mover threads livremente entre CPUs.|  
|**process_kernel_time_ms**|**bigint**|**Aplica-se a: [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] por meio de [! INCLUIR [ssCurrent]**(... /Token/ssCurrent_md.MD)].<br /><br /> Tempo total em milissegundos gasto por todos os threads do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no modo kernel. Esse valor pode ser maior que um único relógio de processador porque inclui o tempo de todos os processadores no servidor. Não permite valor nulo.|  
|**process_user_time_ms**|**bigint**|**Aplica-se a: [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] por meio de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]** .<br /><br /> Tempo total em milissegundos gasto por todos os threads do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no modo de usuário. Esse valor pode ser maior que um único relógio de processador porque inclui o tempo de todos os processadores no servidor. Não permite valor nulo.|  
|**time_source**|**int**|**Aplica-se a: [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] por meio de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]** .<br /><br /> Indica a API que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está usando para recuperar a hora no relógio de parede. Não permite valor nulo.<br /><br /> 0 = QUERY_PERFORMANCE_COUNTER<br /><br /> 1 = MULTIMEDIA_TIMER|  
|**time_source_desc**|**nvarchar (60)**|**Aplica-se a: [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] por meio de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]** .<br /><br /> Descreve o **time_source** coluna. Não permite valor nulo.<br /><br /> QUERY_PERFORMANCE_COUNTER = a [QueryPerformanceCounter](http://go.microsoft.com/fwlink/?LinkId=163095) API recupera a hora do relógio na parede.<br /><br /> MULTIMEDIA_TIMER = a [timer multimídia](http://go.microsoft.com/fwlink/?LinkId=163094) API que recupera a hora do relógio na parede.|  
|**virtual_machine_type**|**int**|**Aplica-se a: [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] por meio de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]** .<br /><br /> Indica se o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está executando em um ambiente virtualizado.  Não permite valor nulo.<br /><br /> 0 = NONE<br /><br /> 1 = HYPERVISOR<br /><br /> 2 = OTHER|  
|**virtual_machine_type_desc**|**nvarchar (60)**|**Aplica-se a: [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] por meio de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]** .<br /><br /> Descreve o **virtual_machine_type** coluna. Não permite valor nulo.<br /><br /> NONE = [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não está em execução em uma máquina virtual.<br /><br /> HYPERVISOR = o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está em execução dentro de um hipervisor, o que implica uma virtualização assistida por hardware. Quando a função Hyper-V é instalada, o hipervisor hospeda o sistema operacional, para que uma instância em execução no sistema operacional host esteja em execução no hipervisor.<br /><br /> OTHER = o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está em execução dentro de uma máquina virtual que não usa assistente de hardware, como o Microsoft Virtual PC.|  
|**softnuma_configuration**|**int**|**Aplica-se a: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] por meio de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]** .<br /><br /> Especifica que os nós NUMA forma são configurados. Não permite valor nulo.<br /><br /> 0 = OFF indica o padrão de hardware<br /><br /> 1 = automatizada soft-NUMA<br /><br /> 2 = soft-NUMA manual por meio do registro|  
|**softnuma_configuration_desc**|**nvarchar (60)**|**Aplica-se a: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] por meio de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]** .<br /><br /> OFF = Soft-NUMA recurso está desativado<br /><br /> = NO SQL Server automaticamente determina os tamanhos de nó para Soft-NUMA<br /><br /> MANUAL = soft-NUMA configurado manualmente|
|**process_physical_affinity**|**nvarchar(3072)** |**Aplica-se a: começando com [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)]** .<br /><br />Informações ainda no futuro. |
|**sql_memory_model**|**int**|**Aplica-se a: [!INCLUDE[sssql11](../../includes/sssql11-md.md)] SP4 e começando com [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP1**.<br /><br />Especifica o modelo de memória usado pelo SQL Server para alocar memória. Não permite valor nulo.<br /><br />1 = o modelo de memória convencional<br />2 = bloquear páginas na memória<br /> 3 = páginas grandes na memória|
|**sql_memory_model_desc**|**nvarchar(120)**|**Aplica-se a: [!INCLUDE[sssql11](../../includes/sssql11-md.md)] SP4 e começando com [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP1**.<br /><br />Especifica o modelo de memória usado pelo SQL Server para alocar memória. Não permite valor nulo.<br /><br />**CONVENCIONAL** = SQL Server está usando o modelo de memória convencional para alocar memória. Isso é o modelo de memória do sql padrão quando a conta de serviço do SQL Server não têm páginas de bloqueio em privilégios de memória durante a inicialização.<br />**LOCK_PAGES** = SQL server usando bloquear páginas na memória para alocar memória. Isso é o Gerenciador de memória do sql padrão quando a conta de serviço do SQL Server possui bloquear páginas na privilégio de memória durante a inicialização do SQL Server.<br /> **LARGE_PAGES** = SQL Server usando páginas grandes na memória para alocar memória. SQL Server usa o alocador de páginas grandes para alocar memória com o Enterprise edition quando a conta de serviço do SQL Server possui bloquear páginas na privilégio de memória durante a inicialização do servidor e 834 do sinalizador de rastreamento está ativado.|
|**pdw_node_id**|**int**|**Aplica-se a: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)],[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]**<br /><br /> O identificador para o nó que essa distribuição é no.|  
|**socket_count** |**int** | **Aplica-se a: começando com [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)]** .<br /><br />Especifica o número de soquetes do processador disponíveis no sistema. |  
|**cores_per_socket** |**int** | **Aplica-se a: começando com [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)].**.<br /><br />Especifica o número de processadores por soquete disponível no sistema. |  
|**numa_node_count** |**int** | **Aplica-se a: começando com [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)].**.<br /><br />Especifica o número de nós de numa disponíveis no sistema. Esta coluna inclui nós numa físicos, bem como nós de numa temporário. |  
  
## <a name="permissions"></a>Permissões  
 Em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] requer `VIEW SERVER STATE` permissão no servidor.  
  
 Em [!INCLUDE[ssSDS](../../includes/sssds-md.md)] as camadas Premium requerem o `VIEW DATABASE STATE` no banco de dados. Em [!INCLUDE[ssSDS](../../includes/sssds-md.md)] camadas Standard e Basic requer o [!INCLUDE[ssSDS](../../includes/sssds-md.md)] conta de administrador.  
  
## <a name="see-also"></a>Consulte também  
 [Exibições e funções de gerenciamento dinâmico &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Sistema operacional SQL Server relacionadas exibições de gerenciamento dinâmico &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)  
  
  



