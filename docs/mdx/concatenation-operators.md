---
title: Operadores de concatenação | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 8eacfc08fdeb0f92874758d0f95e5cde3e6b295a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63181484"
---
# <a name="concatenation-operators"></a>Operadores de concatenação


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
 Quando as duas cadeias de caracteres usadas em uma concatenação têm a mesma ordenação, a cadeia de caracteres concatenada resultante tem a mesma ordenação das entradas. Quando as cadeias de caracteres usadas em uma concatenação têm ordenações diferentes, as regras de prioridade de ordenação determinam a ordenação da cadeia de caracteres concatenada resultante. Para obter mais informações, consulte [Idiomas e ordenações &#40;Analysis Services&#41;](../analysis-services/languages-and-collations-analysis-services.md).  
  
## <a name="see-also"></a>Consulte também  
 [Referência de operador MDX &#40;MDX&#41;](../mdx/mdx-operator-reference-mdx.md)   
 [Operadores &#40;sintaxe MDX&#41;](../mdx/operators-mdx-syntax.md)  
  
  
