---
title: (MDX) de tratamento de erro | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- scripts [MDX], exceptions
- exceptions [MDX]
ms.assetid: bc6ff0af-9fe6-44d6-bc3c-801d71ea41a9
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 57b7320e8d09a3106d29a7f4c53c14a52afaadd7
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48187976"
---
# <a name="error-handling-mdx"></a>Tratamento de erros (MDX)
  Cada cubo pode controlar como são tratados os erros em um script MDX. Tratamento de erro é feito por meio de `ScriptErrorHandlingMode` enumerador. Os valores possíveis para esse enumerador são:  
  
 `IgnoreNone`  
 Faz com que o servidor produza um erro se o [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] localizar algum erro no script MDX.  
  
 `IgnoreAll`  
 Faz com que o servidor ignore todos os comandos do script MDX que contém um erro, incluindo erros de sintaxe, de resolução de nomes, entre outros.  
  
## <a name="see-also"></a>Consulte também  
 <xref:Microsoft.AnalysisServices.Cube.ScriptErrorHandlingMode%2A>  
  
  
