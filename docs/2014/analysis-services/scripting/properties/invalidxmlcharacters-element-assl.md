---
title: Elemento InvalidXmlCharacters (ASSL) | Microsoft Docs
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
- InvalidXmlCharacters Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- InvalidXmlCharacters
helpviewer_keywords:
- InvalidXmlCharacters element
ms.assetid: 92b1210c-1075-4f2f-a2c4-dfdc6d7e5c05
caps.latest.revision: 33
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 1a3735beb602045bc4789d716bdf1cb5968af06f
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37229666"
---
# <a name="invalidxmlcharacters-element-assl"></a>Elemento InvalidXmlCharacters (ASSL)
  Especifica o método de manipulação de caracteres XML nos dados de origem que não são válidos.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<DataItem>  
   ...  
   <InvalidXmlCharacters>...</InvalidXmlCharacters>  
   ...  
</DataItem  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Description|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Cadeia de caracteres (enumeração)|  
|Valor padrão|*Preservar*|  
|Cardinalidade|0-1: elemento opcional que pode ocorrer apenas uma única vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elemento pai|[DataItem](../data-type/dataitem-data-type-assl.md)|  
|Elementos filho|Nenhum|  
  
## <a name="remarks"></a>Remarks  
 O valor desse elemento é limitado a uma das cadeias de caracteres listadas na tabela a seguir.  
  
|Valor|Description|  
|-----------|-----------------|  
|*Preservar*|Os caracteres XML inválidos são preservados.|  
|*Remover*|Os caracteres XML inválidos são removidos.|  
|*Substituir*|Os caracteres XML inválidos são substituídos por caracteres de ponto de interrogação (?).|  
  
 A enumeração que corresponde aos valores permitidos para `InvalidXmlCharacters` no objeto Analysis Management Objects (AMO) o modelo é <xref:Microsoft.AnalysisServices.InvalidXmlCharacters>.  
  
## <a name="see-also"></a>Consulte também  
 [Propriedades &#40;ASSL&#41;](properties-assl.md)  
  
  
