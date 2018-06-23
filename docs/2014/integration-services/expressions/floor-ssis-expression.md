---
title: FLOOR (Expressão SSIS) | Microsoft Docs
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
- largest integer less than or equal to expression
- FLOOR function [SSIS]
ms.assetid: 168084db-badd-40f2-87b4-1f5bc45c3e24
caps.latest.revision: 33
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: cae43e01a262258fa2fce824797b3d20682c3829
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36011424"
---
# <a name="floor-ssis-expression"></a>FLOOR (Expressão SSIS)
  Retorna o maior inteiro que é menor que ou igual a uma expressão numérica.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
FLOOR(numeric_expression)  
```  
  
## <a name="arguments"></a>Argumentos  
 *numeric_expression*  
 É uma expressão numérica válida.  
  
## <a name="result-types"></a>Tipos de resultado  
 O tipo de dados numérico da expressão do argumento. O resultado é a parte inteira do valor calculado no mesmo tipo de dados que *numeric_expression.*  
  
## <a name="remarks"></a>Remarks  
 FLOOR retornará um resultado nulo se o argumento for nulo.  
  
## <a name="expression-examples"></a>Exemplos de expressões  
 Estes exemplos aplicam a função FLOOR aos valores positivos, negativos e zerados.  
  
```  
FLOOR(123.45)  
```  
  
 Retorna 123.00  
  
```  
FLOOR(-123.45)  
```  
  
 Retorna -124.00  
  
```  
FLOOR(0.00)  
```  
  
 Retorna 0.00  
  
## <a name="see-also"></a>Consulte também  
 [CEILING &#40;expressão SSIS&#41;](ceiling-ssis-expression.md)   
 [Funções &#40;expressão SSIS&#41;](functions-ssis-expression.md)  
  
  