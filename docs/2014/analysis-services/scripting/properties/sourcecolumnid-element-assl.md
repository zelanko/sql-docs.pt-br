---
title: Elemento SourceColumnID (ASSL) | Microsoft Docs
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
- SourceColumnID Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- SourceColumnID
helpviewer_keywords:
- SourceColumnID element
ms.assetid: 715c0be7-aa07-4dff-a909-9738224941ec
caps.latest.revision: 35
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 523977b881e9e8357b32cd606252d0a758d3b46a
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37281772"
---
# <a name="sourcecolumnid-element-assl"></a>Elemento SourceColumnID (ASSL)
  Contém o identificador (ID) da coluna de estrutura de mineração de origem no ancestral [MiningStructure](../objects/miningstructure-element-assl.md) elemento.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<MiningModelColumn>  
   ...  
   <SourceColumnID>...</SourceColumnID>  
   ...  
</MiningModelColumn>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Description|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Cadeia de caracteres|  
|Valor padrão|Nenhum|  
|Cardinalidade|1-1: elemento obrigatório que ocorre apenas uma única vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elemento pai|[MiningModelColumn](../data-type/miningmodelcolumn-data-type-assl.md)|  
|Elementos filho|Nenhum|  
  
## <a name="remarks"></a>Remarks  
 O valor da `SourceColumnID` elemento corresponde ao identificador de uma coluna de estrutura de mineração em de [colunas](../collections/columns-element-assl.md) coleção do pai `MiningStructure`.  
  
 O elemento que corresponde ao pai de `SourceColumnID` no objeto Analysis Management Objects (AMO) o modelo é <xref:Microsoft.AnalysisServices.MiningModelColumn>.  
  
## <a name="see-also"></a>Consulte também  
 [Propriedades &#40;ASSL&#41;](properties-assl.md)  
  
  
