---
title: "DATEPART (expressão SSIS) | Microsoft Docs"
ms.custom:
- ssisdev020617
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- dates [Integration Services], DATEPART
- DATEPART function
ms.assetid: 3e590094-fc49-4144-805f-fdc1bf2fe509
caps.latest.revision: 40
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 49d23d0f60954f9312b6e36bd6570a9bc7b8121b
ms.contentlocale: pt-br
ms.lasthandoff: 08/03/2017

---
# <a name="datepart-ssis-expression"></a>DATEPART (Expressão SSIS)
  Retorna um inteiro que representa uma parte de uma data.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
DATEPART(datepart, date)  
```  
  
## <a name="arguments"></a>Argumentos  
 *datepart*  
 É o parâmetro que especifica para qual parte da data retornar um valor novo.  
  
 *date*  
 É uma expressão que retorna uma data válida ou uma cadeia de caracteres em formato de data.  
  
## <a name="result-types"></a>Tipos de resultado  
 DT_I4  
  
## <a name="remarks"></a>Comentários  
 DATEPART retorna um resultado nulo se o argumento for nulo.  
  
 Um literal de data deve ser convertido explicitamente em um dos tipos de dados de data. Para obter mais informações, consulte [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md).  
  
 A tabela a seguir lista as partes de data e as abreviações reconhecidas pelo avaliador de expressão. Os nomes das partes da data não diferenciam maiúsculas de minúsculas.  
  
|datepart|Abreviações|  
|--------------|-------------------|  
|Year|aa, aaaa|  
|Quarter|qq, q|  
|Month|mm, m|  
|Dia do ano|dy, y|  
|Day|dd, d|  
|Week|wk, ww|  
|Dia de semana|dw|  
|Hora|Hh|  
|Minuto|mi, n|  
|Segundo|ss, s|  
|Milissegundos|Ms|  
  
## <a name="ssis-expression-examples"></a>Exemplos de expressões SSIS  
 Este exemplo retorna o inteiro que representa o mês em um literal de data. Se a data estiver em formato mm/dd/aaaa", este exemplo retornará 11.  
  
```  
DATEPART("month", (DT_DBTIMESTAMP)"11/04/2002")  
```  
  
 Este exemplo retorna o inteiro que representa o dia na coluna **ModifiedDate** .  
  
```  
DATEPART("dd", ModifiedDate)  
```  
  
 Este exemplo retorna o inteiro que representa o ano da data atual.  
  
```  
DATEPART("yy",GETDATE())  
```  
  
## <a name="see-also"></a>Consulte também  
 [DATEADD &#40; Expressão do SSIS &#41;](../../integration-services/expressions/dateadd-ssis-expression.md)   
 [DATEDIFF &#40; Expressão do SSIS &#41;](../../integration-services/expressions/datediff-ssis-expression.md)   
 [DIA &#40; Expressão do SSIS &#41;](../../integration-services/expressions/day-ssis-expression.md)   
 [MÊS &#40; Expressão do SSIS &#41;](../../integration-services/expressions/month-ssis-expression.md)   
 [ANO &#40; Expressão do SSIS &#41;](../../integration-services/expressions/year-ssis-expression.md)   
 [Funções &#40; Expressão do SSIS &#41;](../../integration-services/expressions/functions-ssis-expression.md)  
  
  
