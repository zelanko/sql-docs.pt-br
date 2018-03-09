---
title: "GETUTCDATE (Expressão SSIS) | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: expressions
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- dates [Integration Services], GETUTCDATE
- current date
- UTC time
- GETUTCDATE function
ms.assetid: 2282339c-c24f-493e-8e66-181ea8af5ad0
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 07df1948bdd1a6d74ef3a858c1823838ab8e07a7
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/25/2018
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
 [GETDATE &#40;Expressão do SSIS&#41;](../../integration-services/expressions/getdate-ssis-expression.md)   
 [Funções &#40;Expressão do SSIS&#41;](../../integration-services/expressions/functions-ssis-expression.md)  
  
  
