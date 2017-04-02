---
title: "Criando c&#225;lculos de c&#233;lula em MDX (MDX) | Microsoft Docs"
ms.custom: ""
ms.date: "03/13/2017"
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
  - "células calculadas [MDX]"
  - "consultas [MDX], cálculos de célula"
  - "células [MDX]"
  - "MDX [Analysis Services], cálculos"
  - "subcubos de cálculo [MDX]"
  - "valores calculados [MDX]"
  - "Expressões MDX [Analysis Services], cálculos de célula"
ms.assetid: 068aea63-d419-4791-a960-3d74e76f808e
caps.latest.revision: 30
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
---
# Criando c&#225;lculos de c&#233;lula em MDX (MDX)
  As expressões multidimensionais (MDX) fornecem inúmeras ferramentas para a geração de valores calculados, como membros calculados, acúmulos personalizados e membros personalizados. No entanto, usar esses recursos para afetar um conjunto específico de células, ou uma única célula para esse fim, seria difícil.  
  
 Para valores calculados gerados especificamente para células, use o recurso de células calculadas em MDX. As células calculadas permitem a definição de uma porção de células específica, chamada *subcubo de cálculo*, e aplicam uma fórmula a todas as células do subcubo de cálculo, sujeita a um critério opcional que pode ser aplicado a cada célula.  
  
 Células calculadas também oferecem funcionalidades complexas, como fórmulas que visam metas, como as usadas em KPIs (indicadores chave de desempenho), ou fórmulas de análise especulativa. Esse nível de funcionalidade vem do recurso ordem de passagem do [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] que possibilita a realização de passagens recursivas com células calculadas, sendo as fórmulas de cálculo aplicadas a passagens específicas da ordem de passagem. Para obter mais informações sobre ordem de passagem, consulte [Entendendo a ordem de passagem e a ordem de resolução &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/understanding-pass-order-and-solve-order-mdx.md).  
  
 Em termos de escopo de criação, as células calculadas são similares a conjuntos nomeados e membros calculados no modo como as células calculas podem ser temporariamente criadas para o ciclo de vida de uma sessão ou de uma única consulta ou disponibilizadas globalmente como parte de um cubo:  
  
-   **Com escopo da consulta** Para criar uma célula calculada que seja definida como parte de uma consulta MDX e, portanto, cujo escopo esteja limitado à consulta, use a palavra-chave WITH. Você pode usar a célula calculada em uma instrução MDX SELECT. Usando essa abordagem, a célula calculada criada pelo uso da palavra-chave **WITH** pode ser alterada sem afetar a instrução SELECT.  
  
     Para obter mais informações sobre como usar a palavra-chave WITH para criar membros calculados, consulte [Criando cálculos de célula no escopo da consulta &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/creating-query-scoped-cell-calculations-mdx.md).  
  
-   **Com escopo da sessão** Para criar um membro calculado cujo escopo seja mais amplo que o contexto da consulta, ou seja, cujo escopo seja o tempo de vida da sessão MDX, use a instrução CREATE CELL CALCULATION ou ALTER CUBE.  
  
     Para obter mais informações sobre como usar a instrução CREATE CELL CALCULATION ou ALTER CUBE para criar células calculadas em uma sessão, consulte [Criando células calculadas no escopo da sessão](../../../analysis-services/multidimensional-models/mdx/creating-session-scoped-calculated-cells.md)  
  
## Consulte também  
 [Instrução ALTER CUBE &#40;MDX&#41;](../Topic/ALTER%20CUBE%20Statement%20\(MDX\).md)   
 [Instrução CREATE CELL CALCULATION &#40;MDX&#41;](../Topic/CREATE%20CELL%20CALCULATION%20Statement%20\(MDX\).md)   
 [Criando cálculos de célula no escopo da consulta &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/creating-query-scoped-cell-calculations-mdx.md)   
 [Conceitos básicos de consulta MDX &#40;Analysis Services&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-query-fundamentals-analysis-services.md)  
  
  