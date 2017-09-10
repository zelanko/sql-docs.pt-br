---
title: Formatar elemento (ASSL) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- Format Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- Format
helpviewer_keywords:
- Format element
ms.assetid: 881ea707-52a7-46f7-ba16-ac2ec44eca22
caps.latest.revision: 35
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: fb34b3f3f32492abb36a9f1bb6d645596493bfbc
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="format-element-assl"></a>Elemento Format (ASSL)
  Contém o formato exigido do [DataItem](../../../analysis-services/scripting/data-type/dataitem-data-type-assl.md) elemento.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<DataItem>  
   ...  
   <Format>...</Format>  
      ...  
</DataItem>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Descrição|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|String|  
|Valor padrão|Nenhuma|  
|Cardinalidade|0-1: elemento obrigatório que pode ocorrer apenas uma vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elemento pai|[O item de dados](../../../analysis-services/scripting/data-type/dataitem-data-type-assl.md)|  
|Elementos filho|Nenhuma|  
  
## <a name="remarks"></a>Comentários  
 Os valores permitidos para o elemento **Format** são os formatos do Microsoft Office Excel e as cadeias de caracteres *TrimRight*, *TrimLeft*, *TrimAll*e *TrimNone*. Para a fragmentação, *TrimRight* é o padrão.  
  
 O valor desse elemento é limitado a uma das cadeias de caracteres listadas na tabela a seguir.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|Todas a cadeia de caracteres do formato Excel|Os dados são formatados de acordo com o nome ou a cadeia de caracteres de formato personalizada que forem especificados. Qualquer cadeia de caracteres de formato à qual o Excel oferecer suporte pode ser fornecida.|  
|*TrimAll*|Os dados são fragmentados à esquerda e à direita.|  
|*TrimLeft*|Os dados são fragmentados à esquerda.|  
|*TrimNone*|Os dados não são fragmentados.|  
|*TrimRight*|Os dados são fragmentados à direita.|  
  
 O elemento que corresponde ao pai do **formato** no objeto Analysis Management Objects (AMO) o modelo é <xref:Microsoft.AnalysisServices.DataItem>.  
  
## <a name="see-also"></a>Consulte também  
 [Propriedades &#40; ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
