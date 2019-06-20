---
title: Repetir até um ponto de interrupção (SQL Server Profiler) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: profiler
ms.topic: conceptual
helpviewer_keywords:
- breakpoints [SQL Server]
- traces [SQL Server], replaying
ms.assetid: 3caf751e-df3b-40c7-b5e8-4490ae178e0c
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 33860d4e84e828b404236527dbe3c8c8cf6becc2
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63183507"
---
# <a name="replay-to-a-breakpoint-sql-server-profiler"></a>Repetir até um ponto de interrupção (SQL Server Profiler)
  Este tópico descreve como definir pontos de interrupção em um arquivo ou tabela de rastreamento que se deseja repetir, usando o [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]. Definir pontos de interrupção em um arquivo ou tabela de rastreamento antes de dar início à repetição do rastreamento permite que você pause a repetição em eventos específicos. Usar pontos de interrupção ao repetir um rastreamento dá suporte à depuração, pois é possível dividir a repetição de scripts de rastreamento longos em segmentos curtos que podem ser analisados incrementalmente.  
  
### <a name="to-replay-to-a-breakpoint"></a>Para repetir até um ponto de interrupção  
  
1.  Abra o arquivo ou tabela de rastreamento que deseja repetir. Para obter mais informações, consulte [Abrir um arquivo de rastreamento &#40;SQL Server Profiler&#41;](open-a-trace-file-sql-server-profiler.md) ou do [Abrir uma tabela de rastreamento &#40;SQL Server Profiler&#41;](open-a-trace-table-sql-server-profiler.md).  
  
     Certifique-se de que o arquivo ou tabela de rastreamento aberto contém as classes de evento necessárias para a repetição. Para obter mais informações, consulte [Replay Requirements](replay-requirements.md).  
  
2.  Na janela de rastreamento, clique em um evento que você deseje usar como ponto de interrupção. Use um destes três métodos para definir um ponto de interrupção:  
  
    -   Pressione F9.  
  
    -   No menu **Repetir** , clique em **Alternar Ponto de Interrupção**.  
  
    -   Clique com o botão direito do mouse no evento e clique em **Alternar Ponto de Interrupção**.  
  
     Um marcador vermelho aparecerá próximo ao evento de rastreamento selecionado, indicando que se trata de um ponto de interrupção do rastreamento.  
  
     Repita essa etapa para definir vários pontos de interrupção.  
  
3.  No menu **Repetir** , clique em **Iniciar**e conecte-se ao servidor em que deseja repetir o rastreamento.  
  
4.  Na caixa de diálogo **Configuração de Repetição** , verifique as definições e clique em **OK**.  
  
     A repetição tem início, sendo pausada quando o ponto de interrupção é alcançado.  
  
5.  Pressione F5 para retomar a repetição e prosseguir até o próximo ponto de interrupção.  
  
6.  Repita a Etapa 5 até o término do rastreamento.  
  
## <a name="see-also"></a>Consulte também  
 [Reproduzir para um cursor &#40;SQL Server Profiler&#41;](replay-to-a-cursor-sql-server-profiler.md)   
 [Repetir rastreamentos](replay-traces.md)   
 [SQL Server Profiler](sql-server-profiler.md)  
  
  
