---
title: XOR (MDX) | Microsoft Docs
ms.date: 05/30/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: eb0a91faaec7e5c2b6a7b2289e65989ba19b33e3
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/02/2018
ms.locfileid: "34581868"
---
# <a name="xor-mdx"></a>XOR (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

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
 Um valor booliano que retorna **true** se apenas um argumento for avaliado como **true**; caso contrário, **false**.  
  
## <a name="remarks"></a>Remarks  
 O **XOR** operador trata ambos os parâmetros como valores boolianos (zero, 0, como **false**; caso contrário, **true**) antes do operador realizar a exclusão lógica. A tabela a seguir ilustra como o **XOR** operador realizar a exclusão lógica.  
  
|*Expression1*|*Expression2*|Valor retornado|  
|-------------------|-------------------|------------------|  
|**true**|**true**|**false**|  
|**true**|**false**|**true**|  
|**false**|**true**|**true**|  
|**false**|**false**|**false**|  
  
## <a name="see-also"></a>Consulte também  
 [Referência de operador MDX &#40;MDX&#41;](../mdx/mdx-operator-reference-mdx.md)  
  
  
