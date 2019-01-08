---
title: Usando propriedades do membro (MDX) | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 7876031fddb74115fd1fe412f4c8a9d9aacdb054
ms.sourcegitcommit: 6443f9a281904af93f0f5b78760b1c68901b7b8d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/11/2018
ms.locfileid: "53216035"
---
# <a name="mdx-member-properties"></a>Propriedades de membro MDX
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  As propriedades do membro incluem informações básicas sobre cada membro de cada tupla. Entre as informações básicas estão nome do membro, nível pai, número de filhos, e assim por diante. As propriedades do membro estão disponíveis para todos os membros de um determinado nível. Em termos de organização, elas são tratadas como dados organizados dimensionalmente, armazenados em uma única dimensão.  
  
> [!NOTE]
>  No [!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], as propriedades do membro são conhecidas como relações de atributo. Para obter mais informações, consulte [Relações de atributos](../../../analysis-services/multidimensional-models-olap-logical-dimension-objects/attribute-relationships.md).  
  
 As propriedades do membro são *intrínsecas* ou *personalizadas*:  
  
 Propriedades do membro intrínsecas  
 Todos os membros suportam propriedades intrínsecas, como o valor formatado de um membro, enquanto dimensões e níveis fornecem propriedades do membro da dimensão e do nível intrínsecas adicionais, como a identificação de um membro.  
  
 Para obter mais informações, consulte [Propriedades intrínsecas do membro &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-member-properties-intrinsic-member-properties.md).  
  
 Propriedades do membro definidas pelo usuário  
 Com frequência, os membros possuem propriedades adicionais associadas a eles. Por exemplo, o nível Produtos pode oferecer as propriedades SKU, SRP, Importância e Volume para cada produto. Essas propriedades não são membros, mas contêm informações adicionais sobre os membros do nível Produtos.  
  
 Para obter mais informações, consulte [Propriedades do membro definidas pelo usuário &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-member-properties-user-defined-member-properties.md).  
  
 Tanto as propriedades do membro intrínsecas como as definidas pelo usuário podem ser recuperadas por meio da palavra-chave **PROPERTIES** ou da função [Propriedades](../../../mdx/properties-mdx.md).  
  
## <a name="using-the-properties-keyword"></a>Usando a palavra-chave PROPERTIES  
 A palavra-chave **PROPERTIES** especifica as propriedades do membro que serão usadas em uma determinada dimensão de eixo. A palavra-chave **PROPERTIES** é inserida na cláusula `<axis specification>` da instrução MDX [SELECT](../../../mdx/mdx-data-manipulation-select.md) :  
  
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
>  Para obter mais informações sobre os valores `<set>` e `<axis_name>`, consulte [Especificando o conteúdo de um eixo de consulta &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-query-and-slicer-axes-specify-the-contents-of-a-query-axis.md).  
  
 A palavra-chave `<dim_props>` permite a consulta de uma dimensão, de um nível e de propriedades do membro usando a palavra-chave **PROPERTIES** . A sintaxe a seguir mostra a formatação da cláusula `<dim_props>` :  
  
```  
<dim_props> ::= [DIMENSION] PROPERTIES <property> [,<property>...]  
```  
  
 A quebra da sintaxe `<property>` varia de acordo com a propriedade que você está consultando:  
  
-   Propriedades do membro intrínsecas sensíveis a contexto devem ser precedidas pelo nome da dimensão ou do nível. No entanto, propriedades do membro intrínsecas não sensíveis a contexto não podem ser qualificadas pelo nome da dimensão ou do nível. Para obter mais informações sobre como usar a palavra-chave **PROPERTIES** com propriedades intrínsecas do membro, consulte [Propriedades intrínsecas do membro &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-member-properties-intrinsic-member-properties.md).  
  
-   Propriedades do membro definidas pelo usuário devem ser precedidas pelo nome do nível no qual residem. Para obter mais informações sobre como usar a palavra-chave **PROPERTIES** com propriedades do membro definidas pelo usuário, consulte [Propriedades do membro definidas pelo usuário &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-member-properties-user-defined-member-properties.md).  
  
## <a name="see-also"></a>Consulte também  
 [Criando e usando valores de propriedade &#40;MDX&#41;](http://msdn.microsoft.com/library/0cafb269-03c8-4183-b6e9-220f071e4ef2)  
  
  
