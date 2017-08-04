---
title: "ANO (expressão SSIS) | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- dates [Integration Services], YEAR
- YEAR function
ms.assetid: 9d88dead-ace8-44b9-b8e2-916c1842e155
caps.latest.revision: 35
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: a72a54b02f136f2d9acc130051e79852d72a2f1f
ms.contentlocale: pt-br
ms.lasthandoff: 08/03/2017

---
# <a name="year-ssis-expression"></a>YEAR (Expressão SSIS)
  Retorna um inteiro que representa o ano da parte da data.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
YEAR(date)  
```  
  
## <a name="arguments"></a>Argumentos  
 *date*  
 É uma data em qualquer formato de data.  
  
## <a name="result-types"></a>Tipos de resultado  
 DT_I4  
  
## <a name="remarks"></a>Comentários  
 YEAR retornará um resultado nulo se o argumento for nulo.  
  
 Um literal de data deve ser convertido explicitamente em um dos tipos de dados de data. Para obter mais informações, consulte [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md).  
  
> [!NOTE]  
>  A expressão não é validada quando um literal de data é convertido explicitamente em um destes tipos de dados de data: DT_DBTIMESTAMPOFFSET e DT_DBTIMESTAMP2.  
  
 A função YEAR é mais resumida, mas equivale a usar a função DATEPART ("Ano", data).  
  
## <a name="expression-examples"></a>Exemplos de expressões  
 Este exemplo retorna o número do ano em um literal de data. Se a data estiver no formato mm/dd/aaaa, este exemplo retornará "2002".  
  
```  
YEAR((DT_DBTIMESTAMP)"11/23/2002")  
```  
  
 Este exemplo retorna o inteiro que representa o ano na coluna **ModifiedDate** .  
  
```  
YEAR(ModifiedDate)  
```  
  
 Este exemplo retorna o inteiro que representa o ano da data atual.  
  
```  
YEAR(GETDATE())  
```  
  
## <a name="see-also"></a>Consulte também  
 [DATEADD &#40; Expressão do SSIS &#41;](../../integration-services/expressions/dateadd-ssis-expression.md)   
 [DATEDIFF &#40; Expressão do SSIS &#41;](../../integration-services/expressions/datediff-ssis-expression.md)   
 [DATEPART &#40; Expressão do SSIS &#41;](../../integration-services/expressions/datepart-ssis-expression.md)   
 [DIA &#40; Expressão do SSIS &#41;](../../integration-services/expressions/day-ssis-expression.md)   
 [MÊS &#40; Expressão do SSIS &#41;](../../integration-services/expressions/month-ssis-expression.md)   
 [Funções &#40; Expressão do SSIS &#41;](../../integration-services/expressions/functions-ssis-expression.md)  
  
  
