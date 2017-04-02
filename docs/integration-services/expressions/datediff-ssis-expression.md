---
title: "DATEDIFF (Express&#227;o SSIS) | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "instrução DATEDIFF"
  - "datas [Integration Services], DATEDIFF"
ms.assetid: 449b327f-47c7-4709-8bc6-4ee9a35cc330
caps.latest.revision: 40
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 40
---
# DATEDIFF (Express&#227;o SSIS)
  Retorna o número de limites de data e hora entre duas datas especificadas. O parâmetro *datepart* identifica quais limites de data e hora serão comparados.  
  
## Sintaxe  
  
```  
  
DATEDIFF(datepart, startdate, endate)  
```  
  
## Argumentos  
 *datepart*  
 É o parâmetro que especifica qual parte da data será comparada e para a qual um valor será retornado.  
  
 *startdate*  
 É a data de início do intervalo.  
  
 *endate*  
 É a data de término do intervalo.  
  
## Tipos de resultado  
 DT_I4  
  
## Comentários  
 A tabela a seguir lista as partes de data e as abreviações reconhecidas pelo avaliador de expressão.  
  
|Datepart|Abreviações|  
|--------------|-------------------|  
|Year|aa, aaaa|  
|Quarter|qq, q|  
|Month|mm, m|  
|Dia do ano|dy, y|  
|Day|dd, d|  
|Week|wk, ww|  
|Dia de semana|dw, w|  
|Hora|Hh|  
|Minuto|mi, n|  
|Segundo|ss, s|  
|Milissegundos|Ms|  
  
 DATEDIFF retornará um resultado nulo se qualquer argumento for nulo.  
  
 Um literal de data deve ser convertido explicitamente em um dos tipos de dados de data. Para obter mais informações, consulte [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md).  
  
 Ocorrerá um erro se uma data não for válida, se a unidade de data ou hora não for uma cadeia de caracteres, se a data de início não for uma data ou se a data de término não for uma data.  
  
 Se a data de término for anterior à data de início, a função retornará um número negativo. Se as datas de início e término forem iguais ou estiverem dentro do mesmo intervalo, a função retornará zero.  
  
## Exemplos de expressões SSIS  
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
  
## Consulte também  
 [DATEADD &#40;Expressão do SSIS&#41;](../../integration-services/expressions/dateadd-ssis-expression.md)   
 [DATEPART &#40;Expressão do SSIS&#41;](../../integration-services/expressions/datepart-ssis-expression.md)   
 [DAY &#40;Expressão do SSIS&#41;](../../integration-services/expressions/day-ssis-expression.md)   
 [MONTH &#40;Expressão do SSIS&#41;](../../integration-services/expressions/month-ssis-expression.md)   
 [YEAR &#40;Expressão do SSIS&#41;](../../integration-services/expressions/year-ssis-expression.md)   
 [Funções &#40;Expressão do SSIS&#41;](../../integration-services/expressions/functions-ssis-expression.md)  
  
  