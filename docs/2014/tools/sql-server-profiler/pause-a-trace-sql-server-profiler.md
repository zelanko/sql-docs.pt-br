---
title: Pausar um rastreamento (SQL Server Profiler) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- pausing traces
- temporarily stopping traces
- traces [SQL Server], pausing
- stopping traces
ms.assetid: 432b9b0c-b5e7-47f3-a71b-310fb3bf2445
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: d213e6b680bfe0d020a7c95b4e3924ef5679d7e2
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48077096"
---
# <a name="pause-a-trace-sql-server-profiler"></a>Pausar um rastreamento (SQL Server Profiler)
  Pausar um rastreamento impede que mais dados de eventos sejam capturados até que o rastreamento seja reiniciado.  
  
 Pausando um rastreamento, você impede que sejam capturados dados de eventos até que o rastreamento seja reiniciado. Reiniciar um rastreamento permite que as operações de rastreamento sejam retomadas. Nenhum dado capturado anteriormente é perdido após o reinício. Quando o rastreamento é reiniciado, a captura de dados é retomada daquele ponto em diante. Enquanto um rastreamento está pausado, você pode alterar o nome, os eventos, as colunas e os filtros. Porém, você não pode alterar os destinos para os quais estão sendo enviados os dados de rastreamento, nem a conexão do servidor.  
  
### <a name="to-pause-a-trace"></a>Para pausar um rastreamento  
  
1.  Selecione uma janela que contenha um rastreamento em execução.  
  
2.  No menu **Arquivo** , clique em **Pausar Rastreamento**.  
  
## <a name="see-also"></a>Consulte também  
 [SQL Server Profiler](sql-server-profiler.md)  
  
  
