---
title: Reproduzir um único evento de cada vez (SQL Server Profiler) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: profiler
ms.topic: conceptual
helpviewer_keywords:
- events [SQL Server], replaying single event at a time
- traces [SQL Server], replaying
- replaying traces
ms.assetid: 220fb192-9636-41a2-b15c-62af6cab8fff
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 9c36aafe3a01a48f7623fa1d2871428ee3bea390
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/03/2018
ms.locfileid: "52779288"
---
# <a name="replay-a-single-event-at-a-time-sql-server-profiler"></a>Repetir um único evento de cada vez (SQL Server Profiler)
  Este tópico descreve como repetir um evento de cada vez em um arquivo ou tabela de rastreamento de repetição usando o [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)].  
  
### <a name="to-replay-a-single-event-at-a-time"></a>Para repetir um único evento de cada vez  
  
1.  Abra o arquivo ou tabela de rastreamento que deseja repetir. Para obter mais informações, consulte [Abrir um arquivo de rastreamento &#40;SQL Server Profiler&#41;](open-a-trace-file-sql-server-profiler.md) ou do [Abrir uma tabela de rastreamento &#40;SQL Server Profiler&#41;](open-a-trace-table-sql-server-profiler.md).  
  
     Certifique-se de que o arquivo ou tabela de rastreamento aberto contém as classes de evento necessárias para a repetição. Para obter mais informações, consulte [Replay Requirements](replay-requirements.md).  
  
2.  No menu **Repetir** , clique em **Etapa**e conecte-se à instância de servidor em que deseja repetir o rastreamento.  
  
3.  Na caixa de diálogo **Configuração de Repetição** , verifique as definições e clique em **OK**. Para obter mais informações sobre como especificar configurações na caixa de diálogo **Configuração de Reprodução**, consulte [Repetir um arquivo de rastreamento &#40;SQL Server Profiler&#41;](replay-a-trace-file-sql-server-profiler.md) ou [Repetir uma tabela de rastreamento &#40;SQL Server Profiler&#41;](replay-a-trace-table-sql-server-profiler.md).  
  
4.  Para repetir o primeiro evento, clique em **OK** na caixa de diálogo **Configuração de Repetição** .  
  
5.  Para repetir eventos subsequentes, no menu **Repetir** , clique em **Etapa**ou pressione F10. Continue clicando em **Etapa** ou pressionando F10 para cada evento.  
  
## <a name="see-also"></a>Consulte também  
 [Repetir rastreamentos](replay-traces.md)   
 [SQL Server Profiler](sql-server-profiler.md)  
  
  
