---
title: () (Parênteses) (Expressão SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.service: ''
ms.component: expressions
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- () (parentheses operator)
- evaluation order [Integration Services]
- parentheses operator ()
ms.assetid: 931e10eb-1707-4121-b2f1-43565561119f
caps.latest.revision: 36
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 16412dc829f4a574a505928d6c4ff380dd8273d4
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2018
---
# <a name="-parentheses-ssis-expression"></a>() (Parênteses) (Expressão SSIS)
  Identifica a ordem de avaliação de expressões. Expressões incluídas em parênteses têm a precedência de avaliação mais alta. São avaliadas expressões aninhadas incluídas em parênteses na ordem interno-para-externo.  
  
 Parênteses também são usados para facilitar a compreensão de expressões complexas.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
(expression)  
  
```  
  
## <a name="arguments"></a>Argumentos  
 *expressão*  
 É qualquer expressão válida.  
  
## <a name="result-types"></a>Tipos de resultado  
 O tipo de dados de *expression*. Para obter mais informações, consulte [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md).  
  
## <a name="expression-examples"></a>Exemplos de expressões  
 Este exemplo mostra como o uso de parênteses modifica a precedência de operadores. A primeira expressão é avaliada como 100, embora a segunda seja avaliada como 31.  
  
```  
(5 + 5) * (4 + 6)  
5 + 5 * 4 + 6  
  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Precedência de operador e capacidade de associação](../../integration-services/expressions/operator-precedence-and-associativity.md)   
 [Operadores &#40;Expressão do SSIS&#41;](../../integration-services/expressions/operators-ssis-expression.md)  
  
  
