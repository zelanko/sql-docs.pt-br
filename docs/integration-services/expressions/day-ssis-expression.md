---
title: DAY (Expressão SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- DAY function
- dates [Integration Services], DAY
ms.assetid: d8447187-49df-45b7-a98e-142ad44fd3e2
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 9b170928624565d8dc1f80cea93eed4473db3e5e
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/22/2020
ms.locfileid: "86921269"
---
# <a name="day-ssis-expression"></a>DAY (Expressão SSIS)

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


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
  
## <a name="remarks"></a>Comentários  
 DAY retornará um resultado nulo se o argumento for nulo.  
  
 Um literal de data deve ser convertido explicitamente em um dos tipos de dados de data. Para obter mais informações, consulte [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md).  
  
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
  
## <a name="see-also"></a>Consulte Também  
 [DATEADD &#40;Expressão do SSIS&#41;](../../integration-services/expressions/dateadd-ssis-expression.md)   
 [DATEDIFF &#40;Expressão do SSIS&#41;](../../integration-services/expressions/datediff-ssis-expression.md)   
 [DATEPART &#40;Expressão do SSIS&#41;](../../integration-services/expressions/datepart-ssis-expression.md)   
 [MONTH &#40;Expressão do SSIS&#41;](../../integration-services/expressions/month-ssis-expression.md)   
 [YEAR &#40;Expressão do SSIS&#41;](../../integration-services/expressions/year-ssis-expression.md)   
 [Funções &#40;Expressão do SSIS&#41;](../../integration-services/expressions/functions-ssis-expression.md)  
  
  
