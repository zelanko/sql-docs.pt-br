---
title: LN (Expressão SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- LN function
- natural logarithm of expression [Integration Services]
ms.assetid: 55d7b657-b5fd-4753-9c81-54ed7575e720
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: ac9490abd45c37005fc77ed7733768fa6d7c35a9
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65725247"
---
# <a name="ln-ssis-expression"></a>LN (Expressão SSIS)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  Retorna o logaritmo natural de uma expressão numérica.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
LN(numeric_expression)  
```  
  
## <a name="arguments"></a>Argumentos  
 *numeric_expression*  
 É uma expressão numérica não negativa, diferente de zero válida.  
  
## <a name="result-types"></a>Tipos de resultado  
 DT_R8  
  
## <a name="remarks"></a>Remarks  
 A expressão numérica é convertida para o tipo de dados DT_R8 antes de o logaritmo ser computado. Para obter mais informações, consulte [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md).  
  
 Se *numeric_expression* for avaliado como zero ou um valor negativo, o resultado de retorno será nulo.  
  
## <a name="expression-examples"></a>Exemplos de expressões  
 Esse exemplo usa um literal numérico. A função retorna o valor 3.737766961828337.  
  
```  
LN(42)  
```  
  
 Esse exemplo usa a coluna **Length**. Se o valor da coluna for 53.99, a função retornará 3.9887988442302.  
  
```  
LN(Length)   
```  
  
 Esse exemplo usa a variável **Length**. A variável deve ser um tipo de dados numérico ou a expressão deve incluir uma conversão explícita para um tipo de dados numérico. Se **Length** for 234.567, a função retornará 5.45774126708797.  
  
```  
LN(@Length)   
```  
  
## <a name="see-also"></a>Consulte Também  
 [LOG &#40;Expressão SSIS&#41;](../../integration-services/expressions/log-ssis-expression.md)   
 [Funções &#40;Expressão do SSIS&#41;](../../integration-services/expressions/functions-ssis-expression.md)  
  
  
