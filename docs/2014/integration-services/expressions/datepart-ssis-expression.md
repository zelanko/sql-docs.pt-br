---
title: DATEPART (Expressão SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
helpviewer_keywords:
- dates [Integration Services], DATEPART
- DATEPART function
ms.assetid: 3e590094-fc49-4144-805f-fdc1bf2fe509
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 0e5a5a8b8d9cb15761a35bc01e9d8fe80153b288
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48189056"
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
  
 Um literal de data deve ser convertido explicitamente em um dos tipos de dados de data. Para obter mais informações, consulte [Integration Services Data Types](../data-flow/integration-services-data-types.md).  
  
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
 [DATEADD &#40;expressão do SSIS&#41;](dateadd-ssis-expression.md)   
 [DATEDIFF &#40;expressão do SSIS&#41;](datediff-ssis-expression.md)   
 [DAY &#40;Expressão do SSIS&#41;](day-ssis-expression.md)   
 [MONTH &#40;Expressão do SSIS&#41;](month-ssis-expression.md)   
 [YEAR &#40;Expressão do SSIS&#41;](year-ssis-expression.md)   
 [Funções &#40;expressão do SSIS&#41;](functions-ssis-expression.md)  
  
  
