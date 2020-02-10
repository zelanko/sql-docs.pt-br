---
title: MONTH (Expressão SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- dates [Integration Services], MONTH
- MONTH function
ms.assetid: b5a47a11-c2ef-49bd-bd70-235632ff7bf6
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 2f5e997f40f5af0a9f1c5cd0de4114714a1db8b2
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "62897523"
---
# <a name="month-ssis-expression"></a>MONTH (Expressão SSIS)
  Retorna um número inteiro que representa a parte do mês de uma data.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
MONTH(date)  
```  
  
## <a name="arguments"></a>Argumentos  
 *date*  
 É uma data em qualquer formato de data.  
  
## <a name="result-types"></a>Tipos de resultado  
 DT_I4  
  
## <a name="remarks"></a>Comentários  
 MONTH retornará um resultado nulo se o argumento for nulo.  
  
 Um literal de data deve ser convertido explicitamente em um dos tipos de dados de data. Para obter mais informações, consulte [Integration Services Data Types](../data-flow/integration-services-data-types.md).  
  
> [!NOTE]  
>  A expressão não é validada quando um literal de data é convertido explicitamente em um destes tipos de dados de data: DT_DBTIMESTAMPOFFSET e DT_DBTIMESTAMP2.  
  
 A função MONTH é mais resumida, mas equivale a usar DATEPART ("Mês", data).  
  
## <a name="expression-examples"></a>Exemplos de expressões  
 Este exemplo retorna o número do mês em um literal de data. Se a data estiver no formato "mm/dd/aaaa", este exemplo retornará 11.  
  
```  
MONTH((DT_DBTIMESTAMP)"11/23/2002")  
```  
  
 Este exemplo retorna o inteiro que representa o mês na coluna **ModifiedDate** .  
  
```  
MONTH(ModifiedDate)  
```  
  
 Este exemplo retorna o inteiro que representa o mês da data atual.  
  
```  
MONTH(GETDATE())  
```  
  
## <a name="see-also"></a>Consulte Também  
 [DATEADD &#40;Expressão do SSIS&#41;](dateadd-ssis-expression.md)   
 [DATEDIFF &#40;Expressão do SSIS&#41;](datediff-ssis-expression.md)   
 [DATEPART &#40;Expressão do SSIS&#41;](datepart-ssis-expression.md)   
 [DAY &#40;Expressão do SSIS&#41;](day-ssis-expression.md)   
 [YEAR &#40;Expressão do SSIS&#41;](year-ssis-expression.md)   
 [Funções &#40;Expressão do SSIS&#41;](functions-ssis-expression.md)  
  
  
