---
title: Valor de elemento (ASSL) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- Value Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- Value
helpviewer_keywords:
- Value element
ms.assetid: a2fad411-73fd-42df-b4e1-df2cb8454182
caps.latest.revision: 36
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 5b31ced28db41575887a07ccf6c6e303aea5aaf1
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="value-element-assl"></a>Elemento Value (ASSL)
  Contém o valor do elemento pai.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<AlgorithmParameter> <!-- or one of the elements listed below in the Element Relationships table -->  
   ...  
   <Value>...</Value>  
   ...  
</AlgorithmParameter>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Descrição|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Consulte a tabela a seguir.|  
|Valor padrão|Nenhuma|  
|Cardinalidade|1-1: elemento obrigatório que ocorre apenas uma única vez.|  
  
|Ancestral ou pai|Tipo de Dados|  
|------------------------|---------------|  
|[AlgorithmParameter](../../../analysis-services/scripting/objects/algorithmparameter-element-assl.md)|Qualquer simpleType|  
|[ServerProperty](../../../analysis-services/scripting/objects/serverproperty-element-assl.md)|Qualquer simpleType|  
|Todos os outros|Cadeia de caracteres|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[AlgorithmParameter](../../../analysis-services/scripting/objects/algorithmparameter-element-assl.md), [anotação](../../../analysis-services/scripting/objects/annotation-element-assl.md), [Kpi](../../../analysis-services/scripting/objects/kpi-element-assl.md), [ReportFormatParameter](../../../analysis-services/scripting/objects/reportformatparameter-element-asl.md), [ReportParameter](../../../analysis-services/scripting/objects/reportparameter-element-assl.md), [ServerProperty](../../../analysis-services/scripting/objects/serverproperty-element-assl.md)|  
|Elementos filho|Nenhuma|  
  
## <a name="remarks"></a>Comentários  
 O **valor** elemento contém o valor associado ao objeto pai. O valor esperado de **valor** elemento varia de acordo com o elemento pai, conforme descrito na tabela a seguir.  
  
|Elemento pai|Valor esperado|  
|--------------------|--------------------|  
|[AlgorithmParameter](../../../analysis-services/scripting/objects/algorithmparameter-element-assl.md)|O valor do parâmetro de algoritmo.|  
|[Anotação](../../../analysis-services/scripting/objects/annotation-element-assl.md)|O valor da anotação.|  
|[KPI](../../../analysis-services/scripting/objects/kpi-element-assl.md)|Uma linguagem MDX usada para calcular o valor do KPI (indicador chave de desempenho).|  
|[ReportFormatParameter](../../../analysis-services/scripting/objects/reportformatparameter-element-asl.md)|O valor do parâmetro de formato de relatório.|  
|[ReportParameter](../../../analysis-services/scripting/objects/reportparameter-element-assl.md)|Uma linguagem MDX usada para calcular o valor do parâmetro de relatório.|  
|[ServerProperty](../../../analysis-services/scripting/objects/serverproperty-element-assl.md)|O valor da propriedade de servidor para a instância que está sendo executada no momento.|  
  
 Os elementos que correspondem aos pais de **valor** no modelo de objeto de Analysis Management Objects (AMO) são <xref:Microsoft.AnalysisServices.AlgorithmParameter>, <xref:Microsoft.AnalysisServices.Annotation>, <xref:Microsoft.AnalysisServices.Kpi>, <xref:Microsoft.AnalysisServices.ReportParameter>, e <xref:Microsoft.AnalysisServices.ServerProperty>.  
  
## <a name="see-also"></a>Consulte também  
 [Propriedades &#40; ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  

