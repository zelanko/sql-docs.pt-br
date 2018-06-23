---
title: Formatar elemento (ASSL) | Microsoft Docs
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
- Format Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- Format
helpviewer_keywords:
- Format element
ms.assetid: 881ea707-52a7-46f7-ba16-ac2ec44eca22
caps.latest.revision: 35
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: b7434ba5d6e2db8d2a2e665fa333799b6b2e9eb8
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36120675"
---
# <a name="format-element-assl"></a>Elemento Format (ASSL)
  Contém o formato exigido do [DataItem](../data-type/dataitem-data-type-assl.md) elemento.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<DataItem>  
   ...  
   <Format>...</Format>  
      ...  
</DataItem>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Description|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Cadeia de caracteres|  
|Valor padrão|Nenhum|  
|Cardinalidade|0-1: elemento opcional que pode ocorrer apenas uma única vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elemento pai|[O item de dados](../data-type/dataitem-data-type-assl.md)|  
|Elementos filho|Nenhum|  
  
## <a name="remarks"></a>Remarks  
 Valores permitidos para o `Format` elemento são os formatos do Microsoft Office Excel e as cadeias de caracteres *TrimRight*, *TrimLeft*, *TrimAll*, e  *TrimNone*. Para a fragmentação, *TrimRight* é o padrão.  
  
 O valor desse elemento é limitado a uma das cadeias de caracteres listadas na tabela a seguir.  
  
|Valor|Description|  
|-----------|-----------------|  
|Todas a cadeia de caracteres do formato Excel|Os dados são formatados de acordo com o nome ou a cadeia de caracteres de formato personalizada que forem especificados. Qualquer cadeia de caracteres de formato à qual o Excel oferecer suporte pode ser fornecida.|  
|*TrimAll*|Os dados são fragmentados à esquerda e à direita.|  
|*TrimLeft*|Os dados são fragmentados à esquerda.|  
|*TrimNone*|Os dados não são fragmentados.|  
|*TrimRight*|Os dados são fragmentados à direita.|  
  
 O elemento que corresponde ao pai do `Format` no objeto Analysis Management Objects (AMO) o modelo é <xref:Microsoft.AnalysisServices.DataItem>.  
  
## <a name="see-also"></a>Consulte também  
 [Propriedades &#40;ASSL&#41;](properties-assl.md)  
  
  