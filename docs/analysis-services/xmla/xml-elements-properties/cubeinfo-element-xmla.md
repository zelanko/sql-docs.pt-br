---
title: Elemento CubeInfo (XMLA) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
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
apiname: CubeInfo Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords:
- http://schemas.microsoft.com/analysisservices/2003/engine#CubeInfo
- microsoft.xml.analysis.cubeinfo
- urn:schemas-microsoft-com:xml-analysis#CubeInfo
helpviewer_keywords: CubeInfo element
ms.assetid: a504bac5-4bf2-4f78-a288-e74a34eaa97e
caps.latest.revision: "16"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 86a2b150768f7d5671c599486a4236f9757ef9b7
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="cubeinfo-element-xmla"></a>Elemento CubeInfo (XMLA)
  Contém os metadados de cubo contido pelo pai [OlapInfo](../../../analysis-services/xmla/xml-elements-properties/olapinfo-element-xmla.md) elemento.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<OlapInfo>  
   ...  
   <CubeInfo>  
      <Cube>...</Cube>  
   </CubeInfo>  
   ...  
</OlapInfo>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Descrição|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Nenhuma|  
|Valor padrão|Nenhuma|  
|Cardinalidade|1-1: elemento obrigatório que ocorre apenas uma única vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[OlapInfo](../../../analysis-services/xmla/xml-elements-properties/olapinfo-element-xmla.md)|  
|Elementos filho|[Cube](../../../analysis-services/xmla/xml-elements-properties/cube-element-olapinfo-xmla.md)|  
  
## <a name="remarks"></a>Comentários  
 O **CubeInfo** elemento contém um **cubo** elemento para cada cubo referenciado no conjunto de dados multidimensional.  
  
> [!NOTE]  
>  [!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] retorna um único **cubo** elemento desta coleção porque [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] não dá suporte a instruções que fazem referência a vários cubos na cláusula FROM das expressões multidimensionais ( Linguagem MDX).  
  
## <a name="see-also"></a>Consulte também  
 [Propriedades &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
