---
description: SQRT (Expressão SSIS)
title: SQRT (Expressão SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- SQRT function
- square root of given expression
ms.assetid: 54a75389-c501-4e22-87b8-905f66d6a3a5
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 6308d8534e0a0d10d1696d86c09d619e8f8836aa
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88477379"
---
# <a name="sqrt-ssis-expression"></a>SQRT (Expressão SSIS)

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  Retorna a raiz quadrada de uma expressão numérica.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
SQRT(numeric_expression)  
```  
  
## <a name="arguments"></a>Argumentos  
 *numeric_expression*  
 É uma expressão numérica de qualquer tipo de dados numérico. Para obter mais informações, consulte [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md).  
  
## <a name="result-types"></a>Tipos de resultado  
 DT_R8  
  
## <a name="remarks"></a>Comentários  
 SQRT retornará um resultado nulo se o argumento for nulo.  
  
 SQRT falhará se o argumento for um valor negativo.  
  
 O argumento é convertido para o tipo de dados de DT_R8 antes da operação de raiz quadrada.  
  
## <a name="expression-examples"></a>Exemplos de expressões  
 Este exemplo retorna a raiz quadrada de um literal numérico. O resultado de retorno é 12.  
  
```  
SQRT(144)  
```  
  
 Este exemplo retorna a raiz quadrada de uma expressão, o resultado da subtração de valores nas colunas **Value1** e **Value2** .  
  
```  
SQRT(Value1 - Value2)  
```  
  
 Este exemplo retorna o comprimento do terceiro lado de um triângulo direito, aplicando a função SQUARE a duas variáveis e calculando, em seguida, a raiz quadrada da soma. Se **Side1** contiver 3 e **Side2** contiver 4, a função SQRT retornará 5.  
  
```  
SQRT(SQUARE(@Side1) + SQUARE(@Side2))  
```  
  
> [!NOTE]  
>  Em expressões, nomes de variável incluem sempre o prefixo \@.  
  
## <a name="see-also"></a>Consulte Também  
 [Funções &#40;Expressão do SSIS&#41;](../../integration-services/expressions/functions-ssis-expression.md)  
  
  
