---
title: "Filtrar eventos com base na hora de in&#237;cio do evento (SQL Server Profiler) | Microsoft Docs"
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
  - "horas de início de eventos [SQL Server]"
  - "filtros [SQL Server], rastreamentos"
  - "rastreamentos [SQL Server], filtros"
  - "rastreamentos [SQL Server], eventos"
ms.assetid: e965579e-d006-41a3-89ec-cfd5398c67d2
caps.latest.revision: 25
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 25
---
# Filtrar eventos com base na hora de in&#237;cio do evento (SQL Server Profiler)
  Este tópico descreve como filtrar eventos de rastreamento de acordo com a hora de início do evento, usando o [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)].  
  
### Para filtrar eventos com base na hora de início do evento  
  
1.  No menu **Arquivo**, clique em **Novo Rastreamento** e conecte-se a uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
     A caixa de diálogo **Propriedades do Rastreamento**é exibida.  
  
    > [!NOTE]  
    >  Se a opção **Iniciar rastreamento imediatamente após estabelecer a conexão** estiver marcada, a caixa de diálogo **Propriedades do Rastreamento** não será exibida e o rastreamento será iniciado. Para desabilitar essa configuração, no menu **Ferramentas**, clique em **Opções**e desmarque a caixa de seleção **Iniciar rastreamento imediatamente após estabelecer a conexão** .  
  
2.  Na caixa **Nome do rastreamento**, digite um nome para o rastreamento.  
  
3.  Na lista de nomes **Usar o modelo**, selecione um modelo de rastreamento.  
  
4.  Opcionalmente, especifique um destino para os resultados do rastreamento.  
  
5.  Na guia **Seleção de Eventos**, clique no título de coluna **StartTime**. Você também pode clicar com o botão direito do mouse no título de coluna e clicar em **Editar Filtro de Coluna** para iniciar a caixa de diálogo **Editar Filtro**.  
  
6.  Expanda **Maior que** ou **Menor que** e insira um valor **datetime** no campo que aparece abaixo do operador de comparação.  
  
## Consulte também  
 [SQL Server Profiler](../../tools/sql-server-profiler/sql-server-profiler.md)  
  
  