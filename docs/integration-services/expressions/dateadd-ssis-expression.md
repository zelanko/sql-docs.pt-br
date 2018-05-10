---
title: DATEADD (Expressão SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.component: expressions
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- dates [Integration Services], DATEADD
- dates [Integration Services]
- DATEADD function
ms.assetid: fa5c37b1-2ddc-4857-8f8e-f6d5643b654f
caps.latest.revision: 36
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 02306ac6da7ac6feefa4684206ddf002e8e08939
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="dateadd-ssis-expression"></a>DATEADD (Expressão SSIS)
  Retorna um novo valor DT_DBTIMESTAMP depois de adicionar um número que representa um intervalo de data ou hora para a parte especificada na data. O parâmetro de número deve ser avaliado como um inteiro e o parâmetro de data deve ser avaliado como uma data válida.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
DATEADD(datepart, number, date)  
```  
  
## <a name="arguments"></a>Argumentos  
 *datepart*  
 É o parâmetro que especifica à qual parte da data deve-se adicionar um número.  
  
 *number*  
 É o valor usado para incrementar *datepart*. O valor deve ser um valor inteiro conhecido quando a expressão é analisada.  
  
 *date*  
 É uma expressão que retorna uma data válida ou uma cadeia de caracteres em formato de data.  
  
## <a name="result-types"></a>Tipos de resultado  
 DT_DBTIMESTAMP  
  
## <a name="remarks"></a>Remarks  
 A tabela a seguir lista as partes de data e as abreviações reconhecidas pelo avaliador de expressão. Os nomes das partes da data não diferenciam maiúsculas de minúsculas.  
  
|datepart|Abreviações|  
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
  
 O argumento *number* deve estar disponível quando a expressão é analisada. O argumento pode ser uma constante ou variável. Você não pode usar valores de coluna porque os valores não são conhecidos quando a expressão é analisada.  
  
 O argumento *datepart* deve estar entre aspas.  
  
 Um literal de data deve ser convertido explicitamente em um dos tipos de dados de data. Para obter mais informações, consulte [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md).  
  
 DATEADD retornará um resultado nulo se o argumento for nulo.  
  
 Ocorrerão erros se uma data for inválida, se a unidade de data ou hora não for uma cadeia de caracteres ou se o incremento não for um inteiro estático.  
  
## <a name="ssis-expression-examples"></a>Exemplos de expressões SSIS  
 Esse exemplo adiciona um mês à data atual.  
  
```  
DATEADD("Month", 1,GETDATE())  
```  
  
 Esse exemplo adiciona 21 dias às datas na coluna **ModifiedDate** .  
  
```  
DATEADD("day", 21, ModifiedDate)  
```  
  
 Esse exemplo adiciona 2 anos a uma data literal.  
  
```  
DATEADD("yyyy", 2, (DT_DBTIMESTAMP)"8/6/2003")  
```  
  
## <a name="see-also"></a>Consulte Também  
 [DATEDIFF &#40;Expressão do SSIS&#41;](../../integration-services/expressions/datediff-ssis-expression.md)   
 [DATEPART &#40;Expressão do SSIS&#41;](../../integration-services/expressions/datepart-ssis-expression.md)   
 [DAY &#40;Expressão do SSIS&#41;](../../integration-services/expressions/day-ssis-expression.md)   
 [MONTH &#40;Expressão do SSIS&#41;](../../integration-services/expressions/month-ssis-expression.md)   
 [YEAR &#40;Expressão do SSIS&#41;](../../integration-services/expressions/year-ssis-expression.md)   
 [Funções &#40;Expressão do SSIS&#41;](../../integration-services/expressions/functions-ssis-expression.md)  
  
  
