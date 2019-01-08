---
title: GETUTCDATE (Expressão SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- dates [Integration Services], GETUTCDATE
- current date
- UTC time
- GETUTCDATE function
ms.assetid: 2282339c-c24f-493e-8e66-181ea8af5ad0
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 9dfddc692246050d97893141715b105fc017b46f
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/03/2018
ms.locfileid: "52779098"
---
# <a name="getutcdate-ssis-expression"></a>GETUTCDATE (Expressão SSIS)
  Retorna a data atual do sistema na hora UTC (Universal Time Coordinate ou Greenwich Mean Time) por meio de um formato DT_DBTIMESTAMP. A função GETUTCDATE não pega nenhum argumento.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
GETUTCDATE()  
```  
  
## <a name="arguments"></a>Argumentos  
 None  
  
## <a name="result-types"></a>Tipos de resultado  
 DT_DBTIMESTAMP  
  
## <a name="expression-examples"></a>Exemplos de expressões  
 Este exemplo retorna o ano da data atual em hora de UTC.  
  
```  
DATEPART("year",GETUTCDATE())  
```  
  
 Este exemplo retorna o número de dias entre uma data na coluna **ModifiedDate** e a data atual em UTC.  
  
```  
DATEDIFF("dd",ModifiedDate,GETUTCDATE())  
```  
  
 Este exemplo acrescenta três meses à data atual em UTC.  
  
```  
DATEADD("Month",3,GETUTCDATE())  
```  
  
## <a name="see-also"></a>Consulte também  
 [GETDATE &#40;Expressão do SSIS&#41;](getdate-ssis-expression.md)   
 [Funções &#40;Expressão do SSIS&#41;](functions-ssis-expression.md)  
  
  
