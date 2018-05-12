---
title: Criando cálculos de célula em MDX (MDX) | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: e2263ac667b65def1bd59745e3cfef711820b494
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/10/2018
---
# <a name="mdx-cell-calculations---build-cell-calculations"></a>Cálculos de célula MDX - cálculos de célula de compilação
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  As expressões multidimensionais (MDX) fornecem inúmeras ferramentas para a geração de valores calculados, como membros calculados, acúmulos personalizados e membros personalizados. No entanto, usar esses recursos para afetar um conjunto específico de células, ou uma única célula para esse fim, seria difícil.  
  
 Para valores calculados gerados especificamente para células, use o recurso de células calculadas em MDX. As células calculadas permitem a definição de uma porção de células específica, chamada *subcubo de cálculo*, e aplicam uma fórmula a todas as células do subcubo de cálculo, sujeita a um critério opcional que pode ser aplicado a cada célula.  
  
 Células calculadas também oferecem funcionalidades complexas, como fórmulas que visam metas, como as usadas em KPIs (indicadores chave de desempenho), ou fórmulas de análise especulativa. Esse nível de funcionalidade vem do recurso ordem de passagem do [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] que possibilita a realização de passagens recursivas com células calculadas, sendo as fórmulas de cálculo aplicadas a passagens específicas da ordem de passagem. Para obter mais informações sobre ordem de passagem, consulte [Entendendo a ordem de passagem e a ordem de resolução &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-data-manipulation-understanding-pass-order-and-solve-order.md).  
  
 Em termos de escopo de criação, as células calculadas são similares a conjuntos nomeados e membros calculados no modo como as células calculas podem ser temporariamente criadas para o ciclo de vida de uma sessão ou de uma única consulta ou disponibilizadas globalmente como parte de um cubo:  
  
-   **Com escopo da consulta** Para criar uma célula calculada que seja definida como parte de uma consulta MDX e, portanto, cujo escopo esteja limitado à consulta, use a palavra-chave WITH. Você pode usar a célula calculada em uma instrução MDX SELECT. Usando essa abordagem, a célula calculada criada pelo uso da palavra-chave **WITH** pode ser alterada sem afetar a instrução SELECT.  
  
     Para obter mais informações sobre como usar a palavra-chave WITH para criar membros calculados, consulte [Criando cálculos de célula no escopo da consulta &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-cell-calculations-query-scoped-cell-calculations.md).  
  
-   **Com escopo da sessão** Para criar um membro calculado cujo escopo seja mais amplo que o contexto da consulta, ou seja, cujo escopo seja o tempo de vida da sessão MDX, use a instrução CREATE CELL CALCULATION ou ALTER CUBE.  
  
     Para obter mais informações sobre como usar a instrução CREATE CELL CALCULATION ou ALTER CUBE para criar células calculadas em uma sessão, consulte [Criando células calculadas no escopo da sessão](../../../analysis-services/multidimensional-models/mdx/mdx-cell-calculations-session-scoped-calculated-cells.md)  
  
## <a name="see-also"></a>Consulte também  
 [Instrução ALTER CUBE & #40; MDX & #41;](../../../mdx/mdx-data-definition-alter-cube.md)   
 [Criar instrução de CÁLCULO de CÉLULA & #40; MDX & #41;](../../../mdx/mdx-data-definition-create-cell-calculation.md)   
 [Criando cálculos de célula no escopo da consulta & #40; MDX & #41;](../../../analysis-services/multidimensional-models/mdx/mdx-cell-calculations-query-scoped-cell-calculations.md)   
 [Conceitos básicos de consulta MDX & #40; Analysis Services & #41;](../../../analysis-services/multidimensional-models/mdx/mdx-query-fundamentals-analysis-services.md)  
  
  
