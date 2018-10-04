---
title: Consultar o elemento (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- Query Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
helpviewer_keywords:
- Query element
ms.assetid: 832c3337-de6d-43b2-8f1c-75bdba76539b
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 46720600782cb986c0fd99ee50aa21ef729289e3
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48149266"
---
# <a name="query-element-assl"></a>Elemento Query (ASSL)
  Contém o texto da consulta a ser executado para a notificação.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<QueryNotification>  
   <Query>...</Query>  
</QueryNotification>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Description|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Cadeia de caracteres|  
|Valor padrão|None|  
|Cardinalidade|1-1: elemento obrigatório que ocorre apenas uma única vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elemento pai|[QueryNotification](../objects/querynotification-element-assl.md)|  
|Elementos filho|None|  
  
## <a name="remarks"></a>Comentários  
 O elemento que corresponde ao pai de `Query` no objeto Analysis Management Objects (AMO) o modelo é <xref:Microsoft.AnalysisServices.QueryNotification>.  
  
## <a name="see-also"></a>Consulte também  
 [Tipo de dados ProactiveCachingQueryBinding &#40;ASSL&#41;](../data-type/binding-data-type-assl.md)   
 [Propriedades &#40;ASSL&#41;](properties-assl.md)  
  
  
