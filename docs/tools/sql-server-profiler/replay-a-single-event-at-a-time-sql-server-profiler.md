---
title: Reproduzir um único evento de cada vez
titleSuffix: (SQL Server Profiler
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: profiler
ms.topic: conceptual
ms.assetid: 220fb192-9636-41a2-b15c-62af6cab8fff
author: markingmyname
ms.author: maghan
ms.custom: seo-lt-2019
ms.date: 03/01/2017
ms.openlocfilehash: e8f217e2117e22edbd5f763b71c51cb078d49301
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2020
ms.locfileid: "75307514"
---
# <a name="replay-a-single-event-at-a-time-sql-server-profiler"></a>Repetir um único evento de cada vez (SQL Server Profiler)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Este tópico descreve como repetir um evento de cada vez em um arquivo ou tabela de rastreamento de repetição usando o [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)].  
  
### <a name="to-replay-a-single-event-at-a-time"></a>Para repetir um único evento de cada vez  
  
1.  Abra o arquivo ou tabela de rastreamento que deseja repetir. Para obter mais informações, consulte [Abrir um arquivo de rastreamento &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/open-a-trace-file-sql-server-profiler.md) ou do [Abrir uma tabela de rastreamento &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/open-a-trace-table-sql-server-profiler.md).  
  
     Certifique-se de que o arquivo ou tabela de rastreamento aberto contém as classes de evento necessárias para a repetição. Para obter mais informações, consulte [Replay Requirements](../../tools/sql-server-profiler/replay-requirements.md).  
  
2.  No menu **Repetir** , clique em **Etapa**e conecte-se à instância de servidor em que deseja repetir o rastreamento.  
  
3.  Na caixa de diálogo **Configuração de Repetição** , verifique as definições e clique em **OK**. Para obter mais informações sobre como especificar configurações na caixa de diálogo **Configuração de Reprodução**, consulte [Repetir um arquivo de rastreamento &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/replay-a-trace-file-sql-server-profiler.md) ou [Repetir uma tabela de rastreamento &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/replay-a-trace-table-sql-server-profiler.md).  
  
4.  Para repetir o primeiro evento, clique em **OK** na caixa de diálogo **Configuração de Repetição** .  
  
5.  Para repetir eventos subsequentes, no menu **Repetir** , clique em **Etapa**ou pressione F10. Continue clicando em **Etapa** ou pressionando F10 para cada evento.  
  
## <a name="see-also"></a>Consulte Também  
 [Repetir rastreamentos](../../tools/sql-server-profiler/replay-traces.md)   
 [SQL Server Profiler](../../tools/sql-server-profiler/sql-server-profiler.md)  
  
  
