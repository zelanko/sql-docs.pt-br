---
title: Formatar elemento (ASSL) | Microsoft Docs
ms.date: 5/8/2018
ms.prod: sql
ms.custom: assl
ms.reviewer: owend
ms.technology: analysis-services
ms.topic: reference
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 34220d27f4a0ca1f30b67b5066f5a06877816652
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/10/2018
---
# <a name="format-element-assl"></a>Elemento Format (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
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
  
## <a name="remarks"></a>Remarks  
 Os valores permitidos para o elemento **Format** são os formatos do Microsoft Office Excel e as cadeias de caracteres *TrimRight*, *TrimLeft*, *TrimAll*e *TrimNone*. Para a fragmentação, *TrimRight* é o padrão.  
  
 O valor desse elemento é limitado a uma das cadeias de caracteres listadas na tabela a seguir.  
  
|Valor|Description|  
|-----------|-----------------|  
|Todas a cadeia de caracteres do formato Excel|Os dados são formatados de acordo com o nome ou a cadeia de caracteres de formato personalizada que forem especificados. Qualquer cadeia de caracteres de formato à qual o Excel oferecer suporte pode ser fornecida.|  
|*TrimAll*|Os dados são fragmentados à esquerda e à direita.|  
|*TrimLeft*|Os dados são fragmentados à esquerda.|  
|*TrimNone*|Os dados não são fragmentados.|  
|*TrimRight*|Os dados são fragmentados à direita.|  
  
 O elemento que corresponde ao pai do **formato** no objeto Analysis Management Objects (AMO) o modelo é <xref:Microsoft.AnalysisServices.DataItem>.  
  
## <a name="see-also"></a>Consulte também  
 [Propriedades & #40; ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
