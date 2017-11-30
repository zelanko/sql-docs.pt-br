---
title: "NÃO (MDX) | Microsoft Docs"
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
f1_keywords: NOT
dev_langs: kbMDX
helpviewer_keywords: NOT operator [MDX]
ms.assetid: c11bd3b0-54b3-4a6d-babc-6067722194db
caps.latest.revision: "26"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: df89fa9d5d8a822680dff5d7185753453a7dee87
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/27/2017
---
# <a name="not-mdx"></a>NOT (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Realiza uma negação lógica em uma expressão numérica.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
NOT Expression1  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *Expression1*  
 Uma linguagem MDX válida que retorna um valor numérico.  
  
## <a name="return-value"></a>Valor de retorno  
 Um valor booliano que retorna **false** se o argumento for avaliado como **true**; caso contrário, **true**.  
  
## <a name="remarks"></a>Comentários  
 O **não** operador trata a expressão como um valor booliano (zero, 0, como **false**; caso contrário, **true**) antes que o operador realize a negação lógica. A tabela a seguir ilustra como o **não** operador realize a negação lógica.  
  
|*Expression1*|Valor de retorno|  
|-------------------|------------------|  
|**true**|**false**|  
|**false**|**true**|  
  
## <a name="see-also"></a>Consulte também  
 [Referência de operador MDX &#40; MDX &#41;](../mdx/mdx-operator-reference-mdx.md)  
  
  
