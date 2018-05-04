---
title: Repetir até um Cursor (SQL Server Profiler) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.suite: sql
ms.technology: profiler
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- replaying cursors
- traces [SQL Server], replaying
- replaying traces
ms.assetid: 89eadc41-4424-4a1c-ba61-0b52c851cdb1
caps.latest.revision: 22
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: ead2018ba30ca61703fe266ee3cbbe88129fa444
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MTE
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="replay-to-a-cursor-sql-server-profiler"></a>Repetir até um cursor (SQL Server Profiler)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Este tópico descreve como repetir arquivos ou tabelas de rastreamento e pausar quando um cursor for atingido, usando o [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]. Pausar rastreamentos mediante cursores dá suporte à depuração, pois é possível dividir a repetição de scripts de rastreamento longos em segmentos curtos que podem ser analisados incrementalmente.  
  
### <a name="to-replay-to-the-cursor"></a>Para repetir até o cursor  
  
1.  Abra o arquivo ou tabela de rastreamento que deseja repetir. Para obter mais informações, consulte [Abrir um arquivo de rastreamento &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/open-a-trace-file-sql-server-profiler.md) ou do [Abrir uma tabela de rastreamento &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/open-a-trace-table-sql-server-profiler.md).  
  
     Certifique-se de que o arquivo ou tabela de rastreamento aberto contém as classes de evento necessárias para a repetição. Para obter mais informações, consulte [Replay Requirements](../../tools/sql-server-profiler/replay-requirements.md).  
  
2.  Na janela do rastreamento, clique em um evento.  
  
3.  No menu **Reprodução** , clique em **Executar até Cursor**e conecte-se ao servidor em que deseja reproduzir o rastreamento.  
  
4.  Na caixa de diálogo **Configuração de Repetição** , verifique as definições e clique em **OK**.  
  
     A repetição é iniciada, sendo pausada quando o primeiro cursor é atingido.  
  
5.  Pressione F5 para retomar o rastreamento.  
  
6.  Repita a Etapa 5 até o término do rastreamento.  
  
## <a name="see-also"></a>Consulte Também  
 [Reproduzir em um ponto de interrupção &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/replay-to-a-breakpoint-sql-server-profiler.md)   
 [Repetir rastreamentos](../../tools/sql-server-profiler/replay-traces.md)   
 [SQL Server Profiler](../../tools/sql-server-profiler/sql-server-profiler.md)  
  
  
