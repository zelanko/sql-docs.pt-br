---
title: Valor de elemento (ASSL) | Microsoft Docs
ms.date: 5/8/2018
ms.prod: sql
ms.component: assl
ms.reviewer: owend
ms.technology: analysis-services
ms.topic: reference
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 262bdf0348f3270c88eed90c31524626502e4a87
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/10/2018
---
# <a name="value-element-assl"></a>Elemento Value (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
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
|Comprimento e tipo de dados|Veja a tabela abaixo.|  
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
  
## <a name="remarks"></a>Remarks  
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
 [Propriedades & #40; ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
