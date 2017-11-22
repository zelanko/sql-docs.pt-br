---
title: Filtrar IDs de processo do servidor (SPIDs) em um rastreamento (SQL Server Profiler) | Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- filters [SQL Server], traces
- filters [SQL Server], SPIDs
- traces [SQL Server], filters
ms.assetid: f5945c39-be6b-4632-91cb-92066c80e188
caps.latest.revision: "25"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 6bc5b5a3650b2d5eb646b34ad501d7d911799549
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2017
---
# <a name="filter-server-process-ids-spids-in-a-trace-sql-server-profiler"></a>Filtrar IDs de processo de servidor em um rastreamento (SQL Server Profiler)
  Este tópico descreve como filtrar identificadores de processo de servidor (SPIDs) em um rastreamento, usando o [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)].  
  
### <a name="to-filter-system-ids-in-a-trace"></a>Para filtrar IDs de sistema em um rastreamento  
  
1.  No menu **Arquivo** , clique em **Novo Rastreamento**e conecte a uma instância do SQL Server.  
  
     A caixa de diálogo **Propriedades do Rastreamento**é exibida.  
  
    > [!NOTE]  
    >  Se a opção **Iniciar rastreamento imediatamente após estabelecer a conexão**estiver marcada, a caixa de diálogo **Propriedades do Rastreamento**não será exibida e o rastreamento será iniciado. Para desabilitar essa configuração, no menu **Ferramentas**, clique em **Opções**e desmarque a caixa de seleção **Iniciar rastreamento imediatamente após estabelecer a conexão** .  
  
2.  Na caixa **Nome do rastreamento** , digite um nome para o rastreamento.  
  
3.  Na lista de nomes **Usar o modelo**, selecione um modelo de rastreamento.  
  
4.  Opcionalmente, especifique um arquivo ou tabela de destino onde os resultados do rastreamento serão salvos.  
  
5.  Na guia **Seleção de Eventos**, clique no título da coluna **SPID**para iniciar a caixa de diálogo **Editar Filtro** . Você também pode clicar com o botão direito do mouse no título de coluna e selecionar **Editar Filtro de Coluna**. Se a coluna **SPID** não aparecer, marque a caixa **Mostrar todas as colunas** .  
  
6.  Na caixa de diálogo **Editar Filtro** , expanda o operador de comparação apropriado e insira um SPID como valor de comparação.  
  
## <a name="see-also"></a>Consulte também  
 [SQL Server Profiler](../../tools/sql-server-profiler/sql-server-profiler.md)  
  
  
