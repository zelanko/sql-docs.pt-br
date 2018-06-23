---
title: '- (Negar) (Expressão SSIS) | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- '- (negative)'
- negative operator (-)
ms.assetid: f0118dfc-aced-4de2-953e-5ebf9c962b8d
caps.latest.revision: 33
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 6bbdbea2ccc69cbbcf6c35fe14254d2b9e0a4b2d
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36130802"
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
  
## <a name="see-also"></a>Consulte também  
 [Precedência do operador e capacidade de associação](operator-precedence-and-associativity.md)   
 [Operadores &#40;expressão SSIS&#41;](operators-ssis-expression.md)  
  
  