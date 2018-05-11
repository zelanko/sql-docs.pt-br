---
title: Consultando dados multidimensionais com MDX | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: mdx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: d83c450ce2b7e2ecc78c0702718546135d2ca636
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/10/2018
---
# <a name="querying-multidimensional-data-with-mdx"></a>Consultando dados multidimensionais com MDX
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  MDX (linguagem MDX) é a linguagem de consulta usada para trabalhar com dados multidimensionais e recuperá-los no [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]. O MDX é baseado na especificação XMLA (XML for Analysis), com extensões específicas para [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]. O MDX utiliza expressões compostas de identificadores, valores, instruções, funções e operadores que o [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] pode avaliar para recuperar um objeto (por exemplo, um conjunto ou um membro) ou um valor escalar (por exemplo, uma cadeia de caracteres ou um número).  
  
 As consultas e expressões MDX no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] são usadas para fazer o seguinte:  
  
-   Retornar dados a um aplicativo cliente de um cubo do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] .  
  
-   Formatar resultados de consulta.  
  
-   Executar tarefas de design de cubo, incluindo a definição de membros calculados, conjuntos nomeados, tarefas de escopo e KPIs (indicadores chave de desempenho).  
  
-   Executar tarefas administrativas, incluindo dimensão e segurança da célula.  
  
 O MDX é superficialmente semelhante em muitas formas à sintaxe de SQL que normalmente é usada em bancos de dados relacionais. Porém, o MDX não é uma extensão da linguagem SQL e é diferente do SQL em muitas formas. Para criar expressões MDX usadas para desenhar ou proteger cubos, ou para criar consultas de MDX para retornar e formatar dados multidimensionais, você precisa entender os conceitos básicos de modelagem MDX e dimensional, elementos de sintaxe MDX, operadores MDX, instruções MDX e funções MDX.  
  
## <a name="in-this-section"></a>Nesta seção  
  
|Tópico|Description|  
|-----------|-----------------|  
|[Principais conceitos em MDX & #40; Analysis Services & #41;](../../../analysis-services/multidimensional-models/mdx/key-concepts-in-mdx-analysis-services.md)|Você pode usar a linguagem MDX para consultar dados multidimensionais ou criar expressões MDX para uso em um cubo, mas primeiro você deve entender os conceitos e a terminologia do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].|  
|[Conceitos básicos de consulta MDX & #40; Analysis Services & #41;](../../../analysis-services/multidimensional-models/mdx/mdx-query-fundamentals-analysis-services.md)|A linguagem MDX permite que você consulte objetos multidimensionais, como cubos, e retorna conjuntos de células multidimensionais que contêm dados do cubo. Este tópico e respectivos subtópicos fornecem uma visão geral das consultas MDX.|  
|[Conceitos básicos de script MDX & #40; Analysis Services & #41;](../../../analysis-services/multidimensional-models/mdx/mdx-scripting-fundamentals-analysis-services.md)|No [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)], um script MDX é composto de uma ou mais linguagens ou instruções MDX que populam um cubo com cálculos.<br /><br /> Um script MDX define o processo de cálculo de um cubo. Um script MDX também é considerado parte do próprio cubo. Portanto, alterar um script MDX associado a um cubo altera imediatamente o processo de cálculo do cubo.<br /><br /> Para criar scripts MDX, você pode usar o Designer de Cubo no [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)].|  
  
## <a name="see-also"></a>Consulte também  
 [Elementos de sintaxe MDX & #40; MDX & #41;](../../../mdx/mdx-syntax-elements-mdx.md)   
 [Referência de linguagem MDX & #40; MDX & #41;](../../../mdx/mdx-language-reference-mdx.md)  
  
  
