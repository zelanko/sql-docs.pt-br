---
title: DAY (Expressão SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- DAY function
- dates [Integration Services], DAY
ms.assetid: d8447187-49df-45b7-a98e-142ad44fd3e2
caps.latest.revision: 38
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: e79780ad62800eac8dfabbd6c8b80eacc3abe5dc
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37148747"
---
# <a name="day-ssis-expression"></a>DAY (Expressão SSIS)
  Retorna um inteiro que representa a parte do dia em uma data.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
DAY(date)  
```  
  
## <a name="arguments"></a>Argumentos  
 *date*  
 É uma expressão que retorna uma data válida ou uma cadeia de caracteres em formato de data.  
  
## <a name="result-types"></a>Tipos de resultado  
 DT_I4  
  
## <a name="remarks"></a>Remarks  
 DAY retornará um resultado nulo se o argumento for nulo.  
  
 Um literal de data deve ser convertido explicitamente em um dos tipos de dados de data. Para obter mais informações, consulte [Integration Services Data Types](../data-flow/integration-services-data-types.md).  
  
> [!NOTE]  
>  A expressão não é validada quando um literal de data é convertido explicitamente em um destes tipos de dados de data: DT_DBTIMESTAMPOFFSET e DT_DBTIMESTAMP2.  
  
 A função DAY é mais resumida, mas equivale a usar a DATEPART ("Dia", data).  
  
## <a name="expression-examples"></a>Exemplos de expressões  
 Este exemplo retorna o número do dia em um literal de data. Se a data estiver no formato "mm/dd/aaaa", este exemplo retornará 23.  
  
```  
DAY((DT_DBTIMESTAMP)"11/23/2002")  
```  
  
 Este exemplo retorna o inteiro que representa o dia na coluna **ModifiedDate** .  
  
```  
DAY(ModifiedDate)  
```  
  
 Este exemplo retorna o inteiro que representa o dia da data atual.  
  
```  
DAY(GETDATE())  
```  
  
## <a name="see-also"></a>Consulte também  
 [DATEADD &#40;expressão do SSIS&#41;](dateadd-ssis-expression.md)   
 [DATEDIFF &#40;expressão do SSIS&#41;](datediff-ssis-expression.md)   
 [DATEPART &#40;Expressão do SSIS&#41;](datepart-ssis-expression.md)   
 [MONTH &#40;Expressão do SSIS&#41;](month-ssis-expression.md)   
 [YEAR &#40;Expressão do SSIS&#41;](year-ssis-expression.md)   
 [Funções &#40;expressão do SSIS&#41;](functions-ssis-expression.md)  
  
  
