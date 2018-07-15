---
title: Elemento root (XMLA) | Microsoft Docs
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
- Root Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- http://schemas.microsoft.com/analysisservices/2003/engine#root
- urn:schemas-microsoft-com:xml-analysis#root
- microsoft.xml.analysis.root
helpviewer_keywords:
- root element
ms.assetid: ecd9d6e8-b16c-4d62-9a87-107c413a0056
caps.latest.revision: 16
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 11045be6946a5a73f0ad86fdcfcc53610800a6c4
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37321076"
---
# <a name="root-element-xmla"></a>Elemento root (XMLA)
  Contém um resultado retornado pelo [Discover](../xml-elements-methods-discover.md) método ou um comando XML for Analysis (XMLA) executado usando o [Execute](../xml-elements-methods-execute.md) método.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<return> <!-- or results-->  
   ...  
   <root xmlns="urn:schemas-microsoft-com:xml-analysis:mddataset">...</root> <!-- for Execute method only -->  
   <!-- or -->  
   <root xmlns="urn:schemas-microsoft-com:xml-analysis:rowset">...</root>  
   <!-- or -->  
   <root xmlns= xmlns="urn:schemas-microsoft-com:xml-analysis:empty">...</root>  
   ...  
</return>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Description|  
|--------------------|-----------------|  
|Valor padrão|Nenhum|  
|Cardinalidade|1-n: elemento obrigatório que pode ocorrer mais de uma vez.|  
  
## <a name="data-type-and-length"></a>Comprimento e tipo de dados  
  
|Ancestor|Tipo de dados|  
|--------------|---------------|  
|[DiscoverResponse](../xml-data-types/rowset-data-type-xmla.md), [olapxmla_EmptyResult](../xml-data-types/emptyresult-data-type-xmla.md)|  
|[ExecuteResponse](../xml-data-types/mddataset-data-type-xmla.md), [conjunto de linhas](../xml-data-types/rowset-data-type-xmla.md), [olapxmla_EmptyResult](../xml-data-types/emptyresult-data-type-xmla.md)|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[resultados](results-element-xmla.md), [retornar](return-element-xmla.md)|  
|Elementos filho|Nenhum|  
  
## <a name="remarks"></a>Remarks  
 O `root` elemento contém as informações retornadas em qualquer um os [DiscoverResponse](../xml-elements-objects-discoverresponse.md) elemento retornado por uma única `Discover` chamada de método, ou nos [ExecuteResponse](../xml-elements-objects-executeresponse.md) elemento retornado por um único comando XMLA executado por um único `Execute` chamada de método.  
  
## <a name="see-also"></a>Consulte também  
 [Propriedades &#40;XMLA&#41;](xml-elements-properties.md)  
  
  
