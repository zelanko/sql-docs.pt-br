---
title: Consultando dados multidimensionais com MDX | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- multidimensional data [Analysis Services], querying
ms.assetid: e0a5dd60-35a3-4a4f-b36f-52ecea814886
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 6b04669080a9dedd84d3e7c218f6360486076fdc
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66073919"
---
# <a name="querying-multidimensional-data-with-mdx"></a>Consultando dados multidimensionais com MDX
  Expressões multidimensionais (MDX) é a linguagem de consulta que você usa para trabalhar com e recuperar dados multidimensionais [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]no. O MDX é baseado na especificação de XML for Analysis (XMLA), com extensões específicas [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]para o. O MDX utiliza expressões compostas de identificadores, valores, instruções, funções e operadores que o [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] pode avaliar para recuperar um objeto (por exemplo, um conjunto ou um membro) ou um valor escalar (por exemplo, uma cadeia de caracteres ou um número).  
  
 Consultas e expressões MDX no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] são usadas para fazer o seguinte:  
  
-   Retornar dados a um aplicativo cliente de um [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] cubo.  
  
-   Formatar resultados de consulta.  
  
-   Executar tarefas de design de cubo, incluindo a definição de membros calculados, conjuntos nomeados, tarefas de escopo e KPIs (indicadores chave de desempenho).  
  
-   Executar tarefas administrativas, incluindo dimensão e segurança da célula.  
  
 O MDX é superficialmente semelhante em muitas formas à sintaxe de SQL que normalmente é usada em bancos de dados relacionais. Porém, o MDX não é uma extensão da linguagem SQL e é diferente do SQL em muitas formas. Para criar expressões MDX usadas para desenhar ou proteger cubos, ou para criar consultas de MDX para retornar e formatar dados multidimensionais, você precisa entender os conceitos básicos de modelagem MDX e dimensional, elementos de sintaxe MDX, operadores MDX, instruções MDX e funções MDX.  
  
> [!NOTE]  
>  Para obter mais informações, consulte a seção recursos adicionais na página [SQL Server 2005-Analysis Services](https://go.microsoft.com/fwlink/?LinkId=80853) no site do Microsoft TechNet. Para obter mais informações sobre problemas de desempenho relacionados a cálculos e consultas MDX, consulte a seção "escrevendo MDX eficiente" no [Guia de desempenho do SQL Server 2005 Analysis Services](https://docsbay.net/Microsoft-SQL-Server-2005-Analysis-Services-Performance-Guide).  
  
## <a name="in-this-section"></a>Nesta seção  
  
|Tópico|DESCRIÇÃO|  
|-----------|-----------------|  
|[Conceitos principais em MDX &#40;Analysis Services&#41;](../key-concepts-in-mdx-analysis-services.md)|Você pode usar MDX (Multidimensional Expressions) para consultar dados multidimensionais ou para criar expressões MDX para uso em um cubo, mas primeiro você deve [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] entender os conceitos e a terminologia da dimensão.|  
|[Conceitos básicos de consulta MDX &#40;Analysis Services&#41;](mdx-query-fundamentals-analysis-services.md)|A linguagem MDX permite que você consulte objetos multidimensionais, como cubos, e retorna conjuntos de células multidimensionais que contêm dados do cubo. Este tópico e respectivos subtópicos fornecem uma visão geral das consultas MDX.|  
|[Conceitos básicos de script MDX &#40;Analysis Services&#41;](mdx-scripting-fundamentals-analysis-services.md)|No [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)], um script MDX é composto de uma ou mais expressões MDX ou instruções que preenchem um cubo com cálculos.<br /><br /> Um script MDX define o processo de cálculo de um cubo. Um script MDX também é considerado parte do próprio cubo. Portanto, alterar um script MDX associado a um cubo altera imediatamente o processo de cálculo do cubo.<br /><br /> Para criar scripts MDX, você pode usar o Designer de Cubo no [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)].|  
  
## <a name="see-also"></a>Consulte Também  
 [Elementos de sintaxe MDX &#40;&#41;MDX](/sql/mdx/mdx-syntax-elements-mdx)   
 [Referência de linguagem MDX &#40;&#41;MDX](/sql/mdx/mdx-language-reference-mdx)  
  
  
