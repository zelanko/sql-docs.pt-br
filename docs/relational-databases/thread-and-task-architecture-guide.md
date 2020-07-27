---
title: Guia de arquitetura de thread e tarefa | Microsoft Docs
description: Saiba mais sobre a arquitetura de threads e tarefas no SQL Server, incluindo o agendamento de tarefas, a inclusão de CPU a quente e as práticas recomendadas para usar computadores com mais de 64 CPUs.
ms.custom: ''
ms.date: 07/06/2020
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
ms.openlocfilehash: f61fad1afac14c2e6a27314e2a65371722ee9b23
ms.sourcegitcommit: edba1c570d4d8832502135bef093aac07e156c95
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/20/2020
ms.locfileid: "86485568"
---
# <a name="thread-and-task-architecture-guide"></a>guia de arquitetura de threads e tarefas
[!INCLUDE [SQL Server Azure SQL Database](../includes/applies-to-version/sql-asdb.md)]

## <a name="operating-system-task-scheduling"></a>Agendamento de tarefas do sistema operacional
Os threads são as menores unidades de processamento que podem ser executadas por um sistema operacional e permitem que a lógica do aplicativo seja separada em vários caminhos de execução simultâneos. Eles são úteis quando aplicativos complexos têm muitas tarefas que podem ser executadas ao mesmo tempo. 

Quando um sistema operacional executa uma instância de um aplicativo, cria uma unidade denominada processo para gerenciar a instância. O processo tem um thread de execução. Tal processo é a série de instruções de programação executada pelo código de aplicativo. Por exemplo, se um aplicativo simples tiver um único conjunto de instruções que podem ser executadas em série, esse conjunto de instruções é manuseado como uma **tarefa** simples e haverá apenas um caminho de execução (ou **thread**) no aplicativo. Os aplicativos mais complexos podem ter várias **tarefas** que podem ser executadas em simultaneamente, em vez de em série. Um aplicativo pode fazer isso iniciando processos separados para cada tarefa, que é uma operação com uso de muitos recursos, ou iniciar threads separados, que relativamente utilizam menos recursos. Além disso, cada thread pode ser agendado para execução independentemente dos outros threads associados a um processo.

Os threads permitem aplicativos complexos para utilizar com mais eficácia uma CPU (processador), mesmo em computadores com uma única CPU. Com uma CPU, apenas um thread pode ser executado de cada vez. Se um thread executar uma operação longa que não usa a CPU, como leitura ou gravação de disco, outro thread poderá ser executado até que a primeira operação seja concluída. Com a possibilidade de executar threads enquanto outros threads estão esperando pela conclusão de uma operação, o aplicativo consegue maximizar o uso da CPU. Isso é especialmente verdadeiro para aplicativos intensivos multiusuário e de E/S de disco, como um servidor de banco de dados. Os computadores que têm várias CPUs podem executar um thread por CPU ao mesmo tempo. Por exemplo, se um computador tiver oito CPUs, poderá executar oito threads ao mesmo tempo.

## <a name="sql-server-task-scheduling"></a>Agendamento de tarefas SQL Server
No escopo de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], uma **solicitação** é a representação lógica de uma consulta ou lote. Uma solicitação também representa operações exigidas por threads do sistema, como ponto de verificação ou gravador de log. As solicitações existem em vários Estados durante seu tempo de vida e podem acumular esperas quando os recursos necessários para executar a solicitação não estão disponíveis, como [bloqueios](../relational-databases/system-dynamic-management-views/sys-dm-tran-locks-transact-sql.md#locks) ou [travas](../relational-databases/system-dynamic-management-views/sys-dm-os-latch-stats-transact-sql.md#latches). Para saber mais sobre os estados de solicitação, confira [sys.dm_exec_requests](../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md).

Uma **tarefa** representa a unidade de trabalho que precisa ser concluída para atender à solicitação. Uma ou mais tarefas podem ser atribuídas a uma única solicitação. 
-  As solicitações paralelas terão várias tarefas ativas que serão executadas de maneira simultânea em vez de serial, com uma **tarefa pai** (ou tarefa de coordenação) e várias **tarefas filho**. O plano de execução de uma solicitação paralela poderá ter ramificações seriais, áreas do plano com operadores que não são executados em paralelo. A tarefa pai também é responsável por executar esses operadores seriais.
-  As solicitações seriais terão somente uma tarefa ativa em qualquer momento durante a execução.     
Existem tarefas em vários estados durante seu tempo de vida. Para saber mais sobre os estados de tarefas, confira [sys.dm_os_tasks](../relational-databases/system-dynamic-management-views/sys-dm-os-tasks-transact-sql.md). Tarefas em um estado SUSPENSO estão aguardando os recursos necessários para executar a tarefa a ser disponibilizada. Para obter mais informações sobre as tarefas de espera, confira [sys.dm_os_waiting_tasks](../relational-databases/system-dynamic-management-views/sys-dm-os-waiting-tasks-transact-sql.md).

Um [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] **thread de trabalho**, também conhecido como trabalho ou thread, é uma declaração lógica de um thread do sistema operacional. Ao executar **solicitações seriais**, o [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] gerará um trabalho para executar a tarefa ativa (1:1). Ao executar **solicitações paralelas** no [modo de linha](../relational-databases/query-processing-architecture-guide.md#execution-modes), o [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] atribuirá um trabalho para coordenar os trabalhos filho responsáveis por concluir as tarefas atribuídas a eles (também 1:1), chamado de **thread pai** (ou thread de coordenação). O thread pai tem uma tarefa pai associada a ele. O thread pai é o ponto de entrada da solicitação e existe mesmo antes que o mecanismo analise uma consulta. As principais responsabilidades do thread pai são: 
-  Coordenar um exame paralelo.
-  Iniciar trabalhos filhos paralelos.
-  Coletar linhas de threads paralelos e enviar ao cliente.
-  Executar agregações locais e globais.    

> [!NOTE]
> Se um plano de consulta tiver ramificações seriais e paralelas, uma das tarefas paralelas será responsável pela execução da ramificação serial. 

O número de threads de trabalho gerados para cada tarefa depende:
-   Se a solicitação foi qualificada para paralelismo, conforme determinado pelo Otimizador de Consulta.
-   Qual é o [DOP (grau de paralelismo)](../relational-databases/query-processing-architecture-guide.md#DOP) real disponível no sistema com base na carga atual. Isso pode ser diferente do DOP estimado, que se baseia na configuração do servidor para obter o MAXDOP (max degree of parallelism). Por exemplo, a configuração do servidor para MAXDOP pode ser 8, mas o DOP disponível no tempo de execução pode ser apenas 2, o que afeta o desempenho da consulta. 

> [!NOTE]
> O limite do **MAXDOP (grau máximo de paralelismo)** é definido por tarefa, não por solicitação. Isso significa que durante uma execução de consulta paralela, uma solicitação poderá gerar várias tarefas até o limite do MAXDOP, além disso cada tarefa usará um trabalho. Para saber mais sobre MAXDOP, confira [Definir a Opção de Configuração do Servidor de grau máximo de paralelismo](../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md).

Um **agendador**, também conhecido como Agendador SOS, gerencia threads de trabalho que exigem tempo de processamento para realizar trabalho em nome das tarefas. Cada agendador é mapeado para um CPU (processador individual). O tempo que um trabalho pode permanecer ativo em um agendador é chamado de quantum do sistema operacional, com um máximo de 4 ms. Depois que o tempo do quantum expirar, um trabalho dedica seu tempo para outros trabalhos que precisam acessar os recursos da CPU e altera seu estado. Essa cooperação entre os trabalhos para maximizar o acesso aos recursos da CPU é chamada de **agendamento cooperativo**, também conhecido como agendamento não preemptivo. Por sua vez, a alteração no estado de trabalho é propagada para a tarefa associada a esse trabalho e para a solicitação associada à tarefa. Para sabe mais sobre os estados de trabalho, confira [sys.dm_os_workers](../relational-databases/system-dynamic-management-views/sys-dm-os-workers-transact-sql.md). Para saber mais sobre agendadores, confira [sys.dm_os_schedulers ](../relational-databases/system-dynamic-management-views/sys-dm-os-schedulers-transact-sql.md). 

Em resumo, uma **solicitação** poderá gerar uma ou mais **tarefas** para concluir unidades de trabalho. Cada tarefa será atribuída a um **thread de trabalho** responsável pela conclusão da tarefa. Cada thread de trabalho deverá ter um agendamento (feito em um **agendador**) para obter uma execução ativa da tarefa. 

### <a name="scheduling-parallel-tasks"></a>Como agendar tarefas paralelas
Imagine um [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] configurado com um MaxDOP 8, bem como a afinidade da CPU configurada para 24 CPUs (agendadores) em nós NUMA 0 e 1. Os agendadores de 0 a 11 pertencerão ao nó NUMA 0, os agendadores de 12 a 23 pertencerão ao nó NUMA 1. Um aplicativo enviará a seguinte consulta (solicitação) para o [!INCLUDE[ssde_md](../includes/ssde_md.md)]:

```sql
SELECT h.SalesOrderID, h.OrderDate, h.DueDate, h.ShipDate
FROM Sales.SalesOrderHeaderBulk AS h 
INNER JOIN Sales.SalesOrderDetailBulk AS d ON h.SalesOrderID = d.SalesOrderID 
WHERE (h.OrderDate >= '2014-3-28 00:00:00');
```

> [!TIP]
> A consulta de exemplo poderá ser executada usando o banco de dados chamado [banco de dados de exemplo do AdventureWorks2016_EXT](../samples/adventureworks-install-configure.md). As tabelas `Sales.SalesOrderHeader` e `Sales.SalesOrderDetail` foram ampliadas 50 vezes e renomeadas como `Sales.SalesOrderHeaderBulk` e `Sales.SalesOrderDetailBulk`.

O plano de execução mostra uma [junção hash](../relational-databases/performance/joins.md#hash) entre duas tabelas e cada um dos operadores executados em paralelo, conforme indicado pelo círculo amarelo com duas setas. Cada operador do paralelismo será um branch diferente no plano. Portanto, há três ramificações no plano de execução abaixo. 

![Plano de consulta paralela](../relational-databases/media/schedule-parallel-query-plan.png)

> [!NOTE]
> Caso considere obter um plano de execução no formato de árvore, um **branch** será uma área do plano que agrupará um ou mais operadores entre operadores do paralelismo, também chamados de iteradores de troca. Para obter mais informações sobre operadores do plano, confira [Referência de operadores lógicos e físicos do plano de execução](../relational-databases/showplan-logical-and-physical-operators-reference.md). 

Embora haja três ramificações no plano de execução, somente duas poderão ser executadas simultaneamente e a qualquer momento durante este plano de execução:
1.  A ramificação em que um *Exame de índice clusterizado* é usado no `Sales.SalesOrderHeaderBulk` (entrada de build da junção) é executada sozinha.
2.  A ramificação em que um *Exame de Índice Clusterizado* é usado no `Sales.SalesOrderDetailBulk` (entrada de investigação da junção) executa simultaneamente com a ramificação em que o *Bitmap* foi criado e, atualmente, a *Correspondência de Hash* está sendo executada.

O plano de execução XML mostra que 16 threads de trabalho foram reservados e usados no nó NUMA 0:

```xml
<ThreadStat Branches="2" UsedThreads="16">
  <ThreadReservation NodeId="0" ReservedThreads="16" />
</ThreadStat>
```

A reserva de threads garante que o [!INCLUDE[ssde_md](../includes/ssde_md.md)] tenha threads de trabalho suficientes para realizar todas as tarefas que serão necessárias para a solicitação. Os threads podem ser reservados em vários nós NUMA ou em apenas um nó NUMA. A reserva de threads é feita no runtime antes do início da execução e depende do carregamento do agendador. O número de threads de trabalho reservados é genericamente derivado da fórmula ***ramificações simultâneas* * *DOP de runtime*** e exclui o thread de trabalho pai. Cada ramificação é limitada a um número de threads de trabalho igual a MaxDOP. Neste exemplo, há duas ramificações simultâneas e MaxDOP é definido como 8, portanto **2 * 8 = 16**.

Para referência, observe o plano de execução dinâmico das [Estatísticas de Consultas Dinâmicas](../relational-databases/performance/live-query-statistics.md), em que uma ramificação foi concluída e duas ramificações estão sendo executadas simultaneamente.

![Plano de consulta paralela dinâmica](../relational-databases/media/schedule-parallel-query-live-plan.png)

O [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] atribuirá um thread de trabalho para executar uma tarefa ativa (1:1) que poderá ser observada durante a execução da consulta ao consultar a DMV de [sys.dm_os_tasks](../relational-databases/system-dynamic-management-views/sys-dm-os-tasks-transact-sql.md), conforme mostrado no seguinte exemplo:

```sql
SELECT parent_task_address, task_address, 
       task_state, scheduler_id, worker_address
FROM sys.dm_os_tasks
WHERE session_id = <insert_session_id>
ORDER BY parent_task_address, scheduler_id;
```

> [!TIP]
> A coluna `parent_task_address` será sempre nula para a tarefa pai. 

> [!TIP]
> Em um [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] muito ocupado é possível ver várias tarefas ativas que estão acima do limite definido por threads reservados. Essas tarefas podem pertencer a uma ramificação que não está mais sendo usada, além disso elas estão em um estado transitório, aguardando a limpeza. 

[!INCLUDE[ssResult](../includes/ssresult-md.md)] Observe que há 17 tarefas ativas para as ramificações que atualmente estão em execução: 16 tarefas filho correspondentes aos threads reservados, além da tarefa pai ou da tarefa de coordenação.

|parent_task_address|task_address|task_state|scheduler_id|worker_address|
|--------|--------|--------|--------|--------|
|NULO|**0x000001EF4758ACA8**|SUSPENDED|3|0x000001EFE6CB6160|
|0x000001EF4758ACA8|0x000001EFE43F3468|SUSPENDED|0|0x000001EF6DB70160|
|0x000001EF4758ACA8|0x000001EEB243A4E8|SUSPENDED|0|0x000001EF6DB7A160|
|0x000001EF4758ACA8|0x000001EC86251468|SUSPENDED|5|0x000001EEC05E8160|
|0x000001EF4758ACA8|0x000001EFE3023468|SUSPENDED|5|0x000001EF6B46A160|
|0x000001EF4758ACA8|0x000001EFE3AF1468|SUSPENDED|6|0x000001EF6BD38160|
|0x000001EF4758ACA8|0x000001EFE4AFCCA8|SUSPENDED|6|0x000001EF6ACB4160|
|0x000001EF4758ACA8|0x000001EFDE043848|SUSPENDED|7|0x000001EEA18C2160|
|0x000001EF4758ACA8|0x000001EF69038108|SUSPENDED|7|0x000001EF6AEBA160|
|0x000001EF4758ACA8|0x000001EFCFDD8CA8|SUSPENDED|8|0x000001EFCB6F0160|
|0x000001EF4758ACA8|0x000001EFCFDD88C8|SUSPENDED|8|0x000001EF6DC46160|
|0x000001EF4758ACA8|0x000001EFBCC54108|SUSPENDED|9|0x000001EFCB886160|
|0x000001EF4758ACA8|0x000001EC86279468|SUSPENDED|9|0x000001EF6DE08160|
|0x000001EF4758ACA8|0x000001EFDE901848|SUSPENDED|10|0x000001EFF56E0160|
|0x000001EF4758ACA8|0x000001EF6DB32108|SUSPENDED|10|0x000001EFCC3D0160|
|0x000001EF4758ACA8|0x000001EC8628D468|SUSPENDED|11|0x000001EFBFA4A160|
|0x000001EF4758ACA8|0x000001EFBD3A1C28|SUSPENDED|11|0x000001EF6BD72160|

Observe que cada uma das 16 tarefas filho tem um thread de trabalho diferente atribuído (visto na coluna `worker_address`), porém todos os trabalhos serão atribuídos ao mesmo pool de oito agendadores (0, 5, 6, 7, 8, 9, 10 e 11) e a tarefa pai será atribuída a um agendador fora desse pool (3).

> [!IMPORTANT]
> Depois que o primeiro conjunto de tarefas paralelas em uma determinada ramificação for agendado, o [!INCLUDE[ssde_md](../includes/ssde_md.md)] usará o mesmo pool de agendadores para todas as tarefas adicionais em outras ramificações. Isso significa que o mesmo conjunto de agendadores será usado para todas as tarefas paralelas em todo o plano de execução, limitado apenas por MaxDOP.  
> O [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] sempre tentará atribuir agendadores do mesmo nó NUMA para a execução da tarefa e os atribuirá sequencialmente (em modo Round Robin) se os agendadores estiverem disponíveis. No entanto, o thread de trabalho atribuído à tarefa pai poderá ser colocado em um nó NUMA diferente de outras tarefas.

Um thread de trabalho somente poderá permanecer ativo no agendador na duração do quantum (4 ms). Ele deverá suspender o agendador após a expiração do quantum para que um thread de trabalho atribuído a outra tarefa possa se tornar ativo. Quando o quantum de um trabalho expirar e não estiver mais ativo, a respectiva tarefa será colocada em uma fila PEPS em um estado RUNNABLE até que migre para um estado RUNNING novamente. Supondo que a tarefa não exija acesso a recursos que não estão disponíveis no momento, como uma trava ou um bloqueio, a tarefa seria colocada em um estado SUSPENDED em vez RUNNABLE até que esses recursos estejam disponíveis.  

> [!TIP] 
> Para a saída da DMV mostrada acima, todas as tarefas ativas estão no estado SUSPENDED. Mais detalhes sobre as tarefas de espera estão disponíveis ao consultar a DMV de [sys.dm_os_waiting_tasks](../relational-databases/system-dynamic-management-views/sys-dm-os-waiting-tasks-transact-sql.md). 

Em resumo, uma solicitação paralela gera várias tarefas. Cada tarefa deve ser atribuída a um só thread de trabalho. Cada thread de trabalho deve ser atribuído a um só agendador. Portanto, o número de agendadores em uso não pode ultrapassar o número de tarefas paralelas por branch, que é definido pela configuração de MaxDOP ou pela dica de consulta. O thread de coordenação não contribui para o limite de MaxDOP. 

### <a name="allocating-threads-to-a-cpu"></a>Como alocar threads a uma CPU
Por padrão, cada instância do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] inicia cada thread e o sistema operacional distribui threads de instâncias do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] entre os microprocessadores ou as CPUs (processadores) em um computador com base na carga. Se a afinidade do processo tiver sido habilitada no nível do sistema operacional, este atribuirá cada thread a uma CPU específica. Em contraste, o [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] atribui **threads de trabalho** do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] aos **agendadores** que distribuem os threads uniformemente entre as CPUs, em modo Round Robin.
    
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

A opção de configuração [aumento de prioridade](../database-engine/configure-windows/configure-the-priority-boost-server-configuration-option.md) pode ser usada para aumentar a prioridade dos threads de uma instância do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] para 13. Isso é conhecido como prioridade alta. Essa configuração fornece aos threads uma prioridade mais alta [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] do que a maioria dos outros aplicativos. Portanto, os threads do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] geralmente serão expedidos sempre que estiverem prontos para execução e não haverá preempção de threads de outros aplicativos. Isso pode melhorar o desempenho quando um servidor estiver executando apenas instâncias do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] e nenhum outro aplicativo. No entanto, caso uma operação com uso intensivo de memória ocorra no [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], outros aplicativos provavelmente não terão uma prioridade alta o suficiente para a preempção do thread [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. 

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
|Serviços de análise  |As.exe |Não |  
|Integration Services   |Is.exe |Não |  
|Agente de Serviço |Sb.exe |Não |  
|Pesquisa de Texto Completo   |Fts.exe    |Não |  
|SQL Server Agent   |Sqlagent.exe   |Não |  
|SQL Server Management Studio   |Ssms.exe   |Não |  
|instalação do SQL Server   |Setup.exe  |Não |  
