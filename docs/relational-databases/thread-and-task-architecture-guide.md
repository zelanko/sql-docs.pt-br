---
title: Guia de arquitetura de thread e tarefa | Microsoft Docs
ms.custom: ''
ms.date: 11/13/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- guide, thread and task architecture
- thread and task architecture guide
ms.assetid: 925b42e0-c5ea-4829-8ece-a53c6cddad3b
author: rothja
ms.author: jroth
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 5dd4aa4c3beb769509884c6ebb75fd8c82c1c8ae
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68058134"
---
# <a name="thread-and-task-architecture-guide"></a>guia de arquitetura de threads e tarefas
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

Threads são um recurso do sistema operacional que permite a separação da lógica de aplicativo em vários caminhos de execução simultâneos. Esse recurso é útil quando aplicativos complexos têm muitas tarefas que podem ser executadas ao mesmo tempo. 

Quando um sistema operacional executa uma instância de um aplicativo, cria uma unidade denominada processo para gerenciar a instância. O processo tem um thread de execução. Tal processo é a série de instruções de programação executada pelo código de aplicativo. Por exemplo, se um aplicativo simples tiver um único conjunto de instruções que podem ser executadas em série, haverá apenas um caminho de execução ou thread no aplicativo. Aplicativos mais complexos podem ter várias tarefas que podem ser executadas em tandem, em vez de em série. O aplicativo pode fazer isso iniciando os processos separados para cada tarefa. Porém, a inicialização de um processo é uma operação de recurso intensivo. Em vez disso, um aplicativo pode iniciar threads separados. Eles têm recurso relativamente menos intensivo. Além disso, cada thread pode ser agendado para execução independentemente dos outros threads associados a um processo.

Os threads permitem aplicativos complexos para utilizar com mais eficácia uma CPU, mesmo em computadores com uma única CPU. Com uma CPU, apenas um thread pode ser executado de cada vez. Se um thread executar uma operação longa que não usa a CPU, como leitura ou gravação de disco, outro thread poderá ser executado até que a primeira operação seja concluída. Com a possibilidade de executar threads enquanto outros threads estão esperando pela conclusão de uma operação, o aplicativo consegue maximizar o uso da CPU. Isso é especialmente verdadeiro para aplicativos intensivos multiusuário e de E/S de disco, como um servidor de banco de dados. Os computadores que têm vários microprocessadores ou CPUs podem executar um thread por CPU ao mesmo tempo. Por exemplo, se um computador tiver oito CPUs, poderá executar oito threads ao mesmo tempo.

## <a name="sql-server-batch-or-task-scheduling"></a>Agendamento de tarefas ou lotes no SQL Server

### <a name="allocating-threads-to-a-cpu"></a>Alocando threads a uma CPU
Por padrão, cada instância do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] inicia cada thread e o sistema operacional distribui threads de instâncias do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] entre os microprocessadores ou as CPUs em um computador com base na carga. Se a afinidade do processo tiver sido habilitada no nível do sistema operacional, este atribuirá cada thread a uma CPU específica. Em contraste, o [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] atribui threads de trabalho [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] a agendadores que distribuem os threads de maneira uniforme entre os processadores (CPUs).
    
Para multitarefa, por exemplo quando vários aplicativos acessam o mesmo conjunto de processadores, às vezes, o sistema operacional move threads de processo entre diferentes processadores. Embora eficiente de um ponto de vista de sistema operacional, essa atividade pode reduzir o desempenho do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] sob cargas de sistema pesadas, à medida que cada cache de processador é recarregado repetidamente com dados. Atribuir processadores a threads específicos poderá melhorar o desempenho nessas condições eliminando recargas de processador e reduzindo a migração de thread entre processadores (reduzindo portanto a alternância de contexto); tal associação entre um thread e um processador é chamada de afinidade do processador. Se a afinidade foi habilitada, o sistema operacional atribuirá cada thread a uma CPU específica. 

A [opção de máscara de afinidade](../database-engine/configure-windows/affinity-mask-server-configuration-option.md) é definida usando [ALTER SERVER CONFIGURATION](../t-sql/statements/alter-server-configuration-transact-sql.md). Quando a máscara de afinidade não é definida, a instância de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] alocará threads de trabalho entre os agendadores sem máscaras especificadas.

> [!CAUTION]
> Não configure afinidade de CPU no sistema operacional e também configure a máscara de afinidade em [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Essas definições estão tentando alcançar o mesmo resultado e se as configurações forem inconsistentes, você poderá ter resultados imprevisíveis. Para saber mais, confira [opção de máscara de afinidade](../database-engine/configure-windows/affinity-mask-server-configuration-option.md).

O thread pooling ajuda a otimizar o desempenho quando são conectados grandes números de clientes ao servidor. Normalmente, é criado um thread de sistema operacional separado para cada solicitação de consulta. Porém, com centenas de conexões para o servidor, usam um thread por solicitação de consulta pode consumir quantias grandes de recursos do sistema. A [opção máximo de threads de trabalho](..//database-engine/configure-windows/configure-the-max-worker-threads-server-configuration-option.md) habilita o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] para criar um pool de threads de trabalho para atender a um número maior de solicitações de consulta, o que melhora o desempenho. 

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

## <a name="hot-add-cpu"></a>Inclusão de CPU a Quente
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
Não use as opções de configuração do servidor máscara affinity e máscara affinity64 para associar processadores a threads específicos. Essas opções são limitadas a 64 CPUs. Use a opção SET PROCESS AFFINITY de [ALTER SERVER CONFIGURATION](../t-sql/statements/alter-server-configuration-transact-sql.md) .

### <a name="managing-the-transaction-log-file-size"></a>Gerenciando o tamanho do arquivo de log de transações
Não confie no aumento automático para aumentar o tamanho do arquivo de log de transações. O aumento do log de transação deve ser um processo serial. A extensão do log pode impedir a continuação de operações de gravação de transação até que a extensão de log seja concluída. Em vez disso, pré-aloque espaço para os arquivos de log definindo o tamanho de arquivo para um valor grande o bastante para oferecer suporte à carga de trabalho comum no ambiente.

### <a name="setting-max-degree-of-parallelism-for-index-operations"></a>Definindo o grau máximo de paralelismo para operações de índice
O desempenho de operações de índice, como criar ou recompilar índices, pode ser melhorado em computadores com muitas CPUs definindo-se temporariamente o modelo de recuperação do banco de dados como bulk-logged ou simples. Essas operações de índice podem gerar atividade de log significativa, e a contenção de log pode afetar a melhor opção de DOP (grau de paralelismo) feita pelo [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].

Além disso, considere ajustar a configuração de servidor **MAXDOP (grau máximo de paralelismo)** para essas operações. As diretrizes a seguir se baseiam em testes internos e são recomendações gerais. Você deverá testar várias configurações de MAXDOP diferentes para determinar a configuração ideal para o seu ambiente.

* Para o modelo de recuperação completa, limite o valor do grau máximo da opção de paralelismo a oito ou menos.   
* Para o modelo bulk-logged ou simples, considere definir o valor da opção grau máximo de paralelismo como um valor maior que oito.   
* Para servidores que tenham o NUMA configurado, o grau máximo de paralelismo não deve exceder o número de CPUs atribuídas a cada nó NUMA. Isso ocorre porque é mais provável que a consulta use memória local de 1 nó NUMA, o que pode melhorar o tempo de acesso à memória.  
* Para os servidores que têm o hyperthreading habilitado e foram fabricados até 2009 (antes da melhoria do recurso de hyperthreading), o valor de MAXDOP não deve exceder o número de processadores físicos, em vez de processadores lógicos.

Para obter mais informações sobre o grau máximo da opção de paralelismo, veja [Configurar a opção grau máximo de paralelismo da configuração de servidor](../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md).

### <a name="setting-the-maximum-number-of-worker-threads"></a>Configurar o número máximo de threads de trabalho
Sempre defina o número máximo de threads de trabalho para ser superior à configuração do grau máximo de paralelismo. O número de threads de trabalho sempre deve ser definido como um valor de pelo menos sete vezes o número de CPUs presentes no servidor. Para saber mais, veja [Configurar a opção máx. de threads de trabalho](../database-engine/configure-windows/configure-the-max-worker-threads-server-configuration-option.md).

### <a name="using-sql-trace-and-sql-server-profiler"></a>Usando o Rastreamento do SQL e o SQL Server Profiler
É recomendável que você não use o Rastreamento do SQL e o SQL Profiler em um ambiente de produção. A sobrecarga para a execução dessas ferramentas também aumenta à medida que o número de CPUs cresce. Se você usar o Rastreamento do SQL em um ambiente de produção, limite o número de eventos de rastreamento a um nível mínimo. Crie perfis e teste cuidadosamente cada evento de rastreamento sob carga e evite usar combinações de eventos que afetem o desempenho de modo significativo.

### <a name="setting-the-number-of-tempdb-data-files"></a>Definindo o número de arquivos de dados tempdb
Em geral, o número de arquivos de dados tempdb deve corresponder ao número de CPUs. No entanto, ao considerar cuidadosamente as necessidades simultâneas de tempdb, você pode reduzir o gerenciamento do banco de dados. Por exemplo, se um sistema tiver 64 CPUs e geralmente apenas 32 consultas usam tempdb, o aumento do número de arquivos tempdb para 64 não melhorará o desempenho.

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
