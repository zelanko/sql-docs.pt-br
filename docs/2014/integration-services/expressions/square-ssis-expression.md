---
title: SQUARE (Expressão SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- SQUARE
- square values
ms.assetid: cecf1bb2-3d55-40a6-9688-ed67bcc150b4
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: a7b312453000aaf3862eef91c5c660ecf6ecb9cf
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/03/2018
ms.locfileid: "52787228"
---
# <a name="square-ssis-expression"></a>SQUARE (Expressão SSIS)
  Retorna o quadrado de uma expressão numérica.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
SQUARE(numeric_expression)  
```  
  
## <a name="arguments"></a>Argumentos  
 *numeric_expression*  
 É uma expressão numérica de qualquer tipo de dados numérico. Para obter mais informações, consulte [Integration Services Data Types](../data-flow/integration-services-data-types.md).  
  
## <a name="result-types"></a>Tipos de resultado  
 DT_R8  
  
## <a name="remarks"></a>Comentários  
 SQUARE retornará um resultado nulo se o argumento for nulo.  
  
 O argumento é convertido para o tipo de dados de DT_R8 antes da operação de raiz quadrada.  
  
## <a name="expression-examples"></a>Exemplos de expressões  
 Este exemplo retorna o quadrado de 12. O resultado retornado é 144.  
  
```  
SQUARE(12)  
```  
  
 Este exemplo retorna o quadrado do resultado da subtração de valores em duas colunas. Se **Value1** contiver 12 e **Value2** contiver 4, a função SQUARE retornará 64.  
  
```  
SQUARE(Value1 - Value2)  
```  
  
 Este exemplo retorna o comprimento do terceiro lado de um triângulo de ângulo direito, aplicando a função SQUARE a duas variáveis e calculando, em seguida, a raiz quadrada da soma. Se **Side1** contiver 3 e **Side2** contiver 4, a função SQRT retornará 5.  
  
```  
SQRT(SQUARE(@Side1) + SQUARE(@Side2))  
```  
  
> [!NOTE]  
>  Em expressões, nomes de variável incluem sempre o prefixo \@.  
  
## <a name="see-also"></a>Consulte também  
 [Funções &#40;Expressão do SSIS&#41;](functions-ssis-expression.md)  
  
  
