---
title: Instrução DROP SET (MDX) | Microsoft Docs
ms.custom: ''
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- SET
- DROP
- DROP SET
- DROP_SET
dev_langs:
- kbMDX
helpviewer_keywords:
- DROP SET statement
- deleting named sets
- named sets [MDX]
- removing named sets
- dropping named sets
ms.assetid: bbc37afb-af8c-41df-ba81-12771beb1c41
caps.latest.revision: 35
author: Minewiskan
ms.author: owend
manager: erikre
ms.openlocfilehash: e98ab15f5370eab52f4dc467bf13e7d52c62c979
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="mdx-data-definition---drop-set"></a>Definição de dados MDX - DROP SET
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

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
  
## <a name="remarks"></a>Remarks  
 Para obter mais informações sobre conjuntos nomeados, consulte [Criando conjuntos nomeados em MDX &#40;MDX&#41;](../analysis-services/multidimensional-models/mdx/mdx-named-sets-building-named-sets.md).  
  
## <a name="see-also"></a>Consulte também  
 [Instruções de definição de dados MDX &#40;MDX&#41;](../mdx/mdx-data-definition-statements-mdx.md)  
  
  
