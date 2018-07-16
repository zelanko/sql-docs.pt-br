---
title: Elemento CreatedTimestamp (ASSL) | Microsoft Docs
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
- CreatedTimestamp Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- CreatedTimestamp
helpviewer_keywords:
- CreatedTimestamp element
ms.assetid: 35f5dd33-ea82-4be3-a117-69136aa9d1a4
caps.latest.revision: 40
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 1bab2bbc51422d6062b5f7df97fd3ff7b17e40c5
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37235616"
---
# <a name="createdtimestamp-element-assl"></a>Elemento CreatedTimestamp (ASSL)
  Contém o carimbo de data e hora de criação somente leitura do elemento pai.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<Assembly> <!-- or one of the elements listed below in the Element Relationships table -->  
   ...  
   <CreatedTimestamp>...</CreatedTimestamp>  
   ...  
</Assembly>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Description|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|DateTime|  
|Valor padrão|Nenhum|  
|Cardinalidade|0-1: elemento opcional que pode ocorrer apenas uma única vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[Assembly](../objects/assembly-element-assl.md), [cubo](../objects/cube-element-assl.md), [banco de dados](../objects/database-element-assl.md), [DataSource](../objects/datasource-element-assl.md), [DataSourceView](../objects/datasourceview-element-assl.md), [dimensão](../objects/dimension-element-assl.md), [MdxScript](../objects/mdxscript-element-assl.md), [MeasureGroup](../objects/group-element-assl.md), [MiningModel](../objects/miningmodel-element-assl.md), [MiningStructure](../objects/miningstructure-element-assl.md), [partição](../objects/partition-element-assl.md), [Permissão](../data-type/permission-data-type-assl.md), [perspectiva](../objects/perspective-element-assl.md)|  
|Elementos filho|Nenhum|  
  
## <a name="remarks"></a>Remarks  
 O `CreatedTimestamp` elemento contém um somente leitura `DateTime` valor que representa a data e hora em que o objeto foi criado em uma determinada instância do [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]. O valor desse elemento não pode ser vazio.  
  
 Os elementos que correspondem aos pais de `CreatedTimestamp` no modelo de objeto Analysis Management Objects (AMO) são <xref:Microsoft.AnalysisServices.Assembly>, <xref:Microsoft.AnalysisServices.Cube>, <xref:Microsoft.AnalysisServices.Database>, <xref:Microsoft.AnalysisServices.DataSource>, <xref:Microsoft.AnalysisServices.DataSourceView>, <xref:Microsoft.AnalysisServices.Dimension>, <xref:Microsoft.AnalysisServices.MdxScript>, <xref:Microsoft.AnalysisServices.MeasureGroup>, <xref:Microsoft.AnalysisServices.MiningModel>, <xref:Microsoft.AnalysisServices.MiningStructure>, <xref:Microsoft.AnalysisServices.Partition>, <xref:Microsoft.AnalysisServices.Permission>, e <xref:Microsoft.AnalysisServices.Perspective>.  
  
## <a name="see-also"></a>Consulte também  
 [Propriedades &#40;ASSL&#41;](properties-assl.md)  
  
  
