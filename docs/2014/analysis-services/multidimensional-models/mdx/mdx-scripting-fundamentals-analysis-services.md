---
title: Conceitos básicos de script MDX (Analysis Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- cubes [Analysis Services], scripts
- calculations [Analysis Services], scripts
- MDX [Analysis Services], scripts
- scripts [MDX]
- cubes [Analysis Services], calculations
- Multidimensional Expressions [Analysis Services], scripts
ms.assetid: fdecb3ce-7c87-4bab-8000-532ba7a29f96
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 17cb2b326ed510a952249da6a73693b6be6ab252
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66073861"
---
# <a name="mdx-scripting-fundamentals-analysis-services"></a>Conceitos básicos de geração de scripts MDX (Analysis Services)
  No [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)], um script MDX é composto de uma ou mais linguagens ou instruções MDX que populam um cubo com cálculos.  
  
 Um script MDX define o processo de cálculo de um cubo. Um script MDX também é considerado parte do próprio cubo. Portanto, alterar um script MDX associado a um cubo altera imediatamente o processo de cálculo do cubo.  
  
 Para criar scripts MDX, você pode usar o Designer de Cubo no [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)]. Para obter mais informações, consulte [Definir atribuições e outros comandos de script](../define-assignments-and-other-script-commands.md) e [Introdução ao script MDX no Microsoft SQL Server 2005](https://go.microsoft.com/fwlink/?LinkId=81892).  
  
 Para questões de desempenho relacionadas a cálculos e consultas MDX, consulte a seção de otimização de MDX no [Guia de Desempenho do SQL Server Analysis Services](https://go.microsoft.com/fwlink/p/?LinkId=399050).  
  
## <a name="in-this-section"></a>Nesta seção  
  
|Tópico|DESCRIÇÃO|  
|-----------|-----------------|  
|[O script MDX básico &#40;MDX&#41;](the-basic-mdx-script-mdx.md)|Detalhes sobre o script MDX básico, inclusive o script MDX padrão fornecido em cada cubo, e como os scripts MDX geralmente funcionam dentro de um cubo no [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].|  
|[Gerenciando escopo e contexto &#40;MDX&#41;](managing-scope-and-context-mdx.md)|Descreve como usar a instrução [CALCULATE](/sql/mdx/mdx-scripting-calculate) , a instrução [SCOPE](/sql/mdx/mdx-scripting-scope) e a função [This](/sql/mdx/this-mdx) para gerenciar contexto e escopo dentro de um script MDX.|  
|[Usando variáveis e parâmetros &#40;MDX&#41;](using-variables-and-parameters-mdx.md)|Descreve como utilizar variáveis e parâmetros em um script MDX.|  
|[Erro ao manipular &#40;MDX&#41;](error-handling-mdx.md)|Explica a manipulação de erros dentro de um script MDX.|  
|[&#41;MDX &#40;MDX com suporte](supported-mdx-mdx.md)|Fornece uma lista de operadores, instruções e funções MDX suportadas em um script MDX.|  
  
## <a name="see-also"></a>Consulte Também  
 [Referência de linguagem MDX &#40;&#41;MDX](/sql/mdx/mdx-language-reference-mdx)  
  
  
