---
title: SQL Server Profiler-configuração de reprodução (opções de reprodução avançadas) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
f1_keywords:
- sql12.pro.replay.generaloptions.advanced.f1
helpviewer_keywords:
- Replay Configuration dialog box
ms.assetid: b4eb34f7-3af6-4a44-ba7e-2b8430ec3cd7
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: 78ca3fc2d11b22d70c8a4e99d0961f793870bd53
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84928511"
---
# <a name="sql-server-profiler---replay-configuration-advanced-replay-options"></a>SQL Server Profiler - configuração de repetição (Opções de Repetição Avançadas)
  Na caixa de diálogo **Configuração de Reprodução** , use a guia **Opções de Reprodução Avançadas** para especificar como reproduzir um arquivo de rastreamento.  
  
 Para exibir essa janela, use o [!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)] para abrir um arquivo ou tabela de rastreamento que contenha os eventos adequados para repetição. Para obter mais informações, consulte [Replay Requirements](../tools/sql-server-profiler/replay-requirements.md). Enquanto o arquivo ou tabela de rastreamento está aberto, no menu **Reprodução** , clique em **Iniciar**, conecte-se à instância do SQL Server em que você deseja reproduzir o rastreamento e clique na guia **Opções de Reprodução Avançadas** .  
  
## <a name="options"></a>Opções  
 **Repetir SPIDs do sistema**  
 Especifica se o [!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)] repete os identificadores de processos do sistema (SPIDs).  
  
 **Repetir somente um SPID**  
 Repete apenas a atividade no arquivo de rastreamento de origem que está relacionado ao SPID selecionado.  
  
 **SPID para repetir**  
 Especifica o SPID para repetir.  
  
 **Limitar repetição por data e hora**  
 Verifica para repetir apenas uma parte do arquivo de rastreamento de origem.  
  
 **Hora de início**  
 Data e hora no arquivo de rastreamento de origem em que a repetição deve iniciar.  
  
 **Hora de término**  
 Data e hora no arquivo de rastreamento de origem em que a repetição deve ser interrompida.  
  
 **Intervalo de espera do monitor de integridade (s)**  
 Especifica o intervalo de espera de repetição, em segundos. O padrão é 3600 segundos (1 hora). Essa configuração afeta o tempo durante o qual um processo pode ser executado antes de ser concluído pelo monitor de integridade.  
  
 **Intervalo de sondagem do monitor de integridade (s)**  
 Especifica o intervalo de sondagem do monitor de integridade durante a repetição, em segundos. O padrão é 60 segundos. Este valor permite que o usuário configure com que frequência o monitor de integridade sonda candidatos a conclusão.  
  
 **Habilitar monitor de processos bloqueados do SQL Server**  
 Habilita um processo que procura processos bloqueados ou em bloqueio.  
  
 **Intervalo de espera do monitor de processos bloqueados (s)**  
 Configura a frequência com que o monitor de processos bloqueados procura processos bloqueados ou em bloqueio.  
  
## <a name="see-also"></a>Consulte Também  
 [Reproduzir uma tabela de rastreamento &#40;SQL Server Profiler&#41;](../tools/sql-server-profiler/replay-a-trace-table-sql-server-profiler.md)   
 [Reproduzir um arquivo de rastreamento &#40;SQL Server Profiler&#41;](../tools/sql-server-profiler/replay-a-trace-file-sql-server-profiler.md)   
 [Reproduzir rastreamentos](../tools/sql-server-profiler/replay-traces.md)  
  
  
