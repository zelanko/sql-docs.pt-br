---
title: "Repetir até um Cursor (SQL Server Profiler) | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- replaying cursors
- traces [SQL Server], replaying
- replaying traces
ms.assetid: 89eadc41-4424-4a1c-ba61-0b52c851cdb1
caps.latest.revision: 22
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 775216d4634aced69ecc3248064b9539599fe54c
ms.contentlocale: pt-br
ms.lasthandoff: 08/02/2017

---
# <a name="replay-to-a-cursor-sql-server-profiler"></a>Repetir até um cursor (SQL Server Profiler)
  Este tópico descreve como repetir arquivos ou tabelas de rastreamento e pausar quando um cursor for atingido, usando o [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]. Pausar rastreamentos mediante cursores dá suporte à depuração, pois é possível dividir a repetição de scripts de rastreamento longos em segmentos curtos que podem ser analisados incrementalmente.  
  
### <a name="to-replay-to-the-cursor"></a>Para repetir até o cursor  
  
1.  Abra o arquivo ou tabela de rastreamento que deseja repetir. Para obter mais informações, consulte [Abrir um arquivo de rastreamento &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/open-a-trace-file-sql-server-profiler.md) ou [Abrir uma tabela de rastreamento &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/open-a-trace-table-sql-server-profiler.md).  
  
     Certifique-se de que o arquivo ou tabela de rastreamento aberto contém as classes de evento necessárias para a repetição. Para obter mais informações, consulte [Replay Requirements](../../tools/sql-server-profiler/replay-requirements.md).  
  
2.  Na janela do rastreamento, clique em um evento.  
  
3.  No menu **Reprodução** , clique em **Executar até Cursor**e conecte-se ao servidor em que deseja reproduzir o rastreamento.  
  
4.  Na caixa de diálogo **Configuração de Repetição** , verifique as definições e clique em **OK**.  
  
     A repetição é iniciada, sendo pausada quando o primeiro cursor é atingido.  
  
5.  Pressione F5 para retomar o rastreamento.  
  
6.  Repita a Etapa 5 até o término do rastreamento.  
  
## <a name="see-also"></a>Consulte também  
 [Repetir até um ponto de interrupção &#40; SQL Server Profiler &#41;](../../tools/sql-server-profiler/replay-to-a-breakpoint-sql-server-profiler.md)   
 [Repetir rastreamentos](../../tools/sql-server-profiler/replay-traces.md)   
 [SQL Server Profiler](../../tools/sql-server-profiler/sql-server-profiler.md)  
  
  

