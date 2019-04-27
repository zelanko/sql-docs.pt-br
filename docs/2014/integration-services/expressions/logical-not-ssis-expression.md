---
title: '! (Não Lógico) (Expressão SSIS) | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- logical Not (!)
- '! (logical Not)'
ms.assetid: d5c4d1e1-7be4-4d25-bcd9-5b6ddb53b3b3
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: bfcd8337105766d91e097d35201d749c86ca840e
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62769023"
---
# <a name="-logical-not-ssis-expression"></a>! (Não lógico) (Expressão do SSIS)
  Nega um operando booliano.  
  
> [!NOTE]  
>  O operador ! não pode ser usado em conjunto com outros operadores. Por exemplo, você não pode combinar os operadores ! e os operadores > no operador !>.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
!boolean_expression  
  
```  
  
## <a name="arguments"></a>Argumentos  
 *boolean_expression*  
 É qualquer expressão válida avaliada como um Booliano. Para obter mais informações, consulte [Integration Services Data Types](../data-flow/integration-services-data-types.md).  
  
## <a name="result-types"></a>Tipos de resultado  
 DT_BOOL  
  
## <a name="remarks"></a>Comentários  
 A tabela a seguir mostra o resultado da operação publicação.  
  
|Expressão booliana original|Depois de aplicar o operador|  
|---------------------------------|------------------------------------|  
|TRUE|FALSE|  
|NULL|NULL|  
|FALSE|TRUE|  
  
## <a name="expression-examples"></a>Exemplos de expressões  
 Este exemplo será avaliado como FALSE se o valor da coluna **Color** for "vermelho".  
  
```  
!(Color == "red")  
```  
  
 Esse exemplo será avaliado como TRUE se o valor da variável **MonthNumber** for o mesmo que o inteiro que representa o mês atual. Para obter mais informações, consulte [MONTH &#40;Expressão SSIS&#41;](month-ssis-expression.md) e [GETDATE &#40;Expressão SSIS&#41;](getdate-ssis-expression.md).  
  
```  
!(@MonthNumber != MONTH(GETDATE())  
```  
  
## <a name="see-also"></a>Consulte também  
 [Precedência de operador e capacidade de associação](operator-precedence-and-associativity.md)   
 [Operadores &#40;Expressão do SSIS&#41;](operators-ssis-expression.md)  
  
  
