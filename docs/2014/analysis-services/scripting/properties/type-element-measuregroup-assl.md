---
title: Tipo de elemento (MeasureGroup) (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- Type Element (MeasureGroup)
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- TYPE
helpviewer_keywords:
- Type element
ms.assetid: 3a584baf-36bb-4e1d-9128-c4758c0b8f06
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 56824f759d6ab5de864a4b64d26371034a69585e
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48191286"
---
# <a name="type-element-measuregroup-assl"></a>Elemento Type (MeasureGroup) (ASSL)
  Especifica o tipo dos [MeasureGroup](../objects/group-element-assl.md).  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<MeasureGroup>  
   ...  
   <Type>...</Type>  
   ...  
</MeasureGroup>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Description|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Cadeia de caracteres (enumeração)|  
|Valor padrão|*Regular*|  
|Cardinalidade|0-1: elemento opcional que pode ocorrer apenas uma única vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elemento pai|[MeasureGroup](../objects/group-element-assl.md)|  
|Elementos filho|None|  
  
## <a name="remarks"></a>Comentários  
 O valor desse elemento é limitado a uma das cadeias de caracteres listadas na tabela a seguir.  
  
|Valor|Description|  
|-----------|-----------------|  
|*Regular*|Contém medidas regulares.|  
|*ExchangeRate*|Contém medidas de taxa de câmbio estrangeira.|  
|*Vendas*|Contém medidas de vendas.|  
|*Orçamento*|Contém medidas de orçamento.|  
|*FinancialReporting*|Contém medidas de relatórios financeiros.|  
|*De marketing*|Contém medidas de comercialização.|  
|*Inventário*|Contém medidas de inventário.|  
  
 A enumeração que corresponde aos valores permitidos para `Type` no objeto Analysis Management Objects (AMO) o modelo é <xref:Microsoft.AnalysisServices.MeasureGroupType>.  
  
 O elemento que corresponde ao pai de `Type` no objeto Analysis Management Objects (AMO) o modelo é <xref:Microsoft.AnalysisServices.MeasureGroup>.  
  
## <a name="see-also"></a>Consulte também  
 [Propriedades &#40;ASSL&#41;](properties-assl.md)  
  
  
