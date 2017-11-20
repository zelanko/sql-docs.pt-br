---
title: "NÃO (DMX) | Microsoft Docs"
ms.custom: 
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- NOT
dev_langs:
- DMX
helpviewer_keywords:
- NOT operator [DMX]
ms.assetid: 6d91b3d9-270c-4a68-b41f-169cff5faa0e
caps.latest.revision: 13
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 947d066f9dd13d7f4af15407987fcf218c275cc2
ms.contentlocale: pt-br
ms.lasthandoff: 08/02/2017

---
# <a name="not-dmx"></a>NOT (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Operador lógico que executa uma negação lógica em uma expressão numérica.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
NOT Expression1  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *Expression1*  
 Expressão DMX válida que retorna um valor numérico.  
  
## <a name="return-value"></a>Valor de retorno  
 Valor booliano que retorna FALSE se o argumento avaliar como TRUE; do contrário, FALSE.  
  
## <a name="remarks"></a>Comentários  
 O argumento é tratado como valor booliano (0 como FALSE; do contrário, TRUE) antes que o operador realize a negação lógica. Se *Expression1* for TRUE, o operador retornará FALSE. Se *Expression1* é FALSE, o operador retornará TRUE. A tabela a seguir ilustra como a conjunção lógica é executada.  
  
|Se a Expression1 for|O valor de retorno será|  
|-----------------------|---------------------|  
|TRUE|FALSE|  
|FALSE|TRUE|  
  
## <a name="see-also"></a>Consulte também  
 [Extensões de mineração de dados &#40; DMX &#41; Referência de operador](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [Lógica operadores &#40; DMX &#41;](../dmx/operators-logical.md)   
 [Operadores &#40; DMX &#41;](../dmx/operators-dmx.md)  
  
  

