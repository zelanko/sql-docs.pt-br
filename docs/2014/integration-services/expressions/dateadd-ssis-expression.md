---
title: DATEADD (Expressão SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- dates [Integration Services], DATEADD
- dates [Integration Services]
- DATEADD function
ms.assetid: fa5c37b1-2ddc-4857-8f8e-f6d5643b654f
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 3c744d3f28bc27373f3dc9798ba591848d4b720e
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "62769343"
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
  
## <a name="remarks"></a>Comentários  
 A tabela a seguir lista as partes de data e as abreviações reconhecidas pelo avaliador de expressão. Os nomes das partes da data não diferenciam maiúsculas de minúsculas.  
  
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
  
 O argumento *number* deve estar disponível quando a expressão é analisada. O argumento pode ser uma constante ou variável. Você não pode usar valores de coluna porque os valores não são conhecidos quando a expressão é analisada.  
  
 O argumento *datepart* deve estar entre aspas.  
  
 Um literal de data deve ser convertido explicitamente em um dos tipos de dados de data. Para obter mais informações, consulte [Integration Services Data Types](../data-flow/integration-services-data-types.md).  
  
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
 [DATEDIFF &#40;Expressão do SSIS&#41;](datediff-ssis-expression.md)   
 [DATEPART &#40;Expressão do SSIS&#41;](datepart-ssis-expression.md)   
 [DAY &#40;Expressão do SSIS&#41;](day-ssis-expression.md)   
 [MONTH &#40;Expressão do SSIS&#41;](month-ssis-expression.md)   
 [YEAR &#40;Expressão do SSIS&#41;](year-ssis-expression.md)   
 [Funções &#40;Expressão do SSIS&#41;](functions-ssis-expression.md)  
  
  
