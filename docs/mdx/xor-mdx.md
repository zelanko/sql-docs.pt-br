---
title: XOR (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: f9115fc1e226e05c788206706d59a5435bfd1c5d
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63251471"
---
# <a name="xor-mdx"></a>XOR (MDX)


  Executa uma exclusão lógica em duas expressões numéricas.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Expression1 XOR Expression2  
  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *Expression1*  
 Uma linguagem MDX válida que retorna um valor numérico.  
  
 *Expression2*  
 Uma expressão MDX válida que retorna um valor numérico.  
  
## <a name="return-value"></a>Valor retornado  
 Um valor booliano que retorna **verdadeira** se apenas um argumento é avaliado como **verdadeiro**; caso contrário, **false**.  
  
## <a name="remarks"></a>Comentários  
 O **XOR** operador trata ambos os parâmetros como valores boolianos (zero, 0, como **falso**; caso contrário, **verdadeiro**) antes do operador realizar a exclusão lógica. A tabela a seguir ilustra como o **XOR** operador realizar a exclusão lógica.  
  
|*Expression1*|*Expression2*|Valor retornado|  
|-------------------|-------------------|------------------|  
|**true**|**true**|**false**|  
|**true**|**false**|**true**|  
|**false**|**true**|**true**|  
|**false**|**false**|**false**|  
  
## <a name="see-also"></a>Consulte também  
 [Referência de operador MDX &#40;MDX&#41;](../mdx/mdx-operator-reference-mdx.md)  
  
  
