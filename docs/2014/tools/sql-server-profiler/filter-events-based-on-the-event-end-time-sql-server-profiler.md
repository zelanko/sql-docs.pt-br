---
title: Filtrar eventos com base na hora de término do evento (SQL Server Profiler) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: profiler
ms.topic: conceptual
helpviewer_keywords:
- event end times [SQL Server]
- filters [SQL Server], traces
- traces [SQL Server], filters
- traces [SQL Server], events
ms.assetid: 74628f9e-2d39-496a-a443-0a3887db223d
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 48f0ada8740735e64fe57c35bc17553f59aa444c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63184285"
---
# <a name="filter-events-based-on-the-event-end-time-sql-server-profiler"></a>Filtrar eventos com base na hora de término do evento (SQL Server Profiler)
  Este tópico descreve como filtrar eventos de rastreamento de acordo com a hora de término do evento, usando o [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)].  
  
### <a name="to-filter-events-based-on-the-event-end-time"></a>Para filtrar eventos com base na hora de término do evento  
  
1.  No menu **Arquivo** , clique em **Novo Rastreamento**e conecte-se a uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
     A caixa de diálogo **Propriedades do Rastreamento**é exibida.  
  
    > [!NOTE]  
    >  Se **Iniciar rastreamento imediatamente após estabelecer a conexão**estiver selecionado, a caixa de diálogo **Propriedades do Rastreamento**não será exibida e o rastreamento será iniciado. Para desabilitar essa configuração, no menu **Ferramentas**, clique em **Opções**e desmarque a caixa de seleção **Iniciar rastreamento imediatamente após estabelecer a conexão** .  
  
2.  Na caixa de diálogo **Propriedades do Rastreamento** , verifique se a guia **Geral** está marcada e insira um nome na caixa de texto **TraceName** .  
  
3.  Na lista **Usar o modelo**, selecione um modelo de rastreamento.  
  
4.  Opcionalmente, especifique um arquivo ou tabela de destino onde os resultados do rastreamento serão salvos.  
  
5.  Na guia **Seleção de Eventos**, clique na coluna de dados **EndTime** para iniciar a caixa de diálogo **Editar Filtro** . Você também pode clicar com o botão direito do mouse no título de coluna e selecionar **Editar Filtro de Coluna**.  
  
6.  Expandir **maior que** ou **menor que**e insira um `datetime`valor no campo que aparece abaixo do operador de comparação.  
  
## <a name="see-also"></a>Consulte também  
 [SQL Server Profiler](sql-server-profiler.md)   
 [SQL Server Profiler](sql-server-profiler.md)  
  
  
