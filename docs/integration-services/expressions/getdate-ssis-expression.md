---
title: GETDATE (Expressão SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- current date
- GETDATE function
- dates [Integration Services], GETDATE
ms.assetid: 6d20ec93-3244-4d63-baf6-70eff7bd598c
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: afbbc80ce19c2820d24d65a9caa0736d00e7f8b2
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47833154"
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
  
## <a name="see-also"></a>Consulte Também  
 [GETUTCDATE &#40;Expressão do SSIS&#41;](../../integration-services/expressions/getutcdate-ssis-expression.md)   
 [Funções &#40;Expressão do SSIS&#41;](../../integration-services/expressions/functions-ssis-expression.md)  
  
  
