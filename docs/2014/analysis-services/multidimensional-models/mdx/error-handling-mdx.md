---
title: Tratamento de erro (MDX) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- scripts [MDX], exceptions
- exceptions [MDX]
ms.assetid: bc6ff0af-9fe6-44d6-bc3c-801d71ea41a9
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 611e7636f9a5cd6393da4a8412b6c02bcc9ddaf8
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66074675"
---
# <a name="error-handling-mdx"></a>Tratamento de erros (MDX)
  Cada cubo pode controlar como são tratados os erros em um script MDX. O tratamento de erro é feito pelo enumerador `ScriptErrorHandlingMode`. Os valores possíveis para esse enumerador são:  
  
 `IgnoreNone`  
 Faz com que o servidor gere um erro [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] quando encontra qualquer erro no script MDX.  
  
 `IgnoreAll`  
 Faz com que o servidor ignore todos os comandos do script MDX que contém um erro, incluindo erros de sintaxe, de resolução de nomes, entre outros.  
  
## <a name="see-also"></a>Consulte Também  
 <xref:Microsoft.AnalysisServices.Cube.ScriptErrorHandlingMode%2A>  
  
  
