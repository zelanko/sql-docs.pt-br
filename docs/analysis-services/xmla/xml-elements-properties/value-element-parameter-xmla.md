---
title: "Valor de elemento (parâmetro) (XMLA) | Microsoft Docs"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: xmla
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- Value Element (Parameter)
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- microsoft.xml.analysis.value
- urn:schemas-microsoft-com:xml-analysis#Value
- http://schemas.microsoft.com/analysisservices/2003/engine#Value
helpviewer_keywords:
- Value element
ms.assetid: e590d189-91aa-40c7-8669-09c87812f4ce
caps.latest.revision: 13
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 2f421aec3724eb6359bb0c55f825b4e630580b46
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="value-element-parameter-xmla"></a>Elemento Value (Parâmetro) (XMLA)
  Contém o valor de um parâmetro representado pelo [parâmetro](../../../analysis-services/xmla/xml-elements-properties/parameter-element-xmla.md) elemento.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
<Parameter>  
   ...  
   <Value>...</Value>  
   ...  
</Parameter>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Descrição|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Any (qualquer)|  
|Valor padrão|Nenhuma|  
|Cardinalidade|1-1: elemento obrigatório que ocorre apenas uma única vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[Parâmetro](../../../analysis-services/xmla/xml-elements-properties/parameter-element-xmla.md)|  
|Elementos filho|Nenhuma|  
  
## <a name="remarks"></a>Comentários  
 O **valor** elemento pode armazenar qualquer tipo de XML simples, bem como o XML for Analysis (XMLA) **linhas** tipo de dados, para os parâmetros usados pelos comandos XMLA no [Execute](../../../analysis-services/xmla/xml-elements-methods-execute.md) método.  
  
## <a name="see-also"></a>Consulte também  
 [Propriedades &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  

