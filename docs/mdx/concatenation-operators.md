---
description: Operadores de concatenação
title: Operadores de concatenação | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: b53f5d79124a86e8748a473af5b371152932514e
ms.sourcegitcommit: cfa04a73b26312bf18d8f6296891679166e2754d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/19/2020
ms.locfileid: "92192551"
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
 Quando as duas cadeias de caracteres usadas em uma concatenação têm a mesma ordenação, a cadeia de caracteres concatenada resultante tem a mesma ordenação das entradas. Quando as cadeias de caracteres usadas em uma concatenação têm ordenações diferentes, as regras de prioridade de ordenação determinam a ordenação da cadeia de caracteres concatenada resultante. Para obter mais informações, consulte [Idiomas e ordenações &#40;Analysis Services&#41;](/analysis-services/languages-and-collations-analysis-services).  
  
## <a name="see-also"></a>Consulte Também  
 [Referência de operador MDX &#40;&#41;MDX ](../mdx/mdx-operator-reference-mdx.md)   
 [Operadores &#40;sintaxe MDX&#41;](../mdx/operators-mdx-syntax.md)  
  
