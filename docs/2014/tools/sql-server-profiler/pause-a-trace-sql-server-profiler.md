---
title: Pausar um rastreamento (SQL Server Profiler) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
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
caps.latest.revision: 23
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: e31b59bf2a71054f03982278b45e7b9e373f48e3
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36009255"
---
# <a name="pause-a-trace-sql-server-profiler"></a>Pausar um rastreamento (SQL Server Profiler)
  Pausar um rastreamento impede que mais dados de eventos sejam capturados até que o rastreamento seja reiniciado.  
  
 Pausando um rastreamento, você impede que sejam capturados dados de eventos até que o rastreamento seja reiniciado. Reiniciar um rastreamento permite que as operações de rastreamento sejam retomadas. Nenhum dado capturado anteriormente é perdido após o reinício. Quando o rastreamento é reiniciado, a captura de dados é retomada daquele ponto em diante. Enquanto um rastreamento está pausado, você pode alterar o nome, os eventos, as colunas e os filtros. Porém, você não pode alterar os destinos para os quais estão sendo enviados os dados de rastreamento, nem a conexão do servidor.  
  
### <a name="to-pause-a-trace"></a>Para pausar um rastreamento  
  
1.  Selecione uma janela que contenha um rastreamento em execução.  
  
2.  No menu **Arquivo** , clique em **Pausar Rastreamento**.  
  
## <a name="see-also"></a>Consulte também  
 [SQL Server Profiler](sql-server-profiler.md)  
  
  