---
title: SQL Server Profiler – limite de contadores de desempenho | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
f1_keywords:
- sql12.pro.performancecounterlimit.f1
helpviewer_keywords:
- Performance Counters List dialog box
ms.assetid: d10140ef-36c4-449c-b365-1cff1b2524e4
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: e64c5cc39ed8634ef2ec74f8680c84f7b66b98f1
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66088818"
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
  
  
