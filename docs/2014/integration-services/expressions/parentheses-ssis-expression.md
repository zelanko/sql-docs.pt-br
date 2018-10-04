---
title: () (Parênteses) (Expressão SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
helpviewer_keywords:
- () (parentheses operator)
- evaluation order [Integration Services]
- parentheses operator ()
ms.assetid: 931e10eb-1707-4121-b2f1-43565561119f
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 3cfcad949dd07d4eec4513b09a19cf262bd5c787
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48101976"
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
 O tipo de dados de *expression*. Para obter mais informações, consulte [Integration Services Data Types](../data-flow/integration-services-data-types.md).  
  
## <a name="expression-examples"></a>Exemplos de expressões  
 Este exemplo mostra como o uso de parênteses modifica a precedência de operadores. A primeira expressão é avaliada como 100, embora a segunda seja avaliada como 31.  
  
```  
(5 + 5) * (4 + 6)  
5 + 5 * 4 + 6  
  
```  
  
## <a name="see-also"></a>Consulte também  
 [Associatividade e precedência de operador](operator-precedence-and-associativity.md)   
 [Operadores &#40;expressão do SSIS&#41;](operators-ssis-expression.md)  
  
  
