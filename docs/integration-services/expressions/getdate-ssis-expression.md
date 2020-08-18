---
description: GETDATE (Expressão SSIS)
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
author: chugugrace
ms.author: chugu
ms.openlocfilehash: d74e82c27fa21070d3932b98304894964b91e3a8
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88348082"
---
# <a name="getdate-ssis-expression"></a>GETDATE (Expressão SSIS)

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  Retorna a data atual do sistema em um formato DT_DBTIMESTAMP. A função GETDATE não usa nenhum argumento.  
  
> [!NOTE]  
>  O comprimento do resultado de retorno da função GETDATE é de 29 caracteres.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
GETDATE()  
```  
  
## <a name="arguments"></a>Argumentos  
 Nenhum  
  
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
  
  
