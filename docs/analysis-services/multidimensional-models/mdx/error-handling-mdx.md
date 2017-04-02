---
title: "Tratamento de erros (MDX) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
  - "analysis-services/multidimensional-tabular"
  - "analysis-services/data-mining"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "scripts [MDX], exceções"
  - "exceções [MDX]"
ms.assetid: bc6ff0af-9fe6-44d6-bc3c-801d71ea41a9
caps.latest.revision: 26
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 26
---
# Tratamento de erros (MDX)
  Cada cubo pode controlar como são tratados os erros em um script MDX. O tratamento de erro é feito por meio do enumerador **ScriptErrorHandlingMode**. Os valores possíveis para esse enumerador são:  
  
 **IgnoreNone**  
 Faz com que o servidor produza um erro se o [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] localizar algum erro no script MDX.  
  
 **IgnoreAll**  
 Faz com que o servidor ignore todos os comandos do script MDX que contém um erro, incluindo erros de sintaxe, de resolução de nomes, entre outros.  
  
## Consulte também  
 <xref:Microsoft.AnalysisServices.Cube.ScriptErrorHandlingMode%2A>  
  
  