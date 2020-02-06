---
title: '! (Não Lógico) (Expressão SSIS) | Microsoft Docs'
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- logical Not (!)
- '! (logical Not)'
ms.assetid: d5c4d1e1-7be4-4d25-bcd9-5b6ddb53b3b3
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 7ce0a8e44a89dbac275b8c2df320a20e7bc14f14
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/01/2020
ms.locfileid: "71297492"
---
# <a name="-logical-not-ssis-expression"></a>! (Não lógico) (Expressão do SSIS)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  Nega um operando booliano.  
  
> [!NOTE]  
>  O operador ! não pode ser usado em conjunto com outros operadores. Por exemplo, você não pode combinar os operadores ! e os operadores > no operador !>.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
!boolean_expression  
  
```  
  
## <a name="arguments"></a>Argumentos  
 *boolean_expression*  
 É qualquer expressão válida avaliada como um Booliano. Para obter mais informações, consulte [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md).  
  
## <a name="result-types"></a>Tipos de resultado  
 DT_BOOL  
  
## <a name="remarks"></a>Comentários  
 A tabela a seguir mostra o resultado da operação operação.  
  
|Expressão booliana original|Depois de aplicar o operador|  
|---------------------------------|------------------------------------|  
|TRUE|FALSE|  
|NULO|NULO|  
|FALSE|TRUE|  
  
## <a name="expression-examples"></a>Exemplos de expressões  
 Este exemplo será avaliado como FALSE se o valor da coluna **Color** for "vermelho".  
  
```  
!(Color == "red")  
```  
  
 Esse exemplo será avaliado como TRUE se o valor da variável **MonthNumber** for o mesmo que o inteiro que representa o mês atual. Para obter mais informações, consulte [MONTH &#40;Expressão SSIS&#41;](../../integration-services/expressions/month-ssis-expression.md) e [GETDATE &#40;Expressão SSIS&#41;](../../integration-services/expressions/getdate-ssis-expression.md).  
  
```  
!(@MonthNumber != MONTH(GETDATE())  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Precedência de operador e capacidade de associação](../../integration-services/expressions/operator-precedence-and-associativity.md)   
 [Operadores &#40;Expressão do SSIS&#41;](../../integration-services/expressions/operators-ssis-expression.md)  
  
  
