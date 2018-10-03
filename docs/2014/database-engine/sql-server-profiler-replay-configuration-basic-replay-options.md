---
title: SQL Server Profiler - configuração de repetição (opções de repetição básicas) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
f1_keywords:
- sql12.pro.replay.generaloptions.f1
helpviewer_keywords:
- Replay Configuration dialog box
ms.assetid: 85a1dec6-9bbc-477a-86c5-b463db9ebb31
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 379cb1ab2ed12ad8d5d835068bb68008fd6ca9af
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48088296"
---
# <a name="sql-server-profiler---replay-configuration-basic-replay-options"></a>SQL Server Profiler – Configuração de repetição (Opções de repetição básicas)
  Na caixa de diálogo **Configuração de Repetição** , use a página **Opções de Repetição Básicas** para especificar como repetir um arquivo ou tabela de rastreamento.  
  
 Para exibir essa janela, use o [!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)] para abrir um arquivo ou tabela de rastreamento que contenha os eventos adequados para repetição. Para obter mais informações, consulte [Replay Requirements](../tools/sql-server-profiler/replay-requirements.md). Enquanto o arquivo ou tabela de rastreamento está aberto, no menu **Repetição** , clique em **Iniciar**e, então, conecte à instância do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] onde deseja repetir o rastreamento.  
  
## <a name="options"></a>Opções  
 **Servidor de repetição**  
 Exibe a instância do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] para conectar para a repetição.  
  
 **Alterar...**  
 Inicia a caixa de diálogo **Conectar ao Servidor** para conectar a outro servidor.  
  
 **Salvar no arquivo**  
 Salva os resultados da repetição para um arquivo. [!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)] Exibe a caixa de diálogo de arquivo padrão, onde você pode especificar o local para salvar o arquivo.  
  
 **Salvar na tabela**  
 Salva os resultados da repetição em uma tabela. O [!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)] exibe a caixa de diálogo de seleção da tabela, permitindo que se especifique o local para salvar a tabela.  
  
 **Número de threads de repetição**  
 Especifica o número de threads de repetição a usar simultaneamente. Um número maior consome mais recursos durante a repetição, porém esta será mais rápida e simultânea.  
  
 **Repetir eventos na ordem em que foram rastreados**  
 Repete os eventos sequencialmente. Use esta opção se você estiver repetindo um rastreamento para depuração.  
  
 **Reproduzir eventos usando vários threads**  
 Repete os eventos simultaneamente. Essa opção é mais rápida que repetir eventos sequencialmente, mas desabilita a depuração. Os eventos são ordenados dentro de seus identificadores de processo de sistema (SPID).  
  
 **Exibir resultados da repetição**  
 Exibe os resultados da repetição no [!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)].  
  
## <a name="see-also"></a>Consulte também  
 [Repetir uma tabela de rastreamento &#40;SQL Server Profiler&#41;](../tools/sql-server-profiler/replay-a-trace-table-sql-server-profiler.md)   
 [Reproduzir um arquivo de rastreamento &#40;SQL Server Profiler&#41;](../tools/sql-server-profiler/replay-a-trace-file-sql-server-profiler.md)   
 [Reproduzir rastreamentos](../tools/sql-server-profiler/replay-traces.md)  
  
  
