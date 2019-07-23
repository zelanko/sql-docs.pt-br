---
title: Guia de arquitetura de gerenciamento de memória | Microsoft Docs
ms.custom: ''
ms.date: 01/09/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- guide, memory management architecture
- memory management architecture guide
ms.assetid: 7b0d0988-a3d8-4c25-a276-c1bdba80d6d5
author: rothja
ms.author: jroth
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 4e33a8add08837fb71c0d0558d6bbe7f3ae9197c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68115273"
---
# <a name="memory-management-architecture-guide"></a>guia de arquitetura de gerenciamento de memória

[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

## <a name="windows-virtual-memory-manager"></a>Gerenciador de Memória Virtual do Windows  
As regiões confirmadas de espaço de endereço são mapeadas para a memória física disponível pelo VMM (Gerenciador de Memória Virtual) do Windows.  
  
Para obter mais informações sobre a quantidade de memória física compatível com sistemas operacionais diferentes, consulte a documentação do Windows sobre os [Limites de memória para versões do Windows](/windows/desktop/Memory/memory-limits-for-windows-releases).  
  
Os sistemas de memória virtual permitem exceder o uso da memória física, de modo que a taxa entre memória física e virtual pode exceder 1:1. Como resultado, programas maiores podem ser executados em computadores com várias configurações de memória física. No entanto, usar significativamente mais memória virtual do que a média combinada de conjuntos de trabalho de todos os processos pode provocar desempenho inadequado. 

## <a name="sql-server-memory-architecture"></a>Arquitetura de memória do SQL Server

O[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] adquire e libera memória dinamicamente conforme necessário. Normalmente, um administrador não precisa especificar a quantidade de memória que deve ser alocada ao [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], embora essa opção exista e seja necessária em alguns ambientes.

Uma das principais metas de design de todo o software de banco de dados é minimizar a E/S de disco devido às leituras e gravações de disco estarem entre as operações que consomem muitos recursos. O[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] cria um pool de buffers na memória para manter a leitura de páginas do banco de dados. Grande parte do código do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] é dedicada a minimizar o número de leituras e gravações físicas entre o disco e o pool de buffers. O[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] tenta alcançar um equilíbrio entre as duas metas:

* Evitar que o pool de buffers fique tão grande que o sistema inteiro fique com pouca memória.
* Minimizar a E/S física aos arquivos de banco de dados maximizando o tamanho do pool de buffers.

> [!NOTE]
> Em um sistema amplamente carregado, algumas consultas grandes que exigem muita memória para serem executadas não conseguem obter a quantidade mínima de memória solicitada e recebem um erro de tempo limite enquanto esperam recursos de memória. Para resolver isso, aumente a [Opção query wait](../database-engine/configure-windows/configure-the-query-wait-server-configuration-option.md). Para uma consulta paralela, considere a redução da [Opção de grau máximo de paralelismo](../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md).
 
> [!NOTE]
> Em um sistema amplamente carregado sob pressão de memória, as consultas com junção de mesclagem, classificação e bitmap no plano de consulta podem cancelar o bitmap quando as consultas não adquirem a memória mínima necessária para o bitmap. Isso pode afetar o desempenho da consulta e, se o processo de classificação não conseguir se ajustar na memória, poderá aumentar o uso de tabelas de trabalho no banco de dados tempdb, aumentando o tempdb. Para resolver esse problema, adicione memória física ou ajuste as consultas para usar um plano de consulta diferente e mais rápido.
 
### <a name="providing-the-maximum-amount-of-memory-to-includessnoversionincludesssnoversion-mdmd"></a>Fornecendo a quantidade máxima de memória ao [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]

Ao usar o AWE e o privilégio Páginas Bloqueadas na Memória, você pode fornecer as quantidades de memória a seguir para o Mecanismo de Banco de Dados do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] . 

> [!NOTE]
> A tabela a seguir inclui uma coluna para as versões de 32 bits, que não estão mais disponíveis.

| |32 bits <sup>1</sup> |64 bits|
|-------|-------|-------| 
|Memória convencional |Todas as edições do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] . Até o limite de espaço de endereço virtual do processo: <br>- 2 GB<br>- 3 GB com parâmetro de inicialização de /3gb <sup>2</sup> <br>- 4 GB no WOW64 <sup>3</sup> |Todas as edições do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] . Até o limite de espaço de endereço virtual do processo: <br>- 7 TB com arquitetura IA64 (IA64 não tem suporte no [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] e posterior)<br>- Máximo do sistema operacional com a arquitetura x64 <sup>4</sup>
|Mecanismo AWE (Permite ao [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] ir além do limite de espaço de endereço virtual do processo na plataforma de 32 bits.) |[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Edições Standard, Enterprise e Developer: o pool de buffers é capaz de acessar até 64 GB de memória.|Não aplicável <sup>5</sup> |
|Privilégio do SO (sistema operacional) de bloquear páginas na memória (permite o bloqueio de memória física, evitando a paginação do SO da memória bloqueada). <sup>6</sup> |[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Edições Standard, Enterprise e Developer: necessárias para o processo do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] usar o mecanismo AWE. A memória alocada pelo mecanismo AWE não pode passar pelo page out. <br> A concessão desse privilégio sem a ativação de AWE não tem nenhum efeito no servidor. | Utilizada somente quando necessário, ou seja, se houver sinais de que o processo sqlservr está sendo paginado. Neste caso, o erro 17890 será reportado no log de erros, que se assemelha ao exemplo a seguir:`A significant part of sql server process memory has been paged out. This may result in a performance degradation. Duration: #### seconds. Working set (KB): ####, committed (KB): ####, memory utilization: ##%.`|

<sup>1</sup> Versões de 32 bits não estão disponíveis a partir do [!INCLUDE[ssSQL14](../includes/sssql14-md.md)].  
<sup>2</sup> /3gb é um parâmetro de inicialização do sistema operacional. Para saber mais, visite a Biblioteca MSDN.  
<sup>3</sup> WOW64 (Windows on Windows 64) é um modo em que o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] de 32 bits é executado em um sistema operacional de 64 bits.  
<sup>4</sup> [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Standard Edition oferece suporte a até 128 GB. O [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Enterprise Edition é compatível com o limite máximo do sistema operacional.  
<sup>5</sup> Observe que a opção sp_configure awe enabled estava presente no [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]de 64 bits, mas é ignorada.    
<sup>6</sup> Se as páginas bloqueadas no privilégio de memória (LPIM) forem concedidas (em 32 bits para suporte AWE ou em 64 bits por si só), também é recomendável a definição da memória máxima do servidor. Para obter mais informações sobre o LPIM, consulte [Opções Server Memory de configuração do servidor](../database-engine/configure-windows/server-memory-server-configuration-options.md#lock-pages-in-memory-lpim)

> [!NOTE]
> Versões anteriores do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] podiam ser executadas em um sistema operacional de 32 bits. O acesso a mais de 4 GB (gigabytes) de memória em um sistema operacional de 32 bits exigiu que o recurso AWE (Address Windowing Extensions) gerenciasse a memória. Isso não é necessário quando o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] está em execução em sistemas operacionais de 64 bits. Para saber mais sobre o AWE, consulte [Espaço de endereço de processo](https://msdn.microsoft.com/library/ms189334.aspx) e [Gerenciando memória para bancos de dados grandes](https://msdn.microsoft.com/library/ms191481.aspx) na documentação do [!INCLUDE[ssKatmai](../includes/ssKatmai-md.md)].   

<a name="changes-to-memory-management-starting-2012-11x-gm"></a>

## <a name="changes-to-memory-management-starting-with-includesssql11includessssql11-mdmd"></a>Alterações no gerenciamento de memória a partir do [!INCLUDE[ssSQL11](../includes/sssql11-md.md)]

Nas versões anteriores do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] ([!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)], [!INCLUDE[ssKatmai](../includes/ssKatmai-md.md)] e [!INCLUDE[ssKilimanjaro](../includes/ssKilimanjaro-md.md)]), a alocação de memória era feita usando cinco mecanismos diferentes:
-  O **SPA (alocador de página única)** , incluindo somente as alocações de memória que eram menores ou iguais a 8 KB no processo do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. As opções de configuração *max server memory (MB)* e *min server memory (MB)* determinavam os limites de memória física que o SPA consumia. O pool de buffers era simultaneamente o mecanismo do SPA e o maior consumidor de alocações de uma página.
-  O **Alocador de várias páginas (MPA)** , para as alocações de memória que solicitam mais de 8 KB.
-  O **Alocador de CLR**, incluindo os heaps SQL CLR e suas alocações globais que são criadas durante a inicialização do CLR.
-  As alocações de memória para as **[pilhas de thread](../relational-databases/memory-management-architecture-guide.md#stacksizes)** no processo do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].
-  As **DWA (Alocações Diretas do Windows)** , para as solicitações de alocação de memória feitas diretamente no Windows. Elas incluem o uso de heap do Windows e as alocações virtuais diretas feitas pelos módulos que são carregados no processo do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Exemplos de tais solicitações de alocação de memória incluem as alocações de DLLs de procedimento armazenado estendido, os objetos que são criados usando procedimentos de automação (chamadas sp_OA) e as alocações de provedores de servidor vinculados.

A partir do [!INCLUDE[ssSQL11](../includes/sssql11-md.md)], as alocações de uma página, as alocações de várias páginas e as alocações de CLR são consolidadas em um **alocador de páginas de "qualquer tamanho"** que é incluído nos limites de memória controlados pelas opções de configuração *max server memory (MB)* e *min server memory (MB)* . Essa alteração forneceu uma capacidade de dimensionamento mais precisa para todos os requisitos de memória que passam pelo gerenciador de memória do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. 

> [!IMPORTANT]
> Examine com atenção suas configurações *max server memory (MB)* e *min server memory (MB)* atuais depois de fazer upgrade para o [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] por meio do [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]. Isso é necessário porque, a partir do [!INCLUDE[ssSQL11](../includes/sssql11-md.md)], tais configurações agora incluem e consideram mais alocações de memória em comparação com as versões anteriores. Essas alterações se aplicam às versões de 32 e 64 bits do [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] e do [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] e às versões de 64 bits do [!INCLUDE[ssSQL15](../includes/sssql15-md.md)] por meio do [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)].

A tabela a seguir indica se um tipo específico de alocação de memória é controlado pelas opções de configuração *max server memory (MB)* e *min server memory (MB)* :

|Tipo de alocação de memória| [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)], [!INCLUDE[ssKatmai](../includes/ssKatmai-md.md)] e [!INCLUDE[ssKilimanjaro](../includes/ssKilimanjaro-md.md)]| A partir do [!INCLUDE[ssSQL11](../includes/sssql11-md.md)]|
|-------|-------|-------|
|Alocações de uma página|Sim|Sim, consolidadas em alocações de página de “qualquer tamanho”|
|Alocações de várias páginas|Não|Sim, consolidadas em alocações de página de “qualquer tamanho”|
|Alocações de CLR|Não|Sim|
|Memória de pilhas de thread|Não|Não|
|Alocações diretas do Windows|Não|Não|

A partir do [!INCLUDE[ssSQL11](../includes/sssql11-md.md)], o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] pode alocar mais memória do que o valor especificado na configuração max server memory. Esse comportamento pode ocorrer quando o valor de **_Memória Total do Servidor (KB)_** já tiver atingido a configuração da **_Memória do Servidor de Destino (KB)_** (conforme especificado pela memória máxima do servidor). Se houver memória contígua livre insuficiente para atender à demanda de solicitações de memória de várias páginas (mais de 8 KB) devido à fragmentação da memória, o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] poderá exceder o uso em vez de rejeitar a solicitação de memória. 

Assim que essa alocação for executada, a tarefa em segundo plano *Monitor de Recursos* começará a indicar para todos os consumidores de memória liberarem a memória alocada e tentará colocar o valor de *Memória Total do Servidor (KB)* abaixo da especificação da *Memória do Servidor de Destino (KB)* . Portanto, o uso de memória do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] pode rapidamente exceder a configuração max server memory. Nessa situação, o leitor do contador de desempenho da *Memória Total do Servidor (KB)* excederá as configurações max server memory e *Memória do Servidor de Destino (KB)* .

Esse comportamento geralmente é observado durante as operações a seguir: 
-  Consultas grandes do índice columnstore.
-  Recompilações do índice columnstore, que usam grandes volumes de memória para executar operações de hash e de classificação.
-  Operações de backup que exigem buffers de memória grandes.
-  Rastreamento de operações que precisam armazenar grandes parâmetros de entrada.

<a name="#changes-to-memory-management-starting-with-includesssql11includessssql11-mdmd"></a>
## <a name="changes-to-memorytoreserve-starting-with-includesssql11includessssql11-mdmd"></a>Alterações em “memory_to_reserve” a partir do [!INCLUDE[ssSQL11](../includes/sssql11-md.md)]
Nas versões anteriores do SQL Server ([!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)], [!INCLUDE[ssKatmai](../includes/ssKatmai-md.md)] e [!INCLUDE[ssKilimanjaro](../includes/ssKilimanjaro-md.md)]), o gerenciador de memória do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] deixava de lado uma parte do VAS (espaço de endereço virtual) do processo usado pelo **MPA (Alocador de Várias Páginas)** , pelo **Alocador de CLR**, pelas alocações de memória das **pilhas de threads** no processo do SQL Server e pelas **DWA (Alocações Diretas do Windows)** . Esta parte do espaço de endereço virtual também é conhecida como região “Mem-To-Leave” ou como “Pool de buffers sem memória”.

O espaço de endereço virtual reservado para essas alocações é determinado pela opção de configuração _**memory\_to\_reserve**_ . O valor padrão que o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] usa é 256 MB. Para substituir o valor padrão, use o parâmetro de inicialização [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] *-g*. Consulte a página de documentação em [Opções de inicialização do serviço Mecanismo de Banco de Dados](../database-engine/configure-windows/database-engine-service-startup-options.md) para obter informações sobre o parâmetro de inicialização *-g*.

Uma vez que o novo alocador de páginas de “qualquer tamanho” também controla as alocações maiores que 8 KB a partir do [!INCLUDE[ssSQL11](../includes/sssql11-md.md)], o valor de *memory_to_reserve* não inclui as alocações de várias páginas. Exceto por essa alteração, tudo permanece igual com esta opção de configuração.

A tabela a seguir indica se um tipo específico de alocação de memória se encaixa na região *memory_to_reserve* do espaço de endereço virtual para o processo do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]:

|Tipo de alocação de memória| [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)], [!INCLUDE[ssKatmai](../includes/ssKatmai-md.md)] e [!INCLUDE[ssKilimanjaro](../includes/ssKilimanjaro-md.md)]| A partir do [!INCLUDE[ssSQL11](../includes/sssql11-md.md)]|
|-------|-------|-------|
|Alocações de uma página|Não|Não, consolidados em alocações de páginas de “qualquer tamanho”|
|Alocações de várias páginas|Sim|Não, consolidados em alocações de páginas de “qualquer tamanho”|
|Alocações de CLR|Sim|Sim|
|Memória de pilhas de thread|Sim|Sim|
|Alocações diretas do Windows|Sim|Sim|

## <a name="dynamic-memory-management"></a> Gerenciamento de Memória Dinâmica
O comportamento de gerenciamento de memória padrão do [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] é adquirir a quantidade de memória necessária sem provocar escassez de memória no sistema. O [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] faz isto usando as APIs de notificação de memória no Microsoft Windows.

Quando o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] está usando memória dinamicamente, ele consulta o sistema periodicamente para determinar a quantidade de memória livre. Manter essa memória livre impede a paginação do SO (sistema operacional). Se menos memória estiver livre, o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] liberará memória para o SO. Se houver mais memória livre, o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] poderá alocar mais memória. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] adiciona memória apenas quando sua carga de trabalho exige mais. Um servidor em repouso não aumenta o tamanho de seu espaço de endereço virtual.  
  
A opção **[max server memory](../database-engine/configure-windows/server-memory-server-configuration-options.md)** controla a alocação de memória do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], a memória de compilação, todos os caches (incluindo o pool de buffers), as [concessões de memória de execução de consulta](#effects-of-min-memory-per-query), a [memória de gerenciador de bloqueio](#memory-used-by-sql-server-objects-specifications) e a memória do CLR<sup>1</sup> (basicamente qualquer administrador de memória encontrado em **[sys.dm_os_memory_clerks](../relational-databases/system-dynamic-management-views/sys-dm-os-memory-clerks-transact-sql.md)** ). 

<sup>1</sup> A memória do CLR é gerenciada em alocações de max_server_memory a partir do [!INCLUDE[ssSQL11](../includes/sssql11-md.md)].

A instrução a seguir retorna informações sobre a memória alocada atualmente:  
  
```sql  
SELECT 
  physical_memory_in_use_kb/1024 AS sql_physical_memory_in_use_MB, 
    large_page_allocations_kb/1024 AS sql_large_page_allocations_MB, 
    locked_page_allocations_kb/1024 AS sql_locked_page_allocations_MB,
    virtual_address_space_reserved_kb/1024 AS sql_VAS_reserved_MB, 
    virtual_address_space_committed_kb/1024 AS sql_VAS_committed_MB, 
    virtual_address_space_available_kb/1024 AS sql_VAS_available_MB,
    page_fault_count AS sql_page_fault_count,
    memory_utilization_percentage AS sql_memory_utilization_percentage, 
    process_physical_memory_low AS sql_process_physical_memory_low, 
    process_virtual_memory_low AS sql_process_virtual_memory_low
FROM sys.dm_os_process_memory;  
```  
 
<a name="stacksizes"></a> A memória para as pilhas de thread<sup>1</sup>, o CLR<sup>2</sup>, os arquivos .dll de procedimento estendido, os provedores OLE DB referenciados por consultas distribuídas, os objetos de automação referenciados nas instruções do [!INCLUDE[tsql](../includes/tsql-md.md)] e qualquer memória alocada por um [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] não DLL **não** são controlados pela opção max server memory.

<sup>1</sup> Consulte a página da documentação sobre como [Configurar a opção max worker threads de configuração de servidor](../database-engine/configure-windows/configure-the-max-worker-threads-server-configuration-option.md) para obter informações sobre os threads de trabalho padrão calculados para um determinado número de CPUs de afinidade no host atual. Estes são os tamanhos de pilha do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]:

|Arquitetura do SQL Server|Arquitetura do SO|Tamanho da pilha|  
|--------------------|----------------------|----------------------|
|x86 (32 bits)|x86 (32 bits)|512 KB|
|x86 (32 bits)|x64 (64 bits)|768 KB| 
|x64 (64 bits)|x64 (64 bits)|2048 KB|
|IA64 (Itanium)|IA64 (Itanium)|4096 KB|

<sup>2</sup> A memória do CLR é gerenciada em alocações de max_server_memory a partir do [!INCLUDE[ssSQL11](../includes/sssql11-md.md)].

O [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] usa a API de notificação de memória **QueryMemoryResourceNotification** para determinar quando o Gerenciador de Memória do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] pode alocar e liberar memória.  

Quando o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] é iniciado, ele computa o tamanho do espaço de endereço virtual do pool de buffers baseado em vários parâmetros, como quantidade de memória física no sistema, número de threads de servidor e vários parâmetros de inicialização. O[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] reserva a quantidade computada do seu espaço de endereço virtual de processo do pool de buffers, mas adquire (confirma) somente a quantidade exigida da memória física para a carga atual.

A instância continua adquirindo memória conforme necessário para atender a carga de trabalho. Como mais usuários conectam e executam consultas, o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] adquire a memória física adicional por demanda. Uma instância do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] continua adquirindo memória física até alcançar o destino de alocação max server memory ou o SO indicar que não há mais um excesso de memória livre; ela libera memória quando tem mais do que a configuração min server memory e o SO indica que há uma escassez de memória livre. 

Conforme são iniciados outros aplicativos em um computador que está executando uma instância do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], eles consomem memória e a quantidade de memória física livre reduz o destino do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] . A instância do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] ajusta seu consumo de memória. Se outro aplicativo for interrompido e, com isso, houver mais memória disponível, a instância do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] aumentará o tamanho de sua alocação de memória. O[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] pode liberar e adquirir vários megabytes de memória por segundo, permitindo o ajuste rápido às mudanças na alocação de memória.

## <a name="effects-of-min-and-max-server-memory"></a>Efeitos de memória mínima e máxima do servidor
As opções de configuração *min server memory* e *max server memory* estabelecem limites superiores e inferiores à quantidade de memória usada pelo pool de buffers e por outros caches do Mecanismo de Banco de Dados do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. O pool de buffers não adquire imediatamente a quantidade de memória especificada na min server memory. O pool de buffers é iniciado apenas com a memória exigida para inicialização. Conforme a carga de trabalho do [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] aumenta, ele continua adquirindo a memória exigida para oferecer suporte à carga de trabalho. O pool de buffers não libera a memória adquirida até atingir a quantidade especificada na min server memory. Quando a min server memory é atingida, o pool de buffers usa o algoritmo padrão para adquirir e liberar memória, conforme necessário. A única diferença é que o pool de buffers nunca cancela sua alocação de memória abaixo do nível especificado na min server memory, e nunca adquire mais memória que o nível especificado na max server memory.

> [!NOTE]
> Como um processo, o[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] adquire mais memória do que a especificada pela opção max server memory. Os componentes internos e externos podem alocar memória fora do pool de buffers, que consome memória adicional, mas a memória alocada ao pool de buffers, em geral, ainda representa a parte maior da memória consumida pelo [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].

A quantidade de memória adquirida pelo [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] é completamente dependente da carga de trabalho colocada na instância. Uma instância [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] que não está processando muitas solicitações nunca consegue atingir a min server memory.

Se o mesmo valor for especificado para as opções min server memory e max server memory, então, uma vez que a memória alocada ao [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] alcançar esse valor, o [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] interromperá a liberação e a aquisição dinamicamente para o pool de buffers.

Se uma instância do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] estiver sendo executada em um computador em que outros aplicativos são interrompidos ou iniciados com frequência, a alocação e a desalocação de memória pela instância do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] poderão reduzir as inicializações dos outros aplicativos. Além disso, se o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] for um dos vários aplicativos de servidor em execução em um único computador, os administradores de sistema poderão precisar controlar a quantidade de memória alocada ao [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Nesses casos, você pode usar as opções min server memory e max server memory para controlar a quantidade de memória que o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] pode usar. As opções **min server memory** e **max server memory** são especificadas em megabytes. Para saber mais, veja [Opções de configuração de memória do servidor](../database-engine/configure-windows/server-memory-server-configuration-options.md).

## <a name="memory-used-by-sql-server-objects-specifications"></a>Memória usada por especificações de objetos do SQL Server
A lista a seguir descreve a quantidade aproximada de memória usada por diferentes objetos no [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Os valores listados são estimativas e podem variar dependendo do ambiente e de como os objetos são criados:

* Bloqueio (como mantido pelo Gerenciador de Bloqueios): 64 bytes + 32 bytes por proprietário   
* Conexão do usuário: Aproximadamente (3 \* tamanho_do_pacore_de_rede + 94 KB)    

O **tamanho do pacote de rede** é o tamanho dos pacotes de TDS (esquema de dados de tabela) que são usados para comunicação entre os aplicativos e o Mecanismo de Banco de Dados do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. O tamanho de pacote padrão é 4 KB e é controlado pela opção de configuração tamanho do pacote de rede.

Quando vários conjuntos de resultados ativos estiverem habilitados, a conexão do usuário será de aproximadamente (3 + 3 \*número_de_conexões_lógicas)\* tamanho_do_pacote_de_rede + 94 KB

## <a name="effects-of-min-memory-per-query"></a>Efeitos de min memory per query
A opção de configuração *min memory per query* estabelece a quantidade mínima de memória (em quilobytes) que será alocada para a execução de uma consulta. Isso também é conhecido como a concessão de memória mínima. O início da execução de todas as consultas deve aguardar até que a memória mínima solicitada possa ser protegida ou então até que o valor especificado na opção de configuração de servidor query wait seja excedido. O tipo de espera é acumulado neste cenário é RESOURCE_SEMAPHORE.

> [!IMPORTANT]
> Não defina a opção de configuração de servidor min memory per query com um valor muito alto, especialmente em sistemas muito ocupados, porque isso poderia levar a:         
> - Maior competição por recursos de memória.         
> - Redução de simultaneidade, aumentando a quantidade de memória para cada consulta única mesmo se a memória necessária em tempo de execução é menor que essa configuração.    
>    
> Para obter recomendações sobre como usar essa configuração, consulte [Configurar a opção de configuração de servidor min memory per query](../database-engine/configure-windows/configure-the-min-memory-per-query-server-configuration-option.md#Recommendations).

### <a name="memory-grant-considerations"></a>Considerações de concessão de memória
Para **execução em modo de linha**, a concessão de memória inicial não pode ser excedida sob nenhuma condição. Se mais memória do que a concessão inicial for necessária para executar as operações **hash** ou de **classificação**, essas operações serão despejadas para o disco. Uma operação hash que é despejada tem o suporte de um arquivo de trabalho em TempDB, enquanto uma operação de classificação que é despejada tem o suporte de uma [tabela de trabalho](../relational-databases/query-processing-architecture-guide.md#worktables).   

Um despejo que ocorre durante uma operação de classificação é conhecido como um [aviso de classificação](../relational-databases/event-classes/sort-warnings-event-class.md). Avisos de classificação indicam que operações de classificação não cabem na memória. Isso não inclui operações de classificação envolvendo a criação de índices, somente operações de classificação em uma consulta (como uma cláusula `ORDER BY` usada em uma instrução `SELECT`).

Um despejo que ocorre durante uma operação de hash é conhecido como um [aviso de hash](../relational-databases/event-classes/hash-warning-event-class.md). Esses avisos ocorrem após uma recursão ou cessação de hash (esgotamento de hash ) ocorrer durante uma operação de hash.
-  A recursão de hash ocorre quando a entrada de criação não cabe na memória disponível, ocasionando a divisão da entrada em várias partições que são processadas separadamente. Se qualquer uma dessas partições ainda não couber na memória disponível, ela será dividida em subpartições, que também serão processadas separadamente. Esse processo de divisão continuará até que cada partição caiba na memória disponível ou até que o nível máximo de recursão seja atingido.
-  O esgotamento hash ocorre quando uma operação de hashing atinge o nível máximo de recursão e é deslocada para um plano alternativo, de forma a processar os dados particionados restantes. Esses eventos podem causar a redução do desempenho de seu servidor.

Para **execução em modo de lote**, a concessão de memória inicial pode aumentar dinamicamente até um certo limite interno por padrão. Esse mecanismo de concessão de memória dinâmica é projetado para permitir a execução de operações de **hash** ou de **classificação** residentes na memória executadas em modo de lote. Se essas operações ainda não couberem na memória, elas serão despejadas para o disco.

Para obter mais informações sobre modos de execução, consulte [Guia da Arquitetura de Processamento de Consultas](../relational-databases/query-processing-architecture-guide.md#execution-modes).

## <a name="buffer-management"></a>Gerenciamento de buffer
A principal finalidade de um banco de dados do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] é armazenar e recuperar dados, de modo que a intensa E/S de disco é uma característica importante do Mecanismo de Banco de Dados. Como as operações de E/S de disco podem consumir muitos recursos e levar um tempo relativamente longo para terminar, o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] se concentra em tornar a E/S altamente eficiente. O gerenciamento de buffer é um componente fundamental para alcançar essa eficiência. O componente de gerenciamento de buffer consiste em dois mecanismos: o **gerenciador de buffer** para acessar e atualizar páginas de banco de dados e o **cache do buffer** (também chamado de **pool de buffers**) para reduzir a E/S do arquivo de banco de dados. 

### <a name="how-buffer-management-works"></a>Como funciona o gerenciamento de buffer
Um buffer é uma página de 8 KB da memória, o mesmo tamanho de uma página de dados ou de índice. Portanto, o cache do buffer é dividido em páginas de 8 KB. O gerenciador de buffer gerencia as funções lendo páginas de dados ou de índice dos arquivos do disco de banco de dados no cache do buffer e gravando páginas modificadas de volta no disco. Uma página permanece no cache do buffer até que o gerenciador de buffer precise da área de buffer para ler mais dados. Os dados serão gravados no disco apenas se forem modificados. Os dados podem ser modificados no cache do buffer várias vezes antes de serem gravados no disco. Para saber mais, veja [Lendo Páginas](../relational-databases/reading-pages.md) e [Gravando Páginas](../relational-databases/writing-pages.md).

Quando o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] é iniciado, ele computa o tamanho do espaço de endereço virtual do cache de buffers com base em vários parâmetros, como quantidade de memória física no sistema, número máximo de threads de servidor configurado e vários parâmetros de inicialização. O[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] reserva essa quantidade computada de seu espaço de endereço virtual de processo (chamado de memória cache) do cache de buffers, mas adquire (confirma) somente a quantidade exigida da memória física para a carga atual. Você pode consultar as colunas **bpool_commit_target** e **bpool_committed columns** na exibição do catálogo [sys.dm_os_sys_info](../relational-databases/system-dynamic-management-views/sys-dm-os-sys-info-transact-sql.md) para retornar o número de páginas reservado como destino de memória e o número de páginas atualmente confirmado no cache do buffer, respectivamente.

O intervalo entre a inicialização do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] e o momento em que o cache do buffer obtém seu destino de memória é chamado de ramp-up. Nesse momento, as solicitações de leitura preenchem os buffers conforme necessário. Por exemplo, uma solicitação de leitura de página única de 8 KB preenche apenas uma página de buffer. Isso significa que o ramp-up depende do número e do tipo de solicitações do cliente. O ramp-up é expedido ao transformar as solicitações de leitura de página única em solicitações de oito páginas alinhadas (compondo uma extensão). Isso permite ao ramp-up terminar de forma muito mais rápida, especialmente em máquinas com muita memória. Para obter mais informações sobre páginas e extensões, consulte o [Guia de arquitetura de páginas e extensões](../relational-databases/pages-and-extents-architecture-guide.md#pages-and-extents).

Como o gerenciador de buffer usa a maior parte da memória no processo do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] , ele coopera com o gerenciador de memória para permitir que outros componentes usem seus buffers. O gerenciador de buffer interage principalmente com os seguintes componentes:

* Gerenciador de recurso para controlar o uso de memória global e, em plataformas de 32 bits, controlar o uso de espaço de endereço.  
* Gerenciador de banco de dados e SQLOS ( [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Operating System) para operações de E/S de arquivo de nível baixo.  
* Gerenciador de log para log write-ahead.  

### <a name="supported-features"></a>Recursos com suporte
O gerenciador de buffer oferece suporte aos seguintes recursos:

* O gerenciador de buffer reconhece o **NUMA (acesso não uniforme à memória por software)** . São distribuídas páginas de cache do buffer em nós NUMA de hardware, que permitem a um thread acessar uma página de buffer alocada no nó NUMA local em vez de memória externa. 
* O gerenciador de buffer é compatível com a **Adição de Memória a Quente**, que permite aos usuários adicionar memória física sem reiniciar o servidor. 
* O gerenciador de buffer é compatível com **páginas grandes** em plataformas de 64 bits. O tamanho da página é específico para a versão do Windows.

  > [!NOTE]
  > Antes do [!INCLUDE[ssSQL11](../includes/sssql11-md.md)], a habilitação de páginas grandes no [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] exige o [sinalizador de rastreamento 834](../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md).  

* O gerenciador de buffer fornece diagnósticos adicionais que são expostos por meio de exibições de gerenciamento dinâmico. Você pode usar essas exibições para monitorar uma variedade de recursos de sistema operacional específicos do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Por exemplo, você pode usar a exibição [sys.dm_os_buffer_descriptors](../relational-databases/system-dynamic-management-views/sys-dm-os-buffer-descriptors-transact-sql.md) para monitorar as páginas no cache do buffer.   

### <a name="disk-io"></a>E/S de disco
O gerenciador de buffer apenas faz leituras e gravações no banco de dados. Outras operações de arquivo e banco de dados, como abrir, fechar, estender e reduzir são executadas pelos componentes do gerenciador de banco de dados e de arquivos. 

As operações de E/S de disco pelo gerenciador de buffer têm as seguintes características:

* Todas as E/S são executadas de forma assíncrona, o que permite ao thread de chamada continuar o processamento enquanto a operação de E/S acontece em segundo plano.
* Todas as E/S são emitidas nos threads de chamada, a menos que a opção affinity I/O esteja em uso. A opção affinity I/O mask associa a E/S de disco do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] a um subconjunto especificado de CPUs. Em ambientes OLTP (online transactional processing) avançados de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] , esta extensão pode aumentar o desempenho de threads [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] que emitem E/S.
* Várias E/Ss de página são realizadas com E/S de dispersar e reunir, que permite transferir dados para dentro ou para fora de áreas não contíguas de memória. Isso significa que o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] pode preencher ou liberar o cache do buffer rapidamente enquanto evita várias solicitações de E/S físicas. 

#### <a name="long-io-requests"></a>Solicitações de E/S demoradas  
O gerenciador de buffer fornece informações sobre qualquer solicitação de E/S pendente durante pelo menos 15 segundos. Isso ajuda o administrador de sistema a distinguir entre problemas do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] e problemas do subsistema de E/S. A mensagem de erro 833 é informada e exibida no log de erros do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] como segue:

`SQL Server has encountered ## occurrence(s) of I/O requests taking longer than 15 seconds to complete on file [##] in database [##] (#). The OS file handle is 0x00000. The offset of the latest long I/O is: 0x00000.` 

Uma E/S demorada pode ser uma leitura ou uma gravação. Isso não está indicado atualmente na mensagem. Mensagens de E/S demoradas são avisos, não erros. Elas não indicam problemas com o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], mas com o sistema de E/S subjacente. As mensagens são informadas para ajudar o administrador de sistema a encontrar mais depressa a causa de tempos de resposta insatisfatórios do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] e distinguir problemas que estão fora do controle do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Como tal, eles não exigem nenhuma ação, mas o administrador do sistema deve investigar por que a solicitação de E/S demorou tanto e se o tempo é justificável.

#### <a name="causes-of-long-io-requests"></a>Causas de solicitações de E/S demoradas  
Uma mensagem de E/S demorada pode indicar que uma E/S está bloqueada permanentemente e nunca será concluída (conhecida como E/S perdida) ou, então, que apenas não foi concluída ainda. Não é possível distinguir qual é o cenário com base na mensagem, embora uma E/S perdida geralmente conduza a um tempo limite de trava.

E/S demorada geralmente indica uma carga de trabalho do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] muito intensa para o subsistema de disco. Um subsistema de disco inadequado pode ser indicado quando:

* Várias mensagens de E/S demorada são exibidas no log de erros durante uma carga de trabalho pesada do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] .
* Contadores de desempenho mostram latências de disco demoradas, filas de disco demoradas ou nenhum tempo ocioso de disco.  

E/Ss demoradas também podem ser causadas por um componente no caminho de E/S (por exemplo, driver, controlador ou firmware) que continuamente adia o atendimento de uma solicitação de E/S antiga a favor do atendimento mais próximo à posição atual da cabeça de disco. A técnica comum de processamento de solicitações com prioridade baseada no atendimento mais próximo à posição atual da cabeça de leitura/gravação é conhecida como "busca de menor caminho". Isso pode ser difícil de confirmar com a ferramenta do Windows System Monitor (PERFMON.EXE) porque a maioria das E/Ss está sendo atendida prontamente. As solicitações de E/S demoradas podem ser agravadas por cargas de trabalho que executam grandes quantidades de E/S sequenciais, como backup e restauração, exames de tabela, classificação, criação de índices, carregamentos em massa e anulação de arquivos de saída.

E/Ss demoradas e isoladas que não aparecem relacionadas a quaisquer condições anteriores podem ser causadas por um problema de hardware ou driver. O log de eventos do sistema pode conter um evento relacionado que ajuda a diagnosticar o problema.

### <a name="memory-pressure-detection"></a>Detecção de demanda de memória
A demanda de memória é uma condição decorrente da falta de memória e pode resultar em:
- E/S extra (por exemplo, um thread em segundo plano de gravador lento muito ativo)
- Maior taxa de recompilação
- Consultas de execução mais longa (se existirem esperas por concessão de memória)
- Ciclos de CPU adicionais

Essa situação pode ser acionada por causas externas ou internas. As causas externas incluem:
- A RAM (memória física disponível) é insuficiente. Isso faz com que o sistema corte conjuntos de trabalho de processos atualmente em execução, o que pode resultar em um retardamento geral. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] pode reduzir o destino de confirmação de pool de buffers e passar a cortar caches internos com mais frequência. 
- A memória de sistema geral disponível (que inclui o arquivo de paginação do sistema) está baixa. Isso pode causar falha em alocações de memória pelo sistema, já que ele não é capaz de realizar page-out da memória alocada atualmente.
As causas internas incluem:
- Resposta à demanda de memória externa, quando o [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] define limites de uso de memória mais baixos.
- As configurações de memória foram reduzidas manualmente reduzindo-se a configuração *max server memory*. 
- Alterações na distribuição de memória de componentes internos entre os vários caches.

O [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] implementa uma estrutura dedicada a detectar e manipular a demanda de memória, como parte do seu gerenciamento de memória dinâmica. Essa estrutura inclui a tarefa de fundo chamada **Monitor de Recursos**. A tarefa de Monitor de Recursos monitora o estado de indicadores de memória interna e externa. Depois que o status de um desses indicadores se altera, ele calcula a notificação correspondente e a difunde. Essas notificações são mensagens internas de cada um dos componentes do mecanismo e armazenadas em buffers de anéis. 

Dois buffers de anéis mantêm informações relevantes para o gerenciamento de memória dinâmica: 
- O buffer de anéis de Monitor de Recursos, que acompanha a atividade do Monitor de Recursos, por exemplo, se a demanda de memória foi sinalizada ou não. Esse buffer de anéis tem informações de status, dependendo da condição atual de *RESOURCE_MEMPHYSICAL_HIGH*, *RESOURCE_MEMPHYSICAL_LOW*, *RESOURCE_MEMPHYSICAL_STEADY* ou *RESOURCE_MEMVIRTUAL_LOW*.
- O buffer de anéis do agente de memória, que contém registros de notificações de memória para cada pool de recursos do Resource Governor. Conforme a demanda de memória interna é detectada, a notificação de memória baixa é ativada para os componentes que alocam memória, de modo a disparar ações destinadas a equilibrar a memória entre caches. 

Agentes de memória monitoram o consumo de demanda de memória por cada componente e então, com base nas informações coletadas, calculam o valor ideal de memória para cada um desses componentes. Há um conjunto de agentes para cada pool de recursos do Resource Governor. Essas informações são então difundidas para cada um dos componentes que aumentam ou diminuem seu uso conforme necessário.
Para obter mais informações sobre agentes de memória, consulte [sys.dm_os_memory_brokers](../relational-databases/system-dynamic-management-views/sys-dm-os-memory-brokers-transact-sql.md). 

### <a name="error-detection"></a>Detecção de erro  
As páginas de banco de dados podem usar um dentre dois mecanismos opcionais que ajudam a garantir a integridade da página do momento em que é gravada no disco até ser lida novamente: proteção de página interrompida e proteção de soma de verificação. Esses mecanismos permitem um método independente para verificar a exatidão não apenas do armazenamento de dados, mas de componentes de hardware, como controladores, drivers, cabos e até mesmo o sistema operacional. A proteção é adicionada à página um pouco antes da gravação no disco e verificada depois da leitura do disco.

O [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] repetirá mais quatro vezes qualquer leitura que falhe com uma soma de verificação, página interrompida ou outro erro de E/S. Se a leitura tiver êxito em qualquer uma das novas tentativas, uma mensagem será gravada no log de erros e o comando que disparou a leitura continuará. Se as novas tentativas falharem, o comando falhará com a mensagem de erro 824. 

O tipo de proteção de página usado é um atributo do banco de dados que contém a página. A proteção de soma de verificação é a proteção padrão para bancos de dados criados no [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)] e posterior. O mecanismo de proteção da página é especificado no momento da criação do banco de dados e pode ser alterado usando a opção ALTER DATABASE SET. Você pode determinar a configuração de proteção da página atual, consultando a coluna *page_verify_option* na exibição do catálogo [sys.databases](../relational-databases/system-catalog-views/sys-databases-transact-sql.md) ou na propriedade *IsTornPageDetectionEnabled* da função [DATABASEPROPERTYEX](../t-sql/functions/databasepropertyex-transact-sql.md). 

> [!NOTE]
> Se a configuração de proteção de página for alterada, a configuração nova não afetará imediatamente o banco de dados inteiro. Em vez disso, as páginas adotarão o nível de proteção atual do banco de dados sempre que eles forem gravados posteriormente. Isso significa que o banco de dados pode ser composto de páginas com tipos diferentes de proteção. 

#### <a name="torn-page-protection"></a>Proteção de página interrompida  
A proteção de página interrompida , apresentada no [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 2000, é principalmente um modo de detectar páginas corrompidas devido a falhas de energia. Por exemplo, uma falha de energia inesperada pode deixar apenas parte de uma página gravada no disco. Quando a proteção de página interrompida é usada, um padrão de assinatura de 2 bits específico para cada setor de 512 bytes na página de banco de dados de 8 KB (quilobytes) é salvo e armazenado no cabeçalho da página do banco de dados, quando a página é gravada em disco. Quando a página for lida pelo disco, os bits desativados armazenados no cabeçalho da página serão comparados às informações do setor da página real. O padrão de assinatura alterna entre os binários 01 e 10 com cada gravação, de modo que seja sempre possível informar quando apenas uma parte dos setores realizou essa operação no disco: se um bit estiver com estado inválido quando a página tiver sido lida posteriormente, a página terá sido gravada incorretamente e uma página interrompida será detectada. A detecção de página interrompida usa recursos mínimos; porém, não detecta todos os erros provocados por falhas de hardware de disco. Para obter informações sobre como configurar a detecção de página interrompida, consulte [Opções ALTER DATABASE SET &#40;Transact-SQL&#41;](../t-sql/statements/alter-database-transact-sql-set-options.md#page_verify).

#### <a name="checksum-protection"></a>Proteção de soma de verificação  
A proteção de soma de verificação, apresentada no [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)], fornece uma verificação de integridade de dados mais resistente. Uma soma de verificação é calculada para os dados de cada página gravada e armazenada no cabeçalho da página. Sempre que uma página com uma soma de verificação armazenada é lida no disco, o Mecanismo de Banco de Dados recalcula a soma de verificação dos dados na página e gera o erro 824 se a nova soma de verificação for diferente da soma de verificação armazenada. A proteção de soma de verificação pode capturar mais erros que a proteção de página interrompida porque é afetada por todo byte da página, porém, é um recurso moderadamente intensivo. Quando a soma de verificação for habilitada, os erros causados por falta de energia e falha de hardware ou firmware poderão ser detectados sempre que o gerenciador de buffer ler uma página do disco. Para obter informações sobre como configurar a soma de verificação, consulte [Opções ALTER DATABASE SET &#40;Transact-SQL&#41;](../t-sql/statements/alter-database-transact-sql-set-options.md#page_verify).

> [!IMPORTANT]
> Quando um usuário ou banco de dados do sistema é atualizado para o [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)] ou posterior, o valor de [PAGE_VERIFY](../t-sql/statements/alter-database-transact-sql-set-options.md#page_verify) (NONE ou TORN_PAGE_DETECTION) é retido. Recomendamos o uso de CHECKSUM.
> TORN_PAGE_DETECTION pode usar menos recursos, mas fornece um subconjunto mínimo da proteção CHECKSUM.

## <a name="understanding-non-uniform-memory-access"></a>Compreendendo o Non-uniform Memory Access
O [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] reconhece o NUMA (Non-uniform Memory Access) e tem um bom desempenho em hardware de NUMA sem configuração especial. Devido ao aumento da velocidade de clock e do número de processadores, fica muito difícil reduzir a latência de memória exigida para usar este poder de processamento adicional. Para evitar isto, fornecedores de hardware fornecem caches de L3 grandes, mas esta é apenas uma solução limitada. A arquitetura NUMA oferece uma solução escalonável para esse problema. O[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] foi projetado para tirar proveito de computadores baseados em NUMA sem exigir nenhuma mudança de aplicativo. Para obter mais informações, confira [Como configurar o SQL Server para usar o Soft-NUMA](../database-engine/configure-windows/soft-numa-sql-server.md).

## <a name="see-also"></a>Consulte Também
[Opções Server Memory de configuração do servidor](../database-engine/configure-windows/server-memory-server-configuration-options.md)   
[Lendo Páginas](../relational-databases/reading-pages.md)   
[Gravando Páginas](../relational-databases/writing-pages.md)   
[Como configurar o SQL Server para usar o Soft-NUMA](../database-engine/configure-windows/soft-numa-sql-server.md)   
[Requisitos para usar tabelas com otimização de memória](../relational-databases/in-memory-oltp/requirements-for-using-memory-optimized-tables.md)   
[Resolver problemas de memória insuficiente usando tabelas com otimização de memória](../relational-databases/in-memory-oltp/resolve-out-of-memory-issues.md)
