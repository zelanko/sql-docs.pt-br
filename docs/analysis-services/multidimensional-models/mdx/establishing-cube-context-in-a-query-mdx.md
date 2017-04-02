---
title: "Estabelecendo o contexto de cubo em uma consulta (MDX) | Microsoft Docs"
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
  - "cubos [Analysis Services], MDX"
  - "MDX [Analysis Services], contexto de cubo"
  - "Instrução SELECT [MDX]"
  - "Expressões multidimensionais [Analysis Services], contexto de cubo"
  - "consultas [MDX], contexto de cubo"
ms.assetid: 79d6a1e8-2825-4eb9-97df-5071aecae8f0
caps.latest.revision: 29
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 29
---
# Estabelecendo o contexto de cubo em uma consulta (MDX)
  Toda consulta MDX é executada em um contexto de cubo especificado. Esse contexto define os membros que são avaliados pelas expressões da consulta.  
  
 Na instrução SELECT, a cláusula FROM determina o contexto de cubo. Esse contexto pode ser o cubo inteiro ou apenas um subcubo dele. Ao especificar o contexto de cubo usando a cláusula FROM, você pode usar funções adicionais para expandir ou restringir esse contexto.  
  
> [!NOTE]  
>  As instruções SCOPE e CALCULATE também permitem administrar o contexto de cubo a partir de um script MDX. Para obter mais informações, consulte [Conceitos básicos do script MDX &#40;Analysis Services&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-scripting-fundamentals-analysis-services.md).  
  
## Sintaxe da cláusula FROM  
 A sintaxe a seguir descreve a cláusula FROM:  
  
```  
<SELECT subcube clause> ::=  
   Cube_Identifier |   
   (SELECT [  
      * |   
      ( <SELECT query axis clause> [ , <SELECT query axis clause> ... ] ) ]   
   FROM <SELECT subcube clause> <SELECT slicer axis clause> )  
```  
  
 Nessa sintaxe, observe que é a cláusula `<SELECT subcube clause>` que descreve o cubo ou o subcubo no qual a instrução SELECT é executada.  
  
 Um exemplo simples de uma cláusula FROM seria aquele executado no cubo inteiro de exemplo Adventure Works. Essa cláusula FROM teria o seguinte formato:  
  
```  
FROM [Adventure Works]  
```  
  
 Para obter mais informações sobre a cláusula FROM na instrução MDX SELECT, consulte [Instrução SELECT &#40;MDX&#41;](../Topic/SELECT%20Statement%20\(MDX\).md).  
  
## Refinando o contexto  
 Embora a cláusula FROM especifique o contexto de cubo como um único cubo, ela não impede que você trabalhe com os dados de mais de um cubo ao mesmo tempo.  
  
 Você pode usar a função MDX [LookupCube](../../../mdx/lookupcube-mdx.md) para recuperar dados de cubos fora do contexto de cubo. Além disso, funções, como a função [Filter](../../../mdx/filter-mdx.md) , estão disponíveis para permitir a restrição temporária do contexto durante a avaliação da consulta.  
  
## Consulte também  
 [Conceitos básicos de consulta MDX &#40;Analysis Services&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-query-fundamentals-analysis-services.md)  
  
  