---
title: CEILING (Expressão SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
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
ms.openlocfilehash: b0b9c9c7ab5ed0067d86b3beaa69461ab6e90672
ms.sourcegitcommit: fd71d04a9d30a9927cbfff645750ac9d5d5e5ee7
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/16/2019
ms.locfileid: "65725572"
---
# <a name="ceiling-ssis-expression"></a>CEILING (Expressão SSIS)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


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
  
## <a name="remarks"></a>Remarks  
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
  
 Retorna -124,00  
  
```  
CEILING(0.00)  
```  
  
 Retorna 0.00  
  
## <a name="see-also"></a>Consulte Também  
 [FLOOR &#40;Expressão SSIS&#41;](../../integration-services/expressions/floor-ssis-expression.md)   
 [Funções &#40;Expressão do SSIS&#41;](../../integration-services/expressions/functions-ssis-expression.md)  
  
  
