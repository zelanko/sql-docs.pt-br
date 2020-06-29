---
title: '- (Negar) (Expressão SSIS) | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- '- (negative)'
- negative operator (-)
ms.assetid: f0118dfc-aced-4de2-953e-5ebf9c962b8d
author: chugugrace
ms.author: chugu
ms.openlocfilehash: bd4c13677b1c4b7e0a788b3459e8f658e25c2c6c
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/26/2020
ms.locfileid: "85437193"
---
# <a name="--negate-ssis-expression"></a>- (Negação) (Expressão SSIS)
  Nega uma expressão numérica.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
-numeric_expression  
  
```  
  
## <a name="arguments"></a>Argumentos  
 *numeric_expression*  
 É qualquer expressão válida de um tipo de dados numérico. Há suporte somente para tipos de dados numéricos assinados. Para obter mais informações, consulte [Integration Services Data Types](../data-flow/integration-services-data-types.md).  
  
## <a name="result-types"></a>Tipos de resultado  
 Retorna o tipo de dados de *numeric_expression*.  
  
## <a name="expression-examples"></a>Exemplos de expressões  
 Esse exemplo nega o valor da variável **Counter** e adiciona o literal numérico 50.  
  
```  
-@Counter + 50  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Precedência de operador e capacidade de associação](operator-precedence-and-associativity.md)   
 [Operadores &#40;Expressão do SSIS&#41;](operators-ssis-expression.md)  
  
  
