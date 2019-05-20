---
title: () (Parênteses) (Expressão SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- () (parentheses operator)
- evaluation order [Integration Services]
- parentheses operator ()
ms.assetid: 931e10eb-1707-4121-b2f1-43565561119f
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 5eaf16b94271bb27808571c9bf219e41d8a1d868
ms.sourcegitcommit: fd71d04a9d30a9927cbfff645750ac9d5d5e5ee7
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/16/2019
ms.locfileid: "65725056"
---
# <a name="-parentheses-ssis-expression"></a>() (Parênteses) (Expressão SSIS)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


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
  
  
