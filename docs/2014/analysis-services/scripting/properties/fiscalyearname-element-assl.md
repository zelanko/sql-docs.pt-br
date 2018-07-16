---
title: Elemento FiscalYearName (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- FiscalYearName Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- FiscalYearName
helpviewer_keywords:
- FiscalYearName element
ms.assetid: ce613a21-6890-4796-aac5-b029eca46255
caps.latest.revision: 30
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 2564345c916d73c5984be851523a234d2be6bbe4
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37197886"
---
# <a name="fiscalyearname-element-assl"></a>Elemento FiscalYearName (ASSL)
  Define a convenção de nomenclatura para o nome do ano fiscal para um [TimeBinding](../data-type/binding-data-type-assl.md) elemento.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<TimeBinding>  
   ...  
   <FiscalYearName>...</FiscalYearName>  
   ...  
</TimeBinding>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Description|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Cadeia de caracteres (enumeração)|  
|Valor padrão|*NextCalendarYearName*|  
|Cardinalidade|0-1: elemento opcional que pode ocorrer apenas uma única vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elemento pai|[TimeBinding](../data-type/binding-data-type-assl.md)|  
|Elementos filho|Nenhum|  
  
## <a name="remarks"></a>Remarks  
 O valor desse elemento é limitado a uma das cadeias de caracteres listadas na tabela a seguir.  
  
|Valor|Description|  
|-----------|-----------------|  
|*CalendarYearName*|Atribui o nome do ano fiscal do ano civil atual.|  
|*NextCalendarYearName*|Atribui o nome do ano fiscal do próximo ano civil.|  
  
 A enumeração que corresponde aos valores permitidos para `FiscalYearName` no objeto Analysis Management Objects (AMO) o modelo é <xref:Microsoft.AnalysisServices.FiscalYearName>.  
  
## <a name="see-also"></a>Consulte também  
 [Propriedades &#40;ASSL&#41;](properties-assl.md)  
  
  
