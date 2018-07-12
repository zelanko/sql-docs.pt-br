---
title: Elemento Parameters (XMLA) | Microsoft Docs
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
- Parameters Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- http://schemas.microsoft.com/analysisservices/2003/engine#Parameters
- urn:schemas-microsoft-com:xml-analysis#Parameters
- microsoft.xml.analysis.parameters
helpviewer_keywords:
- Parameters element
ms.assetid: d46454a1-a1d1-4aa8-95ea-54be22a53e83
caps.latest.revision: 11
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 87836c6ca9f33c100b3ba10ba91379370e787773
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37158857"
---
# <a name="parameters-element-xmla"></a>Elemento Parameters (XMLA)
  Contém uma coleção de [parâmetro](parameter-element-xmla.md) elementos usados pelo [Execute](../xml-elements-methods-execute.md) método.  
  
 **Namespace:** `urn:schemas-microsoft-com:xml-analysis`  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
<Execute>  
...  
   <Parameters>  
      <Parameter>...</Parameter>  
   </Parameters>  
...  
</Execute>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Description|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Nenhum|  
|Valor padrão|Nenhum|  
|Cardinalidade|0-1: elemento opcional que pode ocorrer apenas uma única vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[Executar](../xml-elements-methods-execute.md)|  
|Elementos filho|[Parâmetro](parameter-element-xmla.md)|  
  
## <a name="remarks"></a>Remarks  
 Alguns comandos do XMLA (XML for Analysis), como o comando [Process](../xml-elements-commands/process-element-xmla.md) , podem requerer informações adicionais. O elemento `Parameters` fornece um mecanismo para fornecer informações adicionais, incluindo partes de informações, de um comando XMLA.  
  
 Se o comando do XMLA não usar o elemento `Parameters`, o elemento pode ser omitido ao chamar o método `Execute`.  
  
## <a name="see-also"></a>Consulte também  
 [Propriedades &#40;XMLA&#41;](xml-elements-properties.md)  
  
  
