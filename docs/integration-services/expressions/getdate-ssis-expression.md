---
title: "GETDATE (Expressão SSIS) | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: expressions
ms.reviewer: 
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- current date
- GETDATE function
- dates [Integration Services], GETDATE
ms.assetid: 6d20ec93-3244-4d63-baf6-70eff7bd598c
caps.latest.revision: "35"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 3351a9e7d24d039c9dac69c3c92352070e6d22a4
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/20/2017
---
# <a name="getdate-ssis-expression"></a>GETDATE (Expressão SSIS)
  Retorna a data atual do sistema em um formato DT_DBTIMESTAMP. A função GETDATE não usa nenhum argumento.  
  
> [!NOTE]  
>  O comprimento do resultado de retorno da função GETDATE é de 29 caracteres.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
GETDATE()  
```  
  
## <a name="arguments"></a>Argumentos  
 Nenhum.  
  
## <a name="result-types"></a>Tipos de resultado  
 DT_DBTIMESTAMP  
  
## <a name="expression-examples"></a>Exemplos de expressões  
 Este exemplo retorna o ano da data atual.  
  
```  
DATEPART("year",GETDATE())  
```  
  
 Este exemplo retorna o número de dias entre uma data na coluna **ModifiedDate** e a data atual.  
  
```  
DATEDIFF("dd",ModifiedDate,GETDATE())  
```  
  
 Este exemplo acrescenta três meses à data atual.  
  
```  
DATEADD("Month",3,GETDATE())  
```  
  
## <a name="see-also"></a>Consulte também  
 [GETUTCDATE &#40;Expressão do SSIS&#41;](../../integration-services/expressions/getutcdate-ssis-expression.md)   
 [Funções &#40;Expressão do SSIS&#41;](../../integration-services/expressions/functions-ssis-expression.md)  
  
  
