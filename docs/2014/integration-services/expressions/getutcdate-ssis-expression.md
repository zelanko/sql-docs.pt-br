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
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 8a124f6149a56240b62f72e06281ebbc1405d9e3
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84966596"
---
# <a name="getutcdate-ssis-expression"></a>GETUTCDATE (Expressão SSIS)
  Retorna a data atual do sistema na hora UTC (Universal Time Coordinate ou Greenwich Mean Time) por meio de um formato DT_DBTIMESTAMP. A função GETUTCDATE não pega nenhum argumento.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
GETUTCDATE()  
```  
  
## <a name="arguments"></a>Argumentos  
 Nenhum  
  
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
  
## <a name="see-also"></a>Consulte Também  
 [GETDATE &#40;Expressão do SSIS&#41;](getdate-ssis-expression.md)   
 [Funções &#40;Expressão do SSIS&#41;](functions-ssis-expression.md)  
  
  
