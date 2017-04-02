---
title: "Filtrar eventos com base na hora de t&#233;rmino do evento (SQL Server Profiler) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "horas de término de eventos [SQL Server]"
  - "filtros [SQL Server], rastreamentos"
  - "rastreamentos [SQL Server], filtros"
  - "rastreamentos [SQL Server], eventos"
ms.assetid: 74628f9e-2d39-496a-a443-0a3887db223d
caps.latest.revision: 27
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 27
---
# Filtrar eventos com base na hora de t&#233;rmino do evento (SQL Server Profiler)
  Este tópico descreve como filtrar eventos de rastreamento de acordo com a hora de término do evento, usando o [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)].  
  
### Para filtrar eventos com base na hora de término do evento  
  
1.  No menu **Arquivo**, clique em **Novo Rastreamento** e conecte-se a uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
     A caixa de diálogo **Propriedades do Rastreamento**é exibida.  
  
    > [!NOTE]  
    >  Se **Iniciar rastreamento imediatamente após estabelecer a conexão**estiver selecionado, a caixa de diálogo **Propriedades do Rastreamento**não será exibida e o rastreamento será iniciado. Para desabilitar essa configuração, no menu **Ferramentas**, clique em **Opções**e desmarque a caixa de seleção **Iniciar rastreamento imediatamente após estabelecer a conexão** .  
  
2.  Na caixa de diálogo **Propriedades do Rastreamento**, verifique se a guia **Geral** está marcada e insira um nome na caixa de texto **TraceName**.  
  
3.  Na lista **Usar o modelo**, selecione um modelo de rastreamento.  
  
4.  Opcionalmente, especifique um arquivo ou tabela de destino onde os resultados do rastreamento serão salvos.  
  
5.  Na guia **Seleção de Eventos**, clique na coluna de dados **EndTime** para iniciar a caixa de diálogo **Editar Filtro**. Você também pode clicar com o botão direito do mouse no título de coluna e selecionar **Editar Filtro de Coluna**.  
  
6.  Expanda **Maior que** ou **Menor que** e insira um valor **datetime** no campo que aparece abaixo do operador de comparação.  
  
## Consulte também  
 [SQL Server Profiler](../../tools/sql-server-profiler/sql-server-profiler.md)   
 [SQL Server Profiler](../../tools/sql-server-profiler/sql-server-profiler.md)  
  
  