---
title: EXP (Expressão SSIS) | Microsoft Docs
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
- exponential functions
- EXP function
ms.assetid: 4cd96d3c-58c9-4a67-a6f6-b72758232912
caps.latest.revision: 34
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: cd5eb9625ad6987b38faa350b3a0c7c10d3ea612
ms.sourcegitcommit: cc46afa12e890edbc1733febeec87438d6051bf9
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/12/2018
ms.locfileid: "35410848"
---
# <a name="exp-ssis-expression"></a>EXP (Expressão SSIS)
  Retorna o expoente para a base e de uma expressão numérica. A função EXP complementa a ação da função LN e, às vezes, é chamado de antilogaritmo.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
EXP(numeric_expression)  
```  
  
## <a name="arguments"></a>Argumentos  
 *numeric_expression*  
 É uma expressão numérica válida.  
  
## <a name="result-types"></a>Tipos de resultado  
 DT_R8  
  
## <a name="remarks"></a>Remarks  
 A expressão numérica é lançada para o tipo de dados de DT_R8 antes de o expoente ser computado. Para obter mais informações, consulte [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md).  
  
 O resultado de retorno sempre é um número positivo.  
  
## <a name="expression-examples"></a>Exemplos de expressões  
 Estes exemplos se aplicam à função EXP para valores positivo e negativos e para zero.  
  
```  
EXP(74)  
```  
  
 Retorna 1.373382979540176E+32.  
  
```  
EXP(-27)  
```  
  
 Retorna 1.879528816539083E-12.  
  
```  
EXP(0)  
```  
  
 Retorna 1.  
  
## <a name="see-also"></a>Consulte Também  
 [LOG &#40;Expressão SSIS&#41;](../../integration-services/expressions/log-ssis-expression.md)   
 [Funções &#40;Expressão do SSIS&#41;](../../integration-services/expressions/functions-ssis-expression.md)  
  
  
