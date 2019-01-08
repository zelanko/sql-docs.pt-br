---
title: LN (Expressão SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- LN function
- natural logarithm of expression [Integration Services]
ms.assetid: 55d7b657-b5fd-4753-9c81-54ed7575e720
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: eea8fed6bb9330bd552aed042d6aac3557274376
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/03/2018
ms.locfileid: "52823670"
---
# <a name="ln-ssis-expression"></a>LN (Expressão SSIS)
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
  
## <a name="remarks"></a>Comentários  
 A expressão numérica é convertida para o tipo de dados DT_R8 antes de o logaritmo ser computado. Para obter mais informações, consulte [Integration Services Data Types](../data-flow/integration-services-data-types.md).  
  
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
  
## <a name="see-also"></a>Consulte também  
 [LOG &#40;Expressão SSIS&#41;](log-ssis-expression.md)   
 [Funções &#40;Expressão do SSIS&#41;](functions-ssis-expression.md)  
  
  
