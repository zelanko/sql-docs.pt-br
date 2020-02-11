---
title: Usando propriedades de membro (MDX) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- DIMENSION PROPERTIES keyword
- Properties function
- member properties [MDX]
- members [MDX], properties
ms.assetid: 26b5ad08-3799-4a5e-89f3-dca25e637d45
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 8c0326d45af68db966f120fa12e35eb59f30becc
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66074157"
---
# <a name="using-member-properties-mdx"></a>Usando propriedades do membro (MDX)
  As propriedades do membro incluem informações básicas sobre cada membro de cada tupla. Entre as informações básicas estão nome do membro, nível pai, número de filhos, e assim por diante. As propriedades do membro estão disponíveis para todos os membros de um determinado nível. Em termos de organização, elas são tratadas como dados organizados dimensionalmente, armazenados em uma única dimensão.  
  
> [!NOTE]  
>  No [!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], as propriedades do membro são conhecidas como relações de atributo. Para obter mais informações, consulte [Relações de atributos](../../multidimensional-models-olap-logical-dimension-objects/attribute-relationships.md).  
  
 As propriedades do membro são *intrínsecas* ou *personalizadas*:  
  
 Propriedades do membro intrínsecas  
 Todos os membros suportam propriedades intrínsecas, como o valor formatado de um membro, enquanto dimensões e níveis fornecem propriedades do membro da dimensão e do nível intrínsecas adicionais, como a identificação de um membro.  
  
 Para obter mais informações, consulte [Propriedades intrínsecas do membro &#40;MDX&#41;](mdx-member-properties-intrinsic-member-properties.md).  
  
 Propriedades do membro definidas pelo usuário  
 Com frequência, os membros possuem propriedades adicionais associadas a eles. Por exemplo, o nível Produtos pode oferecer as propriedades SKU, SRP, Importância e Volume para cada produto. Essas propriedades não são membros, mas contêm informações adicionais sobre os membros do nível Produtos.  
  
 Para obter mais informações, consulte [Propriedades do membro definidas pelo usuário &#40;MDX&#41;](mdx-member-properties-user-defined-member-properties.md).  
  
 As propriedades intrínsecas e definidas pelo usuário podem ser recuperadas por meio do uso `PROPERTIES` da palavra-chave ou da função [Properties](/sql/mdx/properties-mdx) .  
  
## <a name="using-the-properties-keyword"></a>Usando a palavra-chave PROPERTIES  
 A palavra-chave `PROPERTIES` especifica as propriedades do membro que serão usadas em uma determinada dimensão de eixo. A `PROPERTIES` palavra-chave é incluída `<axis specification>` na cláusula da instrução MDX [Select](/sql/mdx/mdx-data-manipulation-select) :  
  
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
>  Para obter mais informações sobre os valores `<set>` e `<axis_name>`, consulte [Especificando o conteúdo de um eixo de consulta &#40;MDX&#41;](mdx-query-and-slicer-axes-specify-the-contents-of-a-query-axis.md).  
  
 A cláusula `<dim_props>` permite a consulta de uma dimensão, de um nível e de propriedades do membro usando a palavra-chave `PROPERTIES`. A sintaxe a seguir mostra a formatação da cláusula `<dim_props>` :  
  
```  
<dim_props> ::= [DIMENSION] PROPERTIES <property> [,<property>...]  
```  
  
 A quebra da sintaxe `<property>` varia de acordo com a propriedade que você está consultando:  
  
-   Propriedades do membro intrínsecas sensíveis a contexto devem ser precedidas pelo nome da dimensão ou do nível. No entanto, propriedades do membro intrínsecas não sensíveis a contexto não podem ser qualificadas pelo nome da dimensão ou do nível. Para obter mais informações sobre como usar a `PROPERTIES` palavra-chave com propriedades intrínsecas do membro, consulte [propriedades intrínsecas do membro &#40;MDX&#41;](mdx-member-properties-intrinsic-member-properties.md).  
  
-   Propriedades do membro definidas pelo usuário devem ser precedidas pelo nome do nível no qual residem. Para obter mais informações sobre como usar a `PROPERTIES` palavra-chave com propriedades de membro definidas pelo usuário, consulte [Propriedades do membro definidas pelo usuário &#40;MDX&#41;](mdx-member-properties-user-defined-member-properties.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Criando e usando valores de propriedade &#40;MDX&#41;](../../creating-and-using-property-values-mdx.md)  
  
  
