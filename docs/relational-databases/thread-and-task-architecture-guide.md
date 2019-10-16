---
title: Guia de arquitetura de thread e tarefa | Microsoft Docs
ms.custom: ''
ms.date: 10/11/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- guide, thread and task architecture
- thread and task architecture guide
ms.assetid: 925b42e0-c5ea-4829-8ece-a53c6cddad3b
author: pmasl
ms.author: jroth
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 08efd7847fba1ad0b4df10d3a761475c735ceca8
ms.sourcegitcommit: 43c3d8939f6f7b0ddc493d8e7a643eb7db634535
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2019
ms.locfileid: "72289376"
---
# <a name="thread-and-task-architecture-guide"></a>guia de arquitetura de threads e tarefas
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

## <a name="operating-system-task-scheduling"></a>Agendamento de tarefas do sistema operacional
Os threads são as menores unidades de processamento que podem ser executadas por um sistema operacional e permitem que a lógica do aplicativo seja separada em vários caminhos de execução simultâneos. Eles são úteis quando aplicativos complexos têm muitas tarefas que podem ser executadas ao mesmo tempo. 

Quando um sistema operacional executa uma instância de um aplicativo, cria uma unidade denominada processo para gerenciar a instância. O processo tem um thread de execução. Tal processo é a série de instruções de programação executada pelo código de aplicativo. Por exemplo, se um aplicativo simples tiver um único conjunto de instruções que podem ser executadas em série, esse conjunto de instruções é manuseado como uma **tarefa** simples e haverá apenas um caminho de execução (ou **thread**) no aplicativo. Os aplicativos mais complexos podem ter várias **tarefas** que podem ser executadas em simultaneamente, em vez de em série. Um aplicativo pode fazer isso iniciando processos separados para cada tarefa, que é uma operação com uso de muitos recursos, ou iniciar threads separados, que relativamente utilizam menos recursos. Além disso, cada thread pode ser agendado para execução independentemente dos outros threads associados a um processo.

Os threads permitem aplicativos complexos para utilizar com mais eficácia uma CPU (processador), mesmo em computadores com uma única CPU. Com uma CPU, apenas um thread pode ser executado de cada vez. Se um thread executar uma operação longa que não usa a CPU, como leitura ou gravação de disco, outro thread poderá ser executado até que a primeira operação seja concluída. Com a possibilidade de executar threads enquanto outros threads estão esperando pela conclusão de uma operação, o aplicativo consegue maximizar o uso da CPU. Isso é especialmente verdadeiro para aplicativos intensivos multiusuário e de E/S de disco, como um servidor de banco de dados. Os computadores que têm várias CPUs podem executar um thread por CPU ao mesmo tempo. Por exemplo, se um computador tiver oito CPUs, poderá executar oito threads ao mesmo tempo.

## <a name="sql-server-task-scheduling"></a>Agendamento de tarefas SQL Server
No escopo de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], uma **solicitação** é a representação lógica de uma consulta ou lote. Uma solicitação também representa operações exigidas por threads do sistema, como ponto de verificação ou gravador de log. As solicitações existem em vários Estados durante seu tempo de vida e podem acumular esperas quando os recursos necessários para executar a solicitação não estão disponíveis, como [bloqueios](../relational-databases/system-dynamic-management-views/sys-dm-tran-locks-transact-sql.md#locks) ou [travas](../relational-databases/system-dynamic-management-views/sys-dm-os-latch-stats-transact-sql.md#latches). Para saber mais sobre os estados de solicitação, confira [sys.dm_exec_requests](../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md).

Uma **tarefa** representa a unidade de trabalho que precisa ser concluída para atender à solicitação. Uma ou mais tarefas podem ser atribuídas a uma única solicitação. As solicitações paralelas terão várias tarefas ativas que são executadas simultaneamente em vez de em série. Uma solicitação que é executada em série terá apenas uma tarefa ativa em um determinado momento. Existem tarefas em vários estados durante seu tempo de vida. Para saber mais sobre os estados de tarefas, confira [sys.dm_os_tasks](../relational-databases/system-dynamic-management-views/sys-dm-os-tasks-transact-sql.md). O termo Tarefas indica um estado SUSPENSO que está aguardando os recursos necessários para executar a tarefa a ser disponibilizada. Para saber mais sobre a tarefa de espera, confira [sys.dm_os_waiting_tasks](../relational-databases/system-dynamic-management-views/sys-dm-os-waiting-tasks-transact-sql.md).

Um [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] **thread de trabalho**, também conhecido como trabalho ou thread, é uma representação lógica de um thread do sistema operacional. Ao executar solicitações em série, [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] gera um trabalho para executar a tarefa ativa. Ao executar solicitações paralelas no [modo linha](../relational-databases/query-processing-architecture-guide.md#execution-modes), [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] atribui um trabalho para coordenar os trabalhos secundários responsáveis por concluir tarefas atribuídas a eles. O número de threads de trabalho gerados para cada tarefa depende:
-   Se a solicitação foi qualificada para paralelismo, conforme determinado pelo Otimizador de Consulta.
-   Qual é o [DOP (grau de paralelismo)](../relational-databases/query-processing-architecture-guide.md#DOP) real disponível no sistema com base na carga atual. Isso pode ser diferente do DOP estimado, que é baseado na configuração do servidor para MAXDOP (grau máximo de paralelismo). Por exemplo, a configuração do servidor para MAXDOP pode ser 8, mas o DOP disponível no tempo de execução pode ser apenas 2, o que afeta o desempenho da consulta. 

> [!NOTE]
> O limite do **MAXDOP (grau máximo de paralelismo)** é definido por tarefa, não por solicitação. Isso significa que durante uma execução de consulta paralela, uma única solicitação pode gerar várias tarefas, e cada tarefa pode usar vários trabalhos até o limite do MAXDOP. Para saber mais sobre MAXDOP, confira [Definir a Opção de Configuração do Servidor de grau máximo de paralelismo](../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md).

Um **agendador**, também conhecido como Agendador SOS, gerencia threads de trabalho que exigem tempo de processamento para realizar trabalho em nome das tarefas. Cada agendador é mapeado para um CPU (processador individual). O tempo que um trabalho pode permanecer ativo em um agendador é chamado de quantum do sistema operacional, com um máximo de 4 ms. Depois que o tempo do quantum expirar, um trabalho dedica seu tempo para outros trabalhos que precisam acessar os recursos da CPU e altera seu estado. Essa cooperação entre os trabalhos para maximizar o acesso aos recursos da CPU é chamada de **agendamento cooperativo**, também conhecido como agendamento não preemptivo. Por sua vez, a alteração no estado de trabalho é propagada para a tarefa associada a esse trabalho e para a solicitação associada à tarefa. Para sabe mais sobre os estados de trabalho, confira [sys.dm_os_workers](../relational-databases/system-dynamic-management-views/sys-dm-os-workers-transact-sql.md). Para saber mais sobre agendadores, confira [sys.dm_os_schedulers ](../relational-databases/system-dynamic-management-views/sys-dm-os-schedulers-transact-sql.md). 

### <a name="allocating-threads-to-a-cpu"></a>Como alocar threads a uma CPU
Por padrão, cada instância do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] inicia cada thread e o sistema operacional distribui threads de instâncias do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] entre os microprocessadores ou as CPUs (processadores) em um computador com base na carga. Se a afinidade do processo tiver sido habilitada no nível do sistema operacional, este atribuirá cada thread a uma CPU específica. Em contraste, o [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] atribui **threads de trabalho** [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] aos **agendadores** que distribuem os threads uniformemente entre as CPUs.
    
Para multitarefa, por exemplo quando vários aplicativos acessam o mesmo conjunto de CPUs, às vezes, o sistema operacional move threads de trabalho entre diferentes CPUs. Embora eficiente de um ponto de vista de sistema operacional, essa atividade pode reduzir o desempenho do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] sob cargas de sistema pesadas, à medida que cada cache de processador é recarregado repetidamente com dados. Atribuir CPUs a threads específicos poderá melhorar o desempenho nessas condições eliminando recargas de processador e reduzindo a migração de thread entre CPUs (reduzindo portanto a alternância de contexto); tal associação entre um thread e um processador é chamada de afinidade do processador. Se a afinidade foi habilitada, o sistema operacional atribuirá cada thread a uma CPU específica. 

A [opção de máscara de afinidade](../database-engine/configure-windows/affinity-mask-server-configuration-option.md) é definida usando [ALTER SERVER CONFIGURATION](../t-sql/statements/alter-server-configuration-transact-sql.md). Quando a máscara de afinidade não é definida, a instância de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] alocará threads de trabalho entre os agendadores sem máscaras especificadas.

> [!CAUTION]
> Não configure afinidade de CPU no sistema operacional e também configure a máscara de afinidade em [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Essas definições estão tentando alcançar o mesmo resultado e se as configurações forem inconsistentes, você poderá ter resultados imprevisíveis. Para saber mais, confira [opção de máscara de afinidade](../database-engine/configure-windows/affinity-mask-server-configuration-option.md).

O thread pooling ajuda a otimizar o desempenho quando são conectados grandes números de clientes ao servidor. Normalmente, é criado um thread de sistema operacional separado para cada solicitação de consulta. Porém, com centenas de conexões para o servidor, usam um thread por solicitação de consulta pode consumir quantias grandes de recursos do sistema. A [opção máximo de threads de trabalho](../database-engine/configure-windows/configure-the-max-worker-threads-server-configuration-option.md) habilita o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] para criar um pool de threads de trabalho para atender a um número maior de solicitações de consulta, o que melhora o desempenho. 

### <a name="using-the-lightweight-pooling-option"></a>Usando a opção lightweight pooling
A sobrecarga envolvida na troca de contextos de thread pode não ser muito grande. A maioria das instâncias do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] não observará nenhuma diferença de desempenho entre a configuração da opção lightweight pooling como 0 ou 1. As únicas instâncias do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] que podem obter benefícios do [lightweight pooling](../database-engine/configure-windows/lightweight-pooling-server-configuration-option.md) são aquelas executadas em um computador que tem as seguintes características:    
* Um servidor grande com várias CPUs
* Todas as CPUs executadas em capacidade próxima à máxima
* Há um nível alto de troca de contexto

Esses sistemas poderão observar um pequeno aumento no desempenho se o valor lightweight pooling for definido como 1.

> [!IMPORTANT]
> Não use o agendamento do modo fibra para operação de rotina. Isso pode diminuir o desempenho inibindo os benefícios regulares de troca de contexto e porque alguns componentes do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] não funcionam corretamente no modo fibra. Para saber mais, confira [lightweight pooling](../database-engine/configure-windows/lightweight-pooling-server-configuration-option.md).

## <a name="thread-and-fiber-execution"></a>Execução de fibra e thread
O Microsoft Windows usa um sistema de prioridade numérica que varia de 1 a 31 para agendar threads para execução. Zero é reservado para uso do sistema operacional. Quando vários threads estão esperando para serem executados, o Windows despacha o thread com a prioridade mais alta.

Por padrão, cada instância do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] tem prioridade 7, conhecida como a prioridade normal. Esse padrão fornece aos threads do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] uma prioridade alta o bastante para obter recursos de CPU suficientes sem prejudicar outros aplicativos. 

A opção de configuração [aumento de prioridade](../database-engine/configure-windows/configure-the-priority-boost-server-configuration-option.md) pode ser usada para aumentar a prioridade dos threads de uma instância do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] para 13. Isso é conhecido como prioridade alta. Essa configuração fornece aos threads uma prioridade mais alta [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] do que a maioria dos outros aplicativos. Portanto, os threads do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] geralmente são despachados sempre que estão prontos para serem executados e não são evitados por threads de outros aplicativos. Isso pode melhorar o desempenho quando um servidor estiver executando apenas instâncias do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] e nenhum outro aplicativo. Porém, se uma operação com intensa utilização de memória ocorrer no [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], outros aplicativos provavelmente não terão prioridade alta o bastante para evitar o thread do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. 

Se você estiver executando várias instâncias do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] em um computador, e aumentar a prioridade apenas para algumas das instâncias, o desempenho de qualquer instância que estiver sendo executada na prioridade normal poderá ser prejudicado. Além disso, o desempenho de outros aplicativos e componentes no servidor poderá piorar se o aumento de prioridade for ativado. Portanto, ele só deveria ser usado em condições estritamente controladas.

## <a name="hot-add-cpu"></a>Inclusão de CPU a quente
Inclusão de CPU a quente é a capacidade de adicionar dinamicamente CPUs a um sistema em execução. A inclusão de CPUs pode ocorrer fisicamente, pela adição de um novo hardware; logicamente, pelo particionamento do hardware online; ou virtualmente, através de uma camada de virtualização. Começando com o [!INCLUDE[ssKatmai](../includes/ssKatmai-md.md)], o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] dá suporte à adição de CPU a quente.

Requisitos para a inclusão de CPU a quente:  
* Requer hardware que ofereça suporte à inclusão de CPU a quente.
* Requer a edição de 64 bits do sistema operacional Windows Server 2008 Datacenter ou Windows Server 2008 Enterprise Edition para Sistemas Baseados no Itanium.
* Requer o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Enterprise.
* [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] não pode ser configurado para usar NUMA temporário. Para saber mais sobre soft-NUMA, veja [Soft-NUMA (SQL Server)](../database-engine/configure-windows/soft-numa-sql-server.md).

[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] não começa a usar as CPUs automaticamente depois que elas são incluídas. Isso impede o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] de usar CPUs que possam ser incluídas para algum outro propósito. Depois de adicionar CPUs, execute a instrução [RECONFIGURE](../t-sql/language-elements/reconfigure-transact-sql.md) de forma que [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] reconhecerá as novas CPUs como recursos disponíveis.

> [!NOTE]
> Se a [máscara affinity64](../database-engine/configure-windows/affinity64-mask-server-configuration-option.md) for configurada, ela deverá ser modificada para usar as CPUs novas.
 
## <a name="best-practices-for-running-sql-server-on-computers-that-have-more-than-64-cpus"></a>Práticas recomendadas para executar o SQL Server em computadores que têm mais de 64 CPUs

### <a name="assigning-hardware-threads-with-cpus"></a>Atribuindo threads de hardware com CPUs
Não use as opções de configuração do servidor máscara affinity e máscara affinity64 para associar processadores a threads específicos. Essas opções são limitadas a 64 CPUs. Em vez disso, use a opção `SET PROCESS AFFINITY` de [ALTER SERVER CONFIGURATION](../t-sql/statements/alter-server-configuration-transact-sql.md).

### <a name="managing-the-transaction-log-file-size"></a>Como gerenciar o tamanho do arquivo de log de transações
Não confie no aumento automático para aumentar o tamanho do arquivo de log de transações. O aumento do log de transação deve ser um processo serial. A extensão do log pode impedir a continuação de operações de gravação de transação até que a extensão de log seja concluída. Em vez disso, pré-aloque espaço para os arquivos de log definindo o tamanho de arquivo para um valor grande o bastante para oferecer suporte à carga de trabalho comum no ambiente.

### <a name="setting-max-degree-of-parallelism-for-index-operations"></a>Definição do grau máximo de paralelismo para operações de índice
O desempenho de operações de índice, como criar ou recompilar índices, pode ser melhorado em computadores com muitas CPUs definindo-se temporariamente o modelo de recuperação do banco de dados como bulk-logged ou simples. Essas operações de índice podem gerar atividade de log significativa, e a contenção de log pode afetar a melhor opção de DOP (grau de paralelismo) feita pelo [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].

Além de ajustar a opção de configuração de servidor de **MAXDOP (grau máximo de paralelismo)** , considere ajustar o paralelismo para operações de índice usando a [opção MAXDOP](../t-sql/statements/alter-index-transact-sql.md). Para obter mais informações, consulte [Configurar operações de índice paralelo](../relational-databases/indexes/configure-parallel-index-operations.md). Para saber mais e obter diretrizes sobre como ajustar a opção de configuração de servidor de grau máximo de paralelismo, confira [Definir a Opção de Configuração do Servidor de grau máximo de paralelismo](../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md).

### <a name="setting-the-maximum-number-of-worker-threads"></a>Configurar o número máximo de threads de trabalho
[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] configurará dinamicamente a opção de configuração de servidor de **máximo de threads de trabalho** na inicialização. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] usa o número de CPUs disponíveis e a arquitetura do sistema para determinar essa configuração de servidor durante a inicialização, usando uma [fórmula](../database-engine/configure-windows/configure-the-max-worker-threads-server-configuration-option.md#Recommendations) documentada.

Esta é uma opção avançada e deve ser alterada somente por um administrador de banco de dados experiente ou por um profissional certificado do SQL Server. Se você suspeitar que há um problema de desempenho, é provável que não seja a disponibilidade dos threads de trabalho. A causa mais provável é que algo, como a E/S, está fazendo com que os threads de trabalho aguardem. É melhor localizar a causa raiz de um problema de desempenho antes de alterar a configuração max worker threads. No entanto, se você precisar definir manualmente o número máximo de threads de trabalho, esse valor de configuração sempre deve ser definido como no mínimo sete vezes o número de CPUs presentes no sistema. Para saber mais, confira [Configurar o máximo de threads de trabalho](../database-engine/configure-windows/configure-the-max-worker-threads-server-configuration-option.md).

### <a name="using-sql-trace-and-sql-server-profiler"></a>Usando o Rastreamento do SQL e o SQL Server Profiler
É recomendável que você não use o Rastreamento do SQL e o SQL Profiler em um ambiente de produção. A sobrecarga para a execução dessas ferramentas também aumenta à medida que o número de CPUs cresce. Se você usar o Rastreamento do SQL em um ambiente de produção, limite o número de eventos de rastreamento a um nível mínimo. Crie perfis e teste cuidadosamente cada evento de rastreamento sob carga e evite usar combinações de eventos que afetem o desempenho de modo significativo.

> [!IMPORTANT]
> Rastreamento do SQL e [!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)] estão preteridos. O namespace *Microsoft.SqlServer.Management.Trace* que contém os objetos Trace e Replay do Microsoft SQL Server também foi preterido. 
> [!INCLUDE[ssNoteDepFutureAvoid](../includes/ssnotedepfutureavoid-md.md)] 
> Em vez disso, use Eventos Estendidos. Para obter mais informações sobre [Eventos Estendidos](../relational-databases/extended-events/extended-events.md), confira [Início rápido: eventos estendidos no SQL Server](../relational-databases/extended-events/quick-start-extended-events-in-sql-server.md) e no [SSMS XEvent Profiler](../relational-databases/extended-events/use-the-ssms-xe-profiler.md).

> [!NOTE]
> [!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)] para as cargas de trabalho do Analysis Services NÃO está preterido e o suporte a ele continuará.

### <a name="setting-the-number-of-tempdb-data-files"></a>Definição do número de arquivos de dados TempDB
O número de arquivos depende do número de processadores (lógicos) do computador. Como regra geral, se o número de processadores lógicos for menor ou igual a oito, use o mesmo número de processadores lógicos para os arquivos de dados. Se o número de processadores lógicos for maior que oito, use oito arquivos de dados e, se a contenção persistir, aumente o número de arquivos de dados em múltiplos de quatro até que a contenção seja reduzida a níveis aceitáveis ou faça alterações no código/carga de trabalho. Além disso, lembre-se de outras recomendações para o TempDB, disponível em [Otimizando o desempenho de TempDB no SQL Server](../relational-databases/databases/tempdb-database.md#optimizing-tempdb-performance-in-sql-server). 

No entanto, ao considerar cuidadosamente as necessidades simultâneas de tempdb, é possível reduzir a sobrecarga de gerenciamento do banco de dados. Por exemplo, se um sistema tiver 64 CPUs e geralmente apenas 32 consultas usam tempdb, o aumento do número de arquivos tempdb para 64 não melhorará o desempenho.

### <a name="sql-server-components-that-can-use-more-than-64-cpus"></a>Componentes do SQL Server que podem usar mais de 64 CPUs
A tabela a seguir lista os componentes do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] e indica se eles podem usar mais de 64 CPUs.

|Nome do processo   |Programa executável |Usar mais de 64 CPUs |  
|----------|----------|----------|  
|Mecanismo de Banco de Dados do SQL Server |Sqlserver.exe  |Sim |  
|Reporting Services |Rs.exe |Não |  
|Analysis Services  |As.exe |Não |  
|Integration Services   |Is.exe |Não |  
|Service Broker |Sb.exe |Não |  
|Pesquisa de Texto Completo   |Fts.exe    |Não |  
|SQL Server Agent   |Sqlagent.exe   |Não |  
|SQL Server Management Studio   |Ssms.exe   |Não |  
|instalação do SQL Server   |Setup.exe  |Não |  
