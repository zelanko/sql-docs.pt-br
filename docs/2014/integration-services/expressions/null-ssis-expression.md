---
title: NULL (expressão SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- NULL function
- null values [Integration Services]
ms.assetid: df144237-3fbb-41ac-8624-efd92b6522b9
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 379706092613ae7fa3f53fccb493bf756d656b01
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/03/2018
ms.locfileid: "52823290"
---
# <a name="null-ssis-expression"></a>NULL (Expressão SSIS)
  Retorna um valor nulo de um tipo de dados solicitado.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
NULL(typespec)  
```  
  
## <a name="arguments"></a>Argumentos  
 *typespec*  
 É um tipo de dados válido. Para obter mais informações, consulte [Integration Services Data Types](../data-flow/integration-services-data-types.md).  
  
## <a name="result-types"></a>Tipos de resultado  
 Qualquer tipo de dados válido com um valor nulo.  
  
## <a name="remarks"></a>Comentários  
 NULL retornará um resultado nulo se o argumento for nulo.  
  
 Os parâmetros são exigidos para solicitar um valor nulo para alguns tipos de dados. A tabela a seguir lista esses tipos de dados e seus parâmetros.  
  
|Tipo de dados|Parâmetro|Exemplo|  
|---------------|---------------|-------------|  
|DT_STR|*charcount*<br /><br /> *codepage*|(DT_STR,30,1252) converte 30 caracteres para o tipo de dados de DT_STR usando a página de código 1252.|  
|DT_WSTR|*charcount*|(DT_WSTR,20) converte 20 caracteres para o tipo de dados de DT_WSTR.|  
|DT_BYTES|*bytecount*|(DT_BYTES,50) converte 50 bytes para o tipo de dados de DT_BYTES.|  
|DT_DECIMAL|*scale*|(DT_DECIMAL,2) converte um valor numérico para o tipo de dados DT_DECIMAL usando uma escala de 2.|  
|DT_NUMERIC|*precisão*<br /><br /> *scale*|(DT_NUMERIC,10,3) converte um valor numérico para o tipo de dados DT_NUMERIC usando uma precisão de 10 e uma escala de 3.|  
|DT_TEXT|*codepage*|(DT_TEXT,1252) converte um valor para o tipo de dados DT_TEXT usando a página de código 1252.|  
  
## <a name="expression-examples"></a>Exemplos de expressões  
 Esses exemplos retornam o valor nulo dos tipos de dados: DT_STR, DT_DATE e DT_BOOL.  
  
```  
NULL(DT_STR,10,1252)  
NULL(DT_DATE)  
NULL(DT_BOOL)  
```  
  
## <a name="see-also"></a>Consulte também  
 [ISNULL &#40;Expressão SSIS&#41;](null-ssis-expression.md)   
 [Funções &#40;Expressão do SSIS&#41;](functions-ssis-expression.md)  
  
  
