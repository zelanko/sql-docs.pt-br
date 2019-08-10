---
title: Instrução DROP SET (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: f4e31a687597e454b9afe38d6c6dd1c15af486d0
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/09/2019
ms.locfileid: "68893723"
---
# <a name="mdx-data-definition---drop-set"></a>Definição de dados MDX – DROP SET


  Remove um conjunto nomeado.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
DROP [SESSION] SET   
   <Cube_Reference>.Set_Name   
               [,<Cube_Reference>.Set_Name ...n]  
  
<Cube_Reference> ::= {CURRENTCUBE | Cube_Name}  
  
```  
  
## <a name="arguments"></a>Argumentos  
 *Cube_Name*  
 Uma expressão de cadeia de caracteres válida que fornece o nome do cubo.  
  
 *Set_Name*  
 Uma expressão de cadeia de caracteres válida que fornece esse nome do conjunto nomeado a ser descartado.  
  
## <a name="remarks"></a>Comentários  
 Para obter mais informações sobre conjuntos nomeados, consulte [Criando conjuntos nomeados em MDX &#40;MDX&#41;](https://docs.microsoft.com/analysis-services/multidimensional-models/mdx/mdx-named-sets-building-named-sets).  
  
## <a name="see-also"></a>Consulte também  
 [MDX de instruções &#40;de definição de dados MDX&#41;](../mdx/mdx-data-definition-statements-mdx.md)  
  
  
