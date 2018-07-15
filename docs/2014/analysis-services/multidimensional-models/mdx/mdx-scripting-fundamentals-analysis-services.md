---
title: Conceitos básicos (Analysis Services) de script MDX | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- cubes [Analysis Services], scripts
- calculations [Analysis Services], scripts
- MDX [Analysis Services], scripts
- scripts [MDX]
- cubes [Analysis Services], calculations
- Multidimensional Expressions [Analysis Services], scripts
ms.assetid: fdecb3ce-7c87-4bab-8000-532ba7a29f96
caps.latest.revision: 33
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 01f105ab8cd05029ac4dc7d747f5b0c016745962
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37325186"
---
# <a name="mdx-scripting-fundamentals-analysis-services"></a>Conceitos básicos de geração de scripts MDX (Analysis Services)
  No [!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)][!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)], um script MDX é composto de uma ou mais linguagens ou instruções MDX que populam um cubo com cálculos.  
  
 Um script MDX define o processo de cálculo de um cubo. Um script MDX também é considerado parte do próprio cubo. Portanto, alterar um script MDX associado a um cubo altera imediatamente o processo de cálculo do cubo.  
  
 Para criar scripts MDX, você pode usar o Designer de Cubo no [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)]. Para obter mais informações, consulte [Definir atribuições e outros comandos de script](../define-assignments-and-other-script-commands.md) e [Introdução ao script MDX no Microsoft SQL Server 2005](http://go.microsoft.com/fwlink/?LinkId=81892).  
  
 Para questões de desempenho relacionadas a cálculos e consultas MDX, consulte a seção de otimização de MDX no [Guia de Desempenho do SQL Server Analysis Services](http://go.microsoft.com/fwlink/p/?LinkId=399050).  
  
## <a name="in-this-section"></a>Nesta seção  
  
|Tópico|Description|  
|-----------|-----------------|  
|[O Script básico MDX &#40;MDX&#41;](the-basic-mdx-script-mdx.md)|Detalhes sobre o script MDX básico, inclusive o script MDX padrão fornecido em cada cubo, e como os scripts MDX geralmente funcionam dentro de um cubo no [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].|  
|[Gerenciando escopo e contexto &#40;MDX&#41;](managing-scope-and-context-mdx.md)|Descreve como usar a instrução [CALCULATE](/sql/mdx/mdx-scripting-calculate), a instrução [SCOPE](/sql/mdx/mdx-scripting-scope) e a função [This](/sql/mdx/this-mdx) para gerenciar contexto e escopo dentro de um script MDX.|  
|[Usando variáveis e parâmetros &#40;MDX&#41;](using-variables-and-parameters-mdx.md)|Descreve como utilizar variáveis e parâmetros em um script MDX.|  
|[Tratamento de erros &#40;MDX&#41;](error-handling-mdx.md)|Explica a manipulação de erros dentro de um script MDX.|  
|[Suporte para MDX &#40;MDX&#41;](supported-mdx-mdx.md)|Fornece uma lista de operadores, instruções e funções MDX suportadas em um script MDX.|  
  
## <a name="see-also"></a>Consulte também  
 [Referência da linguagem MDX &#40;MDX&#41;](/sql/mdx/mdx-language-reference-mdx)  
  
  
