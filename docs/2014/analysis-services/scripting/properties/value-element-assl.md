---
title: Valor de elemento (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- Value Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- Value
helpviewer_keywords:
- Value element
ms.assetid: a2fad411-73fd-42df-b4e1-df2cb8454182
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: d338b8607d8515bf89183eeadd24252c55af8fc5
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48218186"
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
  
|Característica|Description|  
|--------------------|-----------------|  
|Valor padrão|None|  
|Cardinalidade|1-1: elemento obrigatório que ocorre apenas uma única vez.|  
  
|Ancestral ou pai|Tipo de Dados|  
|------------------------|---------------|  
|[AlgorithmParameter](../objects/algorithmparameter-element-assl.md)|Qualquer simpleType|  
|[ServerProperty](../objects/serverproperty-element-assl.md)|Qualquer simpleType|  
|Todos os outros|Cadeia de caracteres|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[AlgorithmParameter](../objects/algorithmparameter-element-assl.md), [anotação](../objects/annotation-element-assl.md), [Kpi](../objects/kpi-element-assl.md), [ReportFormatParameter](../objects/reportformatparameter-element-asl.md), [ReportParameter](../objects/reportparameter-element-assl.md), [ServerProperty](../objects/serverproperty-element-assl.md)|  
|Elementos filho|None|  
  
## <a name="remarks"></a>Comentários  
 O elemento `Value` contém o valor associado ao objeto pai. O valor esperado do elemento `Value` varia, dependendo do elemento pai, conforme descrito na tabela seguinte.  
  
|Elemento pai|Valor esperado|  
|--------------------|--------------------|  
|[AlgorithmParameter](../objects/algorithmparameter-element-assl.md)|O valor do parâmetro de algoritmo.|  
|[Anotação](../objects/annotation-element-assl.md)|O valor da anotação.|  
|[KPI](../objects/kpi-element-assl.md)|Uma linguagem MDX usada para calcular o valor do KPI (indicador chave de desempenho).|  
|[ReportFormatParameter](../objects/reportformatparameter-element-asl.md)|O valor do parâmetro de formato de relatório.|  
|[ReportParameter](../objects/reportparameter-element-assl.md)|Uma linguagem MDX usada para calcular o valor do parâmetro de relatório.|  
|[ServerProperty](../objects/serverproperty-element-assl.md)|O valor da propriedade de servidor para a instância que está sendo executada no momento.|  
  
 Os elementos que correspondem aos pais de `Value` no modelo de objeto AMO (Objetos de Gerenciamento de Análise)são <xref:Microsoft.AnalysisServices.AlgorithmParameter>, <xref:Microsoft.AnalysisServices.Annotation>, <xref:Microsoft.AnalysisServices.Kpi>, <xref:Microsoft.AnalysisServices.ReportParameter> e <xref:Microsoft.AnalysisServices.ServerProperty>.  
  
## <a name="see-also"></a>Consulte também  
 [Propriedades &#40;ASSL&#41;](properties-assl.md)  
  
  
