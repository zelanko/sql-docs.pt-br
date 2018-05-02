---
title: Pausar um rastreamento (SQL Server Profiler) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: ''
ms.component: sql-server-profiler
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- pausing traces
- temporarily stopping traces
- traces [SQL Server], pausing
- stopping traces
ms.assetid: 432b9b0c-b5e7-47f3-a71b-310fb3bf2445
caps.latest.revision: 24
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: cbf301c5d846a42e1aed2571b60c0b88f638631b
ms.sourcegitcommit: b6116b434d737d661c09b78d0f798c652cf149f3
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/17/2018
---
# <a name="pause-a-trace-sql-server-profiler"></a>Pausar um rastreamento (SQL Server Profiler)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] Pausar um rastreamento impede que mais dados de eventos sejam capturados até que o rastreamento seja reiniciado.  
  
 Pausando um rastreamento, você impede que sejam capturados dados de eventos até que o rastreamento seja reiniciado. Reiniciar um rastreamento permite que as operações de rastreamento sejam retomadas. Nenhum dado capturado anteriormente é perdido após o reinício. Quando o rastreamento é reiniciado, a captura de dados é retomada daquele ponto em diante. Enquanto um rastreamento está pausado, você pode alterar o nome, os eventos, as colunas e os filtros. Porém, você não pode alterar os destinos para os quais estão sendo enviados os dados de rastreamento, nem a conexão do servidor.  
  
### <a name="to-pause-a-trace"></a>Para pausar um rastreamento  
  
1.  Selecione uma janela que contenha um rastreamento em execução.  
  
2.  No menu **Arquivo** , clique em **Pausar Rastreamento**.  
  
## <a name="see-also"></a>Consulte Também  
 [SQL Server Profiler](../../tools/sql-server-profiler/sql-server-profiler.md)  
  
  
