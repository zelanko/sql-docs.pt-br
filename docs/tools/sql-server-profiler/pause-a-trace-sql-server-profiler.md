---
title: Pausar um rastreamento (SQL Server Profiler) | Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: 
ms.component: sql-server-profiler
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- pausing traces
- temporarily stopping traces
- traces [SQL Server], pausing
- stopping traces
ms.assetid: 432b9b0c-b5e7-47f3-a71b-310fb3bf2445
caps.latest.revision: "24"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 07c66a2907d0e0d6b75e413959256133156b67a6
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/05/2017
---
# <a name="pause-a-trace-sql-server-profiler"></a>Pausar um rastreamento (SQL Server Profiler)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]Pausar um rastreamento impede que mais dados de eventos sejam capturados até que o rastreamento seja reiniciado.  
  
 Pausando um rastreamento, você impede que sejam capturados dados de eventos até que o rastreamento seja reiniciado. Reiniciar um rastreamento permite que as operações de rastreamento sejam retomadas. Nenhum dado capturado anteriormente é perdido após o reinício. Quando o rastreamento é reiniciado, a captura de dados é retomada daquele ponto em diante. Enquanto um rastreamento está pausado, você pode alterar o nome, os eventos, as colunas e os filtros. Porém, você não pode alterar os destinos para os quais estão sendo enviados os dados de rastreamento, nem a conexão do servidor.  
  
### <a name="to-pause-a-trace"></a>Para pausar um rastreamento  
  
1.  Selecione uma janela que contenha um rastreamento em execução.  
  
2.  No menu **Arquivo** , clique em **Pausar Rastreamento**.  
  
## <a name="see-also"></a>Consulte também  
 [SQL Server Profiler](../../tools/sql-server-profiler/sql-server-profiler.md)  
  
  
