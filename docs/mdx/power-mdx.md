---
title: ^ (Potência) (MDX) | Microsoft Docs
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
dev_langs:
- kbMDX
helpviewer_keywords:
- functions [MDX], ^ (Power)
ms.assetid: be2becd7-5683-4891-9b8a-6e795fc9e47d
caps.latest.revision: 7
author: Minewiskan
ms.author: owend
manager: erikre
ms.openlocfilehash: 900dba3f0aeb5bc74aa318ee65cbdc5399467c84
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="-power-mdx"></a>^ (Potência) (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Executa uma operação aritmética que eleva um número por outro.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Numeric_Expression ^ Numeric_Expression  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *Numeric_Expression*  
 Uma linguagem MDX válida que retorna um valor numérico.  
  
## <a name="return-value"></a>Valor de retorno  
 Um valor com o tipo de dados do parâmetro com prioridade maior.  
  
## <a name="remarks"></a>Remarks  
 As duas expressões devem ser do mesmo tipo de dados ou uma expressão deve poder ser convertida implicitamente no tipo de dados da outra expressão. Se uma expressão for avaliada como um valor nulo, o operador retornará um valor nulo.  
  
## <a name="see-also"></a>Consulte também  
 [Referência de operador MDX &#40;MDX&#41;](../mdx/mdx-operator-reference-mdx.md)  
  
  
