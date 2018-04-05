---
title: Tipo de dados assembly (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
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
- Assembly Data Type
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- Assembly data type
ms.assetid: 0a381322-9509-4579-a754-c6cdd0a70cc9
caps.latest.revision: 16
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 34af3fd4c829b78c52370ee7aa73d4ed16c17fb9
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/08/2018
---
# <a name="assembly-data-type-assl"></a>Tipo de dados Assembly (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]Define um tipo de dados primitivo abstrato que representa um [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] assembly ou uma biblioteca de vínculo dinâmico (DLL) COM associado com um [servidor](../../../analysis-services/scripting/objects/server-element-assl.md) ou [banco de dados](../../../analysis-services/scripting/objects/database-element-assl.md) elemento.  
  
> [!IMPORTANT]  
>  Os assemblies COM podem representar um risco à segurança. Devido a esse risco e outras considerações, os assemblies COM foram preteridos no [!INCLUDE[ssASversion10](../../../includes/ssasversion10-md.md)]. Talvez não haja suporte para assemblies COM em versões futuras.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<Assembly>  
   <Name>...</Name>  
   <ID>...</ID>  
   <Description>...</Description>  
   <CreatedTimestamp>...</CreatedTimestamp>  
   <LastSchemaUpdate>...</LastSchemaUpdate>  
   <ImpersonationInfo>...</ImpersonationInfo>  
   <Annotations>...</Annotations>  
</Assembly>  
```  
  
## <a name="data-type-characteristics"></a>Características do tipo de dados  
  
|Característica|Description|  
|--------------------|-----------------|  
|Tipos de dados base|Nenhum|  
|Tipos de dados derivados|[ClrAssembly](../../../analysis-services/scripting/data-type/clrassembly-data-type-assl.md), [ComAssembly](../../../analysis-services/scripting/data-type/comassembly-data-type-assl.md)|  
  
## <a name="data-type-relationships"></a>Relação do tipo de dados  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|Nenhum|  
|Elementos filho|[Anotações](../../../analysis-services/scripting/collections/annotations-element-assl.md), [CreatedTimestamp](../../../analysis-services/scripting/properties/createdtimestamp-element-assl.md), [descrição](../../../analysis-services/scripting/properties/description-element-assl.md), [ID](../../../analysis-services/scripting/properties/id-element-assl.md), [ImpersonationInfo](../../../analysis-services/scripting/properties/impersonationinfo-element-assl.md), [ LastSchemaUpdate](../../../analysis-services/scripting/properties/lastschemaupdate-element-assl.md), [nome](../../../analysis-services/scripting/properties/name-element-assl.md)|  
|Elementos derivados|Nenhum|  
  
## <a name="remarks"></a>Remarks  
 O **Assembly** tipo de dados serve como o tipo de dados base para o **ComAssembly** elemento, que representa as bibliotecas associadas com a instância ou banco de dados, e o **ClrAssembly** elemento, que representa [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] assemblies associados com a instância ou banco de dados. Para obter mais informações sobre assemblies, consulte [gerenciamento de Assemblies de modelo Multidimensional](../../../analysis-services/multidimensional-models/multidimensional-model-assemblies-management.md).  
  
 O elemento correspondente no modelo de objeto Analysis Management Objects (AMO) é <xref:Microsoft.AnalysisServices.Assembly>.  
  
## <a name="see-also"></a>Consulte Também  
 [Elemento Server &#40; ASSL &#41;](../../../analysis-services/scripting/objects/server-element-assl.md)   
 [Elemento de banco de dados &#40; ASSL &#41;](../../../analysis-services/scripting/objects/database-element-assl.md)   
 [Tipos de dados XML de linguagem de script &#40; do Analysis Services ASSL &#41;](../../../analysis-services/scripting/data-type/analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
