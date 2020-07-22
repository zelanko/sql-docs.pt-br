---
title: DATEDIFF (Expressão SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- DATEDIFF statement
- dates [Integration Services], DATEDIFF
ms.assetid: 449b327f-47c7-4709-8bc6-4ee9a35cc330
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 2f869de30e8f6b6c65d01cc3189d9e63abfb57e7
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/22/2020
ms.locfileid: "86914732"
---
# <a name="datediff-ssis-expression"></a>DATEDIFF (Expressão SSIS)

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  Retorna o número de limites de data e hora entre duas datas especificadas. O parâmetro *datepart* identifica quais limites de data e hora serão comparados.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
DATEDIFF(datepart, startdate, endate)  
```  
  
## <a name="arguments"></a>Argumentos  
 *datepart*  
 É o parâmetro que especifica qual parte da data será comparada e para a qual um valor será retornado.  
  
 *startdate*  
 É a data de início do intervalo.  
  
 *endate*  
 É a data de término do intervalo.  
  
## <a name="result-types"></a>Tipos de resultado  
 DT_I4  
  
## <a name="remarks"></a>Comentários  
 A tabela a seguir lista as partes de data e as abreviações reconhecidas pelo avaliador de expressão.  
  
|datepart|Abreviações|  
|--------------|-------------------|  
|Ano|aa, aaaa|  
|Quarter|qq, q|  
|Month|mm, m|  
|Dia do ano|dy, y|  
|Dia|dd, d|  
|Semana|wk, ww|  
|Weekday|dw, w|  
|Hora|Hh|  
|Minuto|mi, n|  
|Segundo|ss, s|  
|Milissegundos|Ms|  
  
 DATEDIFF retornará um resultado nulo se qualquer argumento for nulo.  
  
 Um literal de data deve ser convertido explicitamente em um dos tipos de dados de data. Para obter mais informações, consulte [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md).  
  
 Ocorrerá um erro se uma data não for válida, se a unidade de data ou hora não for uma cadeia de caracteres, se a data de início não for uma data ou se a data de término não for uma data.  
  
 Se a data de término for anterior à data de início, a função retornará um número negativo. Se as datas de início e término forem iguais ou estiverem dentro do mesmo intervalo, a função retornará zero.  
  
## <a name="ssis-expression-examples"></a>Exemplos de expressões SSIS  
 Este exemplo calcula o número de dias entre dois literals de data. Se a data estiver no formato "mm/dd/aaaa", a função retornará 7.  
  
```  
DATEDIFF("dd", (DT_DBTIMESTAMP)"8/1/2003", (DT_DBTIMESTAMP)"8/8/2003")  
```  
  
 Este exemplo retorna o número de meses entre um literal de data e a data atual.  
  
```  
DATEDIFF("mm", (DT_DBTIMESTAMP)"8/1/2003",GETDATE())  
```  
  
 Este exemplo retorna o número de semanas entre a data na coluna **ModifiedDate** e a variável **YearEndDate** . Se **YearEndDate** tiver um tipo de dados **date** , nenhuma conversão explícita será necessária.  
  
```  
DATEDIFF("Week", ModifiedDate,@YearEndDate)  
```  
  
## <a name="see-also"></a>Consulte Também  
 [DATEADD &#40;Expressão do SSIS&#41;](../../integration-services/expressions/dateadd-ssis-expression.md)   
 [DATEPART &#40;Expressão do SSIS&#41;](../../integration-services/expressions/datepart-ssis-expression.md)   
 [DAY &#40;Expressão do SSIS&#41;](../../integration-services/expressions/day-ssis-expression.md)   
 [MONTH &#40;Expressão do SSIS&#41;](../../integration-services/expressions/month-ssis-expression.md)   
 [YEAR &#40;Expressão do SSIS&#41;](../../integration-services/expressions/year-ssis-expression.md)   
 [Funções &#40;Expressão do SSIS&#41;](../../integration-services/expressions/functions-ssis-expression.md)  
  
  
