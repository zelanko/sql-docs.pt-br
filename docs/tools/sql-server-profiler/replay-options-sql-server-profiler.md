---
title: "Opções de repetição (SQL Server Profiler) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: sql-server-profiler
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- traces [SQL Server], replaying
- replaying traces
- health monitor [SQL Server]
- Replay Configuration dialog box
ms.assetid: 58761a25-a84f-4a90-9c61-97700bc5ad9c
caps.latest.revision: "17"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: d207e1c930edc41b9270c7e1d34deacef9e08fa7
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/21/2017
---
# <a name="replay-options-sql-server-profiler"></a>Opções de repetição (SQL Server Profiler)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]Antes de repetir um rastreamento capturado com [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)], especificar opções de repetição no **configuração de repetição** caixa de diálogo. Para inicializar essa caixa de diálogo, abra o arquivo ou tabela de rastreamento a repetir no [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]e, no menu **Repetir** , clique em **Iniciar**. Para obter informações sobre quais permissões são necessárias para reproduzir um rastreamento, veja [Permissões necessárias para executar o SQL Server Profiler](../../tools/sql-server-profiler/permissions-required-to-run-sql-server-profiler.md).  
  
 Este tópico descreve as opções especificadas com a caixa de diálogo **Configuração de Repetição** .  
  
> [!NOTE]  
>  É recomendável usar o Distributed Replay Utility para reproduzir um aplicativo OLTP intensivo (com muitas conexões simultâneas ativas ou alta taxa de transferência). O Distributed Replay Utility pode reproduzir dados de rastreamento de vários computadores, com uma simulação melhor de uma carga de trabalho de missão crítica. Para obter mais informações, consulte [SQL Server Distributed Replay](../../tools/distributed-replay/sql-server-distributed-replay.md).  
  
## <a name="basic-replay-options"></a>Opções de repetição básicas  
 **Servidor de repetição**  
 O servidor é o nome da instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em relação ao qual se deseja repetir o rastreamento. O servidor deve cumprir os requisitos de repetição descritos em [Replay Requirements](../../tools/sql-server-profiler/replay-requirements.md)".  
  
 **Salvar no arquivo**  
 O arquivo de saída em que é gravado o resultado da repetição do rastreamento para posterior análise. Por padrão, o [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] exibe os resultados da repetição do rastreamento apenas na tela.  
  
 **Salvar na tabela**  
 O tabela de banco de dados em que é gravado o resultado da repetição do rastreamento para posterior análise.  
  
 **Número de threads de repetição**  
 Especifica o número de threads de repetição a usar simultaneamente. Um número mais alto consome mais recursos durante a repetição, porém ela é mais rápida. A ordenação de eventos não é completamente mantida quando são usados vários threads.  
  
 **Repetir eventos na ordem em que foram rastreados**  
 Permite-lhe usar métodos de depuração, como cada etapa de cada rastreamento. Se esta opção não estiver selecionada, a repetição não garantirá que os eventos sejam repetidos em uma ordem consistente com a que foram capturados originalmente.  
  
 **Repetir eventos usando vários threads**  
 Otimiza o desempenho e desabilita a depuração. Os eventos são repetidos na ordem em que foram registrados para uma ID de processo do servidor (SPID) específica, mas não se garante a ordem dos SPIDs.  
  
 **Exibir resultados da repetição**  
 Exibe os resultados da repetição. Essa é a opção padrão. Se o rastreamento que está sendo repetido for muito grande, pode ser conveniente desabilitar essa opção para economizar espaço em disco.  
  
> [!NOTE]  
>  Para um melhor desempenho da repetição, recomendamos selecionar eventos a repetir usando vários threads e não selecionar a exibição dos resultados da repetição.  
  
## <a name="advanced-replay-options"></a>Opções de repetição avançadas  
 **Repetir SPIDs do sistema**  
 Repetir todos os SPIDs. Essa é a opção padrão.  
  
 **Repetir somente um SPID**  
 Repetir o número de SPID selecionado na lista.  
  
 **Limitar repetição por data e hora**  
 Repete o rastreamento para a **Hora de início** e **Hora de término**especificadas.  
  
 **Intervalo de espera do Health Monitor**  
 Define o tempo de execução permitido a um processo até que o Health Monitor o encerre.  
  
 **Intervalo de sondagem do Health Monitor**  
 Define a frequência com que o Health Monitor sonda candidatos a encerramento.  
  
 **Habilitar monitor de processos bloqueados do SQL Server**  
 Define a frequência com que o monitor de processos bloqueados procura processos bloqueados ou que estejam causando bloqueios.  
  
## <a name="about-the-health-monitor"></a>Sobre o Health Monitor  
 O Health Monitor é um thread de aplicativo que monitora os processos simulados envolvidos na repetição de um rastreamento e encerra os processos que se encontram bloqueados na repetição. Na guia **Opções de Repetição Avançadas** da caixa de diálogo **Configuração de Repetição** , é possível especificar o tempo, em segundos, que o Health Monitor deve esperar antes de encerrar um processo bloqueado (**Intervalo de espera do Health Monitor**). Se você definir esse intervalo como 0, o Health Monitor nunca encerrará os processos que causam bloqueios no rastreamento de repetição.  
  
## <a name="see-also"></a>Consulte Também  
 [Repetir rastreamentos](../../tools/sql-server-profiler/replay-traces.md)   
 [Requisitos para repetição](../../tools/sql-server-profiler/replay-requirements.md)   
 [Considerações para reproduzir rastreamentos &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/considerations-for-replaying-traces-sql-server-profiler.md)  
  
  
