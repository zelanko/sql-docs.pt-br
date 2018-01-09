---
title: Elemento AxisInfo (XMLA) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
apiname: AxisInfo Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords:
- urn:schemas-microsoft-com:xml-analysis#AxisInfo
- microsoft.xml.analysis.axisinfo
- http://schemas.microsoft.com/analysisservices/2003/engine#AxisInfo
helpviewer_keywords: AxisInfo element
ms.assetid: 060741db-b2ec-4174-9277-58d996440a88
caps.latest.revision: "12"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: ad12131fe961f279bf0d670d91ab03900a8a6ad1
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/08/2018
---
# <a name="axisinfo-element-xmla"></a>Elemento AxisInfo (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]Representa os metadados de um único eixo contido pelo pai [AxesInfo](../../../analysis-services/xmla/xml-elements-properties/axesinfo-element-xmla.md) elemento.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<AxesInfo>  
   ...  
   <AxisInfo name="string">  
      <HierarchyInfo>...</HierarchyInfo>  
   </AxisInfo>  
   ...  
</AxesInfo>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Description|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Nenhum|  
|Valor padrão|Nenhum|  
|Cardinalidade|1-n: elemento obrigatório que pode ocorrer mais de uma vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[AxesInfo](../../../analysis-services/xmla/xml-elements-properties/axesinfo-element-xmla.md)|  
|Elementos filho|[HierarchyInfo](../../../analysis-services/xmla/xml-elements-properties/hierarchyinfo-element-xmla.md)|  
  
## <a name="attributes"></a>Atributos  
  
|attribute|Description|  
|---------------|-----------------|  
|Nome|Atributo **String** obrigatório. O nome do eixo.|  
  
## <a name="remarks"></a>Remarks  
 Em um **raiz** elemento que usa o **MDDataSet** objeto, um **AxisInfo** elemento contém uma coleção de **HierarchyInfo** elementos que , combinado com o valor da **nome** atributo, representa a definição de um único eixo retornada no conjunto de dados multidimensional.  
  
## <a name="see-also"></a>Consulte Também  
 [Propriedades &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
