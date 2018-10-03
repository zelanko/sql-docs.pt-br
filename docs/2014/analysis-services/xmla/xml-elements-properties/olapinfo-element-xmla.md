---
title: Elemento OlapInfo (XMLA) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- OlapInfo Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- http://schemas.microsoft.com/analysisservices/2003/engine#OlapInfo
- microsoft.xml.analysis.olapinfo
- urn:schemas-microsoft-com:xml-analysis#OlapInfo
- OLAPInfo
helpviewer_keywords:
- OlapInfo element
ms.assetid: 8828fdd7-c0f7-48ce-a0d0-ab4bc1a995cf
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 39cabfd1ce5e0dcbc815d1cc659fd4a4594be47b
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48050686"
---
# <a name="olapinfo-element-xmla"></a>Elemento OlapInfo (XMLA)
  Contém os metadados de célula e eixo contidos por um [raiz](root-element-xmla.md) elemento que usa o [MDDataSet](../xml-data-types/mddataset-data-type-xmla.md) tipo de dados.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<root xmlns="urn:schemas-microsoft-com:xml-analysis:mddataset">  
   ...  
   <OlapInfo>  
      <CubeInfo>...</CubeInfo>  
      <AxesInfo>...</AxesInfo>  
      <CellInfo>...</CellInfo>  
   </OlapInfo>  
   ...  
</root>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Description|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|None|  
|Valor padrão|None|  
|Cardinalidade|1-1: elemento obrigatório que ocorre apenas uma única vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[root](root-element-xmla.md)|  
|Elementos filho|[AxesInfo](axesinfo-element-xmla.md), [CellInfo](cellinfo-element-xmla.md), [CubeInfo](cubeinfo-element-xmla.md)|  
  
## <a name="remarks"></a>Comentários  
 A seção `OLAPInfo` de um elemento `root` que usa o tipo de dados `MDDataSet` fornece os metadados sobre o cubo, os eixos do resultado multidimensional e as propriedades das células que incluíram o resultado.  
  
## <a name="see-also"></a>Consulte também  
 [Propriedades &#40;XMLA&#41;](xml-elements-properties.md)  
  
  
