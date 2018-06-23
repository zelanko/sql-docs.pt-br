---
title: Elemento CellData (XMLA) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- CellData Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- CellData
- http://schemas.microsoft.com/analysisservices/2003/engine#CellData
- urn:schemas-microsoft-com:xml-analysis#CellData
- microsoft.xml.analysis.celldata
helpviewer_keywords:
- CellData element
ms.assetid: 0ebfb5e1-a674-4b9b-bd8c-c529da105f61
caps.latest.revision: 27
author: mgblythe
ms.author: mblythe
manager: mblythe
ms.openlocfilehash: ce445127e78f7f503bf3b81a640047f0d1f1d87f
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36121357"
---
# <a name="celldata-element-xmla"></a>Elemento CellData (XMLA)
  Contém uma coleção de elementos Cell que representam os dados de célula contidos por um elemento [root](root-element-xmla.md) que usa o tipo de dados [MDDataSet](../xml-data-types/mddataset-data-type-xmla.md) .  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<root xmlns="urn:schemas-microsoft-com:xml-analysis:mddataset">  
   ...  
   <CellData>  
      <Cell>...</Cell>  
   </CellData>  
</root>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Description|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Nenhum|  
|Valor padrão|Nenhum|  
|Cardinalidade|0-n: Elemento opcional que pode ocorrer mais de uma vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[root](root-element-xmla.md)|  
|Elementos filho|[célula](cell-element-mddataset-xmla.md)|  
  
## <a name="remarks"></a>Remarks  
 No elemento root pai, o elemento `Axes` é seguido pelo elemento `CellData`, uma coleção de elementos `Cell` que contêm os valores de propriedade de célula para cada célula retornada no conjunto de dados multidimensionais.  
  
## <a name="see-also"></a>Consulte também  
 [Propriedades &#40;XMLA&#41;](xml-elements-properties.md)  
  
  