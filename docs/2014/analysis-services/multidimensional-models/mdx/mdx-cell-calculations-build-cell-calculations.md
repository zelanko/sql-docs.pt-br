---
title: Criando cálculos de célula em MDX (MDX) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- calculated cells [MDX]
- queries [MDX], cell calculations
- cells [MDX]
- MDX [Analysis Services], calculations
- calculation subcubes [MDX]
- calculated values [MDX]
- Multidimensional Expressions [Analysis Services], cell calculations
ms.assetid: 068aea63-d419-4791-a960-3d74e76f808e
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 2b1d0c01be4901e771278c82c4277c280aeb43ad
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66074514"
---
# <a name="building-cell-calculations-in-mdx-mdx"></a>Criando cálculos de célula em MDX (MDX)
  As expressões multidimensionais (MDX) fornecem inúmeras ferramentas para a geração de valores calculados, como membros calculados, acúmulos personalizados e membros personalizados. No entanto, usar esses recursos para afetar um conjunto específico de células, ou uma única célula para esse fim, seria difícil.  
  
 Para valores calculados gerados especificamente para células, use o recurso de células calculadas em MDX. As células calculadas permitem a definição de uma porção de células específica, chamada *subcubo de cálculo*, e aplicam uma fórmula a todas as células do subcubo de cálculo, sujeita a um critério opcional que pode ser aplicado a cada célula.  
  
 Células calculadas também oferecem funcionalidades complexas, como fórmulas que visam metas, como as usadas em KPIs (indicadores chave de desempenho), ou fórmulas de análise especulativa. Esse nível de funcionalidade é proveniente do recurso de pedido de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] passagem no que permite que passes recursivos sejam feitos com células calculadas, com fórmulas de cálculo aplicadas a passagens específicas na ordem de passagem. Para obter mais informações sobre ordem de passagem, consulte [Entendendo a ordem de passagem e a ordem de resolução &#40;MDX&#41;](mdx-data-manipulation-understanding-pass-order-and-solve-order.md).  
  
 Em termos de escopo de criação, as células calculadas são similares a conjuntos nomeados e membros calculados no modo como as células calculas podem ser temporariamente criadas para o ciclo de vida de uma sessão ou de uma única consulta ou disponibilizadas globalmente como parte de um cubo:  
  
-   **Com escopo de consulta** Para criar uma célula calculada que é definida como parte de uma consulta MDX e, portanto, cujo escopo é limitado à consulta, você usa a palavra-chave WITH. Você pode usar a célula calculada em uma instrução MDX SELECT. Usando essa abordagem, a célula calculada criada pelo uso da palavra-chave `WITH` pode ser alterada sem afetar a instrução SELECT.  
  
     Para obter mais informações sobre como usar a palavra-chave WITH para criar membros calculados, consulte [Criando cálculos de célula no escopo da consulta &#40;MDX&#41;](../../multidimensional-models-olap-logical-cube-objects/calculations.md).  
  
-   **Escopo da sessão** Para criar um membro calculado cujo escopo seja mais largo do que o contexto da consulta, ou seja, cujo escopo é o tempo de vida da sessão MDX, use a instrução CREATE CELL CALCULAtion ou ALTER CUBE.  
  
     Para obter mais informações sobre como usar a instrução CREATE CELL CALCULATION ou ALTER CUBE para criar células calculadas em uma sessão, consulte [Criando células calculadas no escopo da sessão](mdx-cell-calculations-session-scoped-calculated-cells.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Instrução ALTER CUBE &#40;MDX&#41;](/sql/mdx/mdx-data-definition-alter-cube)   
 [CRIAR instrução de cálculo de célula &#40;MDX&#41;](/sql/mdx/mdx-data-definition-create-cell-calculation)   
 [Criando cálculos de célula com escopo de consulta &#40;&#41;MDX](../../multidimensional-models-olap-logical-cube-objects/calculations.md)   
 [Conceitos básicos de consulta MDX &#40;Analysis Services&#41;](mdx-query-fundamentals-analysis-services.md)  
  
  
