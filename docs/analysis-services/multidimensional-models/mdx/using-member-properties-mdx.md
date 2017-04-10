---
title: "Usando propriedades do membro (MDX) | Microsoft Docs"
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
  - "palavra-chave DIMENSION PROPERTIES"
  - "Função Properties"
  - "propriedades do membro [MDX]"
  - "membros [MDX], propriedades"
ms.assetid: 26b5ad08-3799-4a5e-89f3-dca25e637d45
caps.latest.revision: 29
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
---
# Usando propriedades do membro (MDX)
  As propriedades do membro incluem informações básicas sobre cada membro de cada tupla. Entre as informações básicas estão nome do membro, nível pai, número de filhos, e assim por diante. As propriedades do membro estão disponíveis para todos os membros de um determinado nível. Em termos de organização, elas são tratadas como dados organizados dimensionalmente, armazenados em uma única dimensão.  
  
> [!NOTE]  
>  No [!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], as propriedades do membro são conhecidas como relações de atributo. Para obter mais informações, consulte [Relações de atributos](../../../analysis-services/multidimensional-models-olap-logical-dimension-objects/attribute-relationships.md).  
  
 As propriedades do membro são *intrínsecas* ou *personalizadas*:  
  
 Propriedades do membro intrínsecas  
 Todos os membros suportam propriedades intrínsecas, como o valor formatado de um membro, enquanto dimensões e níveis fornecem propriedades do membro da dimensão e do nível intrínsecas adicionais, como a identificação de um membro.  
  
 Para obter mais informações, consulte [Propriedades intrínsecas do membro &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/intrinsic-member-properties-mdx.md).  
  
 Propriedades do membro definidas pelo usuário  
 Com frequência, os membros possuem propriedades adicionais associadas a eles. Por exemplo, o nível Produtos pode oferecer as propriedades SKU, SRP, Importância e Volume para cada produto. Essas propriedades não são membros, mas contêm informações adicionais sobre os membros do nível Produtos.  
  
 Para obter mais informações, consulte [Propriedades do membro definidas pelo usuário &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/user-defined-member-properties-mdx.md).  
  
 Tanto as propriedades do membro intrínsecas como as definidas pelo usuário podem ser recuperadas por meio da palavra-chave **PROPERTIES** ou da função [Propriedades](../../../mdx/properties-mdx.md).  
  
## Usando a palavra-chave PROPERTIES  
 A palavra-chave **PROPERTIES** especifica as propriedades do membro que serão usadas em uma determinada dimensão de eixo. A palavra-chave **PROPERTIES** é inserida na cláusula `<axis specification>` da instrução MDX [SELECT](../Topic/SELECT%20Statement%20\(MDX\).md) :  
  
```  
SELECT [<axis_specification>  
       [, <axis_specification>...]]  
  FROM [<cube_specification>]  
[WHERE [<slicer_specification>]]  
```  
  
 A cláusula `<axis_specification>` inclui uma cláusula `<dim_props>` opcional, como mostrada na sintaxe a seguir:  
  
```  
<axis_specification> ::= <set> [<dim_props>] ON <axis_name>  
```  
  
> [!NOTE]  
>  Para obter mais informações sobre os valores `<set>` e `<axis_name>`, consulte [Especificando o conteúdo de um eixo de consulta &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/specifying-the-contents-of-a-query-axis-mdx.md).  
  
 A palavra-chave `<dim_props>` permite a consulta de uma dimensão, de um nível e de propriedades do membro usando a palavra-chave **PROPERTIES** . A sintaxe a seguir mostra a formatação da cláusula `<dim_props>` :  
  
```  
<dim_props> ::= [DIMENSION] PROPERTIES <property> [,<property>...]  
```  
  
 A quebra da sintaxe `<property>` varia de acordo com a propriedade que você está consultando:  
  
-   Propriedades do membro intrínsecas sensíveis a contexto devem ser precedidas pelo nome da dimensão ou do nível. No entanto, propriedades do membro intrínsecas não sensíveis a contexto não podem ser qualificadas pelo nome da dimensão ou do nível. Para obter mais informações sobre como usar a palavra-chave **PROPERTIES** com propriedades intrínsecas do membro, consulte [Propriedades intrínsecas do membro &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/intrinsic-member-properties-mdx.md).  
  
-   Propriedades do membro definidas pelo usuário devem ser precedidas pelo nome do nível no qual residem. Para obter mais informações sobre como usar a palavra-chave **PROPERTIES** com propriedades do membro definidas pelo usuário, consulte [Propriedades do membro definidas pelo usuário &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/user-defined-member-properties-mdx.md).  
  
## Consulte também  
 [Criando e usando valores de propriedade &#40;MDX&#41;](../Topic/Creating%20and%20Using%20Property%20Values%20\(MDX\).md)  
  
  