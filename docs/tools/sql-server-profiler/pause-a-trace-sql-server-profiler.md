---
title: "Pausar um rastreamento (SQL Server Profiler) | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "pausando rastreamentos"
  - "parando rastreamentos temporariamente"
  - "rastreamentos [SQL Server], pausando"
  - "parando rastreamentos"
ms.assetid: 432b9b0c-b5e7-47f3-a71b-310fb3bf2445
caps.latest.revision: 24
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 24
---
# Pausar um rastreamento (SQL Server Profiler)
  Pausar um rastreamento impede que mais dados de eventos sejam capturados até que o rastreamento seja reiniciado.  
  
 Pausando um rastreamento, você impede que sejam capturados dados de eventos até que o rastreamento seja reiniciado. Reiniciar um rastreamento permite que as operações de rastreamento sejam retomadas. Nenhum dado capturado anteriormente é perdido após o reinício. Quando o rastreamento é reiniciado, a captura de dados é retomada daquele ponto em diante. Enquanto um rastreamento está pausado, você pode alterar o nome, os eventos, as colunas e os filtros. Porém, você não pode alterar os destinos para os quais estão sendo enviados os dados de rastreamento, nem a conexão do servidor.  
  
### Para pausar um rastreamento  
  
1.  Selecione uma janela que contenha um rastreamento em execução.  
  
2.  No menu **Arquivo** , clique em **Pausar Rastreamento**.  
  
## Consulte também  
 [SQL Server Profiler](../../tools/sql-server-profiler/sql-server-profiler.md)  
  
  