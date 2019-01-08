---
title: ROUND (Expressão SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- rounding expressions
- ROUND function [SSIS]
ms.assetid: 376f1947-4fc5-4611-ad86-823e4db1b468
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 3033398be7625230ac6d9abd7b8b329f312632c1
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/03/2018
ms.locfileid: "52808008"
---
# <a name="round-ssis-expression"></a>ROUND (Expressão SSIS)
  Retorna uma expressão numérica arredondada ao comprimento ou precisão especificados. O parâmetro de comprimento deve ser avaliado como um inteiro.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
ROUND(numeric_expression,length)  
```  
  
## <a name="arguments"></a>Argumentos  
 *numeric_expression*  
 É uma expressão de um tipo de numérico válido. Para obter mais informações, consulte [Integration Services Data Types](../data-flow/integration-services-data-types.md).  
  
 *comprimento*  
 É uma expressão de inteiro. Precisão para a qual *numeric_expression* é arredondada.  
  
## <a name="result-types"></a>Tipos de resultado  
 O mesmo tipo que *numeric*_*expression.*  
  
## <a name="remarks"></a>Comentários  
 O argumento *length* deve ser avaliado como um inteiro positivo ou zero.  
  
 ROUND retornará um resultado nulo se o argumento for nulo.  
  
## <a name="expression-examples"></a>Exemplos de expressões  
 Estes exemplos arredondam literais numéricos para um comprimento de três. O primeiro resultado de retorno é 137.1570, o segundo em 137.1580.  
  
```  
ROUND(137.1574,3)  
ROUND(137.1575,3)  
```  
  
## <a name="see-also"></a>Consulte também  
 [Funções &#40;Expressão do SSIS&#41;](functions-ssis-expression.md)  
  
  
