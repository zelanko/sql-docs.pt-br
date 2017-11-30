---
title: "Operadores de concatenação | Microsoft Docs"
ms.custom: 
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: kbMDX
helpviewer_keywords: concatenation operators [MDX]
ms.assetid: 9e4c181a-b71e-41ec-98a1-ec8b5b5103b1
caps.latest.revision: "25"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 317648b66574a2997720525d40ff3d0b77f095f1
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/27/2017
---
# <a name="concatenation-operators"></a>Operadores de concatenação
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  O operador de concatenação é o sinal de mais (+). Você pode combinar ou concatenar duas ou mais cadeias de caracteres em uma única cadeia de caracteres. Também é possível concatenar cadeias de caracteres binárias.  
  
 O código a seguir é um exemplo de operador de concatenação que combina o nome de produto com o nome exclusivo do produto:  
  
```  
WITH MEMBER Measures.ProductName AS   
   Product.Product.CurrentMember.Name + " (" + Product.Product.CurrentMember.UniqueName + ")"  
SELECT   
   {Measures.ProductName} ON COLUMNS,  
   Product.Product.Members ON ROWS  
FROM [Adventure Works]  
```  
  
## <a name="language-considerations"></a>Considerações sobre idioma  
 Quando as duas cadeias de caracteres usadas em uma concatenação têm o mesmo agrupamento, a cadeia de caracteres concatenada resultante tem o mesmo agrupamento das entradas. Quando as cadeias de caracteres usadas em uma concatenação têm agrupamentos diferentes, as regras de prioridade de agrupamento determinam o agrupamento da cadeia de caracteres concatenada resultante. Para obter mais informações, consulte [Idiomas e agrupamentos &#40;Analysis Services&#41;](../analysis-services/languages-and-collations-analysis-services.md).  
  
## <a name="see-also"></a>Consulte também  
 [Referência de operador MDX &#40; MDX &#41;](../mdx/mdx-operator-reference-mdx.md)   
 [Operadores &#40; Sintaxe MDX &#41;](../mdx/operators-mdx-syntax.md)  
  
  
