---
title: SQL Server Profiler – limite de contadores de desempenho | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql12.pro.performancecounterlimit.f1
helpviewer_keywords:
- Performance Counters List dialog box
ms.assetid: d10140ef-36c4-449c-b365-1cff1b2524e4
caps.latest.revision: 19
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 4d2265147cf660430e1995030354013a518e76a7
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37237216"
---
# <a name="sql-server-profiler---performance-counters-limit"></a>SQL Server Profiler – Limite de Contadores de Desempenho
  Use a caixa de diálogo Limite de Contadores de Desempenho para limitar as informações de um arquivo de log de desempenho do Monitor do Sistema ao correlacioná-lo com um rastreamento do [!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)] . Você pode usar essa caixa de diálogo para selecionar os contadores que devem ser exibidos e usados para a correlação.  
  
 A caixa de diálogo **Limite de Contadores de Desempenho** é populada com objetos e contadores de desempenho contidos no arquivo de log de desempenho.  
  
### <a name="to-select-performance-objects-and-counters-to-correlate-with-a-trace"></a>Para selecionar objetos e contadores de desempenho a correlacionar com um rastreamento  
  
1.  Expanda um objeto de desempenho para verificar quais contadores estão incluídos no arquivo de log de desempenho.  
  
2.  Verifique os contadores que você deseja correlacionar com o arquivo de rastreamento do [!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)] .  
  
     Para selecionar todos os contadores de um objeto de desempenho, marque a caixa adjacente ao objeto. Marcando o nó mais alto, que indica o computador, você seleciona todos os objetos e contadores de desempenho contidos no arquivo de log de desempenho.  
  
## <a name="see-also"></a>Consulte também  
 [Correlacionar um rastreamento com dados do log de desempenho do Windows &#40;SQL Server Profiler&#41;](../tools/sql-server-profiler/correlate-a-trace-with-windows-performance-log-data.md)  
  
  
