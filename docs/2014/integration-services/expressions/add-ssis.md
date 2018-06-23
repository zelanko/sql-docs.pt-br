---
title: + (Adicionar) (SSIS) | Microsoft Docs
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
- + (add)
- add operator (+)
- adding expressions
ms.assetid: 44df4154-fed5-4e7f-9995-e703a0164f6a
caps.latest.revision: 27
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: b96a6e5c659925ea5eed876e1f7505997ea02b71
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36117020"
---
# <a name="-add-ssis"></a>+ (Adição) (SSIS)
  Soma duas expressões numéricas.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
numeric_expression1 + numeric_expression2  
  
```  
  
## <a name="arguments"></a>Argumentos  
 *numeric_expression1, numeric_ expression2*  
 É qualquer expressão válida de um tipo de dados numérico.  
  
## <a name="result-types"></a>Tipos de resultado  
 Determinado por tipos de dados dos dois argumentos. Para obter mais informações, consulte [Integration Services Data Types](../data-flow/integration-services-data-types.md).  
  
## <a name="remarks"></a>Remarks  
 Se qualquer operando for nulo, o resultado será nulo.  
  
## <a name="expression-examples"></a>Exemplos de expressões  
 Este exemplo soma literais numéricos.  
  
```  
5 + 6.09 + 7.0  
```  
  
 Este exemplo soma valores nas colunas **VacationHours** e **SickLeaveHours** .  
  
```  
VacationHours + SickLeaveHours  
```  
  
 Este exemplo acrescenta um valor calculado à coluna **StandardCost** . A variável **Profit%** deve estar entre colchetes porque o nome inclui o caractere % . Para obter mais informações, consulte [Identificadores &#40;SSIS&#41;](identifiers-ssis.md).  
  
```  
StandardCost + (StandardCost * @[Profit%])  
```  
  
## <a name="see-also"></a>Consulte também  
 [Precedência do operador e capacidade de associação](operator-precedence-and-associativity.md)   
 [Operadores &#40;expressão SSIS&#41;](operators-ssis-expression.md)  
  
  