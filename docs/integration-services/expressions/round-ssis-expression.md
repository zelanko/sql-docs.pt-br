---
title: ROUND (Expressão SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- rounding expressions
- ROUND function [SSIS]
ms.assetid: 376f1947-4fc5-4611-ad86-823e4db1b468
caps.latest.revision: 33
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: e6a3156fd30348f8bae8f3e66233ac1b0be99a66
ms.sourcegitcommit: cc46afa12e890edbc1733febeec87438d6051bf9
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/12/2018
ms.locfileid: "35400478"
---
# <a name="round-ssis-expression"></a>ROUND (Expressão SSIS)
  Retorna uma expressão numérica arredondada ao comprimento ou precisão especificados. O parâmetro de comprimento deve ser avaliado como um inteiro.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
ROUND(numeric_expression,length)  
```  
  
## <a name="arguments"></a>Argumentos  
 *numeric_expression*  
 É uma expressão de um tipo de numérico válido. Para obter mais informações, consulte [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md).  
  
 *comprimento*  
 É uma expressão de inteiro. Precisão para a qual *numeric_expression* é arredondada.  
  
## <a name="result-types"></a>Tipos de resultado  
 O mesmo tipo que *numeric*_*expression.*  
  
## <a name="remarks"></a>Remarks  
 O argumento *length* deve ser avaliado como um inteiro positivo ou zero.  
  
 ROUND retornará um resultado nulo se o argumento for nulo.  
  
## <a name="expression-examples"></a>Exemplos de expressões  
 Estes exemplos arredondam literais numéricos para um comprimento de três. O primeiro resultado de retorno é 137.1570, o segundo em 137.1580.  
  
```  
ROUND(137.1574,3)  
ROUND(137.1575,3)  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Funções &#40;Expressão do SSIS&#41;](../../integration-services/expressions/functions-ssis-expression.md)  
  
  
