---
title: Reproduzir até um ponto de interrupção
titleSuffix: SQL Server Profiler
description: Facilite a depuração definindo pontos de interrupção, de modo que as repetições sejam pausadas em eventos específicos. Use o SQL Server Profiler para definir pontos de interrupção em um arquivo ou tabela de rastreamento.
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: profiler
ms.topic: conceptual
ms.assetid: 3caf751e-df3b-40c7-b5e8-4490ae178e0c
author: markingmyname
ms.author: maghan
ms.custom: seo-lt-2019
ms.date: 03/01/2017
ms.openlocfilehash: 5c8be9d32a60d44007d3e7c20b0b7da8fdb087c6
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85789904"
---
# <a name="replay-to-a-breakpoint-sql-server-profiler"></a>Repetir até um ponto de interrupção (SQL Server Profiler)

 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

Este tópico descreve como definir pontos de interrupção em um arquivo ou tabela de rastreamento que se deseja repetir, usando o [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]. Definir pontos de interrupção em um arquivo ou tabela de rastreamento antes de dar início à repetição do rastreamento permite que você pause a repetição em eventos específicos. Usar pontos de interrupção ao repetir um rastreamento dá suporte à depuração, pois é possível dividir a repetição de scripts de rastreamento longos em segmentos curtos que podem ser analisados incrementalmente.  
  
### <a name="to-replay-to-a-breakpoint"></a>Para repetir até um ponto de interrupção  
  
1.  Abra o arquivo ou tabela de rastreamento que deseja repetir. Para obter mais informações, consulte [Abrir um arquivo de rastreamento &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/open-a-trace-file-sql-server-profiler.md) ou do [Abrir uma tabela de rastreamento &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/open-a-trace-table-sql-server-profiler.md).  
  
     Certifique-se de que o arquivo ou tabela de rastreamento aberto contém as classes de evento necessárias para a repetição. Para obter mais informações, consulte [Replay Requirements](../../tools/sql-server-profiler/replay-requirements.md).  
  
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
  
## <a name="see-also"></a>Consulte Também  
 [Reproduzir para um cursor &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/replay-to-a-cursor-sql-server-profiler.md)   
 [Repetir rastreamentos](../../tools/sql-server-profiler/replay-traces.md)   
 [SQL Server Profiler](../../tools/sql-server-profiler/sql-server-profiler.md)  
  
  
