---
title: Tipo de dados DSVTableBinding (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- DSVTableBinding Data Type
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- DSVTableBinding
helpviewer_keywords:
- DSVTableBinding data type
ms.assetid: 149e753f-6218-4805-9223-7155b6827e64
caps.latest.revision: 41
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: b6fa9a8d96e9a73531a76db9f96d19bbd1a98796
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="dsvtablebinding-data-type-assl"></a>Tipo de dados DSVTableBinding (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Define um tipo de dados derivado que representa a associação entre uma tabela e um elemento [DataSourceView](../../../analysis-services/scripting/objects/datasourceview-element-assl.md) .  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<DSVTableBinding>  
   <!-- The following elements extend TabularBinding -->  
   <DataSourceViewID>...</DataSourceViewID>  
   <TableID>...</TableID>  
</DSVTableBinding>  
```  
  
## <a name="data-type-characteristics"></a>Características do tipo de dados  
  
|Característica|Descrição|  
|--------------------|-----------------|  
|Tipos de dados base|[TabularBinding](../../../analysis-services/scripting/data-type/tabularbinding-data-type-assl.md)|  
|Tipos de dados derivados|Nenhuma|  
  
## <a name="data-type-relationships"></a>Relação do tipo de dados  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|Nenhuma|  
|Elementos filho|[DataSourceViewID](../../../analysis-services/scripting/properties/datasourceviewid-element-assl.md), [TableID](../../../analysis-services/scripting/properties/tableid-element-assl.md)|  
|Elementos derivados|Consulte [Binding](../../../analysis-services/scripting/data-type/binding-data-type-assl.md)|  
  
## <a name="remarks"></a>Remarks  
 Para obter informações adicionais sobre o **associação** tipo, incluindo tabelas de objetos do Analysis Services Scripting Language (ASSL) da **associação** tipo e a hierarquia de herança de  **Associação** tipos, consulte [associação](../../../analysis-services/scripting/data-type/binding-data-type-assl.md) elemento.  
  
 Para obter uma visão geral de associações de dados em ASSL, consulte [fontes de dados e associações & #40; SSAS Multidimensional & #41; ](../../../analysis-services/multidimensional-models/data-sources-and-bindings-ssas-multidimensional.md).  
  
 O elemento correspondente no modelo de objeto Analysis Management Objects (AMO) é <xref:Microsoft.AnalysisServices.DSVTableBinding>.  
  
## <a name="see-also"></a>Consulte também  
 [Tipos de dados XML de linguagem de script & #40; do Analysis Services ASSL & #41;](../../../analysis-services/scripting/data-type/analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
