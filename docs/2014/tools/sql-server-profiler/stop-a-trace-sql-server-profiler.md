---
title: Interromper um rastreamento (SQL Server Profiler) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- traces [SQL Server], stopping
- stopping traces
ms.assetid: 47c4f33d-63e0-4444-bec8-4c1c91f8e25c
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: b51fa35e63cd4c6445108136f62fde6e20515fce
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48204846"
---
# <a name="stop-a-trace-sql-server-profiler"></a>Interromper um rastreamento (SQL Server Profiler)
  Este tópico descreve como interromper um rastreamento que está sendo executado, usando o [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)].  
  
 Interromper um rastreamento impede que os dados sejam capturados. Depois que um rastreamento é interrompido, ele não pode ser reiniciado sem a perda dos dados já capturados, a menos que eles se encontrem em um arquivo ou tabela de rastreamento. Você também pode salvar os dados coletados em uma tabela ou arquivo após interromper o rastreamento. Todas as propriedades de rastreamento selecionadas anteriormente são preservadas quando um rastreamento é interrompido. Quando um rastreamento é interrompido, você pode alterar o nome, os eventos, as colunas e os filtros.  
  
### <a name="to-stop-a-trace"></a>Para interromper um rastreamento  
  
1.  Selecione um rastreamento que esteja sendo executado.  
  
2.  No menu **Arquivo** , clique em **Parar Rastreamento**.  
  
## <a name="see-also"></a>Consulte também  
 [SQL Server Profiler](sql-server-profiler.md)  
  
  
