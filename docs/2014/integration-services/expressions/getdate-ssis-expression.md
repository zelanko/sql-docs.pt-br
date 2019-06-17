---
title: GETDATE (Expressão SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- current date
- GETDATE function
- dates [Integration Services], GETDATE
ms.assetid: 6d20ec93-3244-4d63-baf6-70eff7bd598c
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 83d8d4126ff7dbcd6e0d5b114626cd8acb1b8d20
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62769022"
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
 None  
  
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
 [GETUTCDATE &#40;Expressão do SSIS&#41;](getutcdate-ssis-expression.md)   
 [Funções &#40;Expressão do SSIS&#41;](functions-ssis-expression.md)  
  
  
