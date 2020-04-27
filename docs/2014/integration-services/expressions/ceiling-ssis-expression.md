---
title: CEILING (Expressão SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- smallest integer great than or equal to expression
- CEILING function [SSIS]
ms.assetid: c35bd4ee-1ab6-46ab-89a7-cf771527faa2
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: a8306fa98194fbf314796b199fea98ddd53cb1fb
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62769422"
---
# <a name="ceiling-ssis-expression"></a>CEILING (Expressão SSIS)
  Retorna o menor inteiro que é maior que ou igual a uma expressão numérica.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
CEILING(numeric_expression)  
```  
  
## <a name="arguments"></a>Argumentos  
 *numeric_expression*  
 É uma expressão numérica válida.  
  
## <a name="result-types"></a>Tipos de resultado  
 O tipo de dados da expressão numérica submetido à função.  
  
## <a name="remarks"></a>Comentários  
 CEILING retornará um resultado nulo se o argumento for nulo.  
  
## <a name="expression-examples"></a>Exemplos de expressões  
 Estes exemplos se aplicam à função CEILING para valores positivo, negativo e zero.  
  
```  
CEILING(123.74)  
```  
  
 Retorna 124,00  
  
```  
CEILING(-124.27)  
```  
  
 Retorna -124.00  
  
```  
CEILING(0.00)  
```  
  
 Retorna 0.00  
  
## <a name="see-also"></a>Consulte Também  
 [FLOOR &#40;Expressão SSIS&#41;](floor-ssis-expression.md)   
 [Funções &#40;Expressão do SSIS&#41;](functions-ssis-expression.md)  
  
  
