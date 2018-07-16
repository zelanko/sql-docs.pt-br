---
title: Tipo de dados assembly (ASSL) | Microsoft Docs
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
- Assembly Data Type
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
helpviewer_keywords:
- Assembly data type
ms.assetid: 0a381322-9509-4579-a754-c6cdd0a70cc9
caps.latest.revision: 16
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 40cafd0d8ef11feaebce5161e97ef3717a9fb943
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37233824"
---
# <a name="assembly-data-type-assl"></a>Tipo de dados Assembly (ASSL)
  Define um tipo de dados primitivo abstrato que representa uma [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] assembly ou uma biblioteca de vínculo dinâmico (DLL) COM associado com um [Server](../objects/server-element-assl.md) ou [banco de dados](../objects/database-element-assl.md) elemento.  
  
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
|Tipos de dados derivados|[ClrAssembly](assembly-data-type-assl.md), [ComAssembly](comassembly-data-type-assl.md)|  
  
## <a name="data-type-relationships"></a>Relação do tipo de dados  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|Nenhum|  
|Elementos filho|[Anotações](../collections/annotations-element-assl.md), [CreatedTimestamp](../properties/createdtimestamp-element-assl.md), [descrição](../properties/description-element-assl.md), [ID](../properties/id-element-assl.md), [ImpersonationInfo](../properties/impersonationinfo-element-assl.md), [ LastSchemaUpdate](../properties/lastschemaupdate-element-assl.md), [nome](../properties/name-element-assl.md)|  
|Elementos derivados|Nenhum|  
  
## <a name="remarks"></a>Remarks  
 O tipo de dados `Assembly` serve como o tipo de dados base para o elemento `ComAssembly`, que representa as bibliotecas COM associadas à instância ou ao banco de dados, e o elemento `ClrAssembly`, que representa os assemblies [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] associados à instância ou ao banco de dados. Para obter mais informações sobre assemblies, consulte [gerenciamento de Assemblies de modelo Multidimensional](../../multidimensional-models/multidimensional-model-assemblies-management.md).  
  
 O elemento correspondente no modelo de objeto Analysis Management Objects (AMO) é <xref:Microsoft.AnalysisServices.Assembly>.  
  
## <a name="see-also"></a>Consulte também  
 [Elemento de servidor &#40;ASSL&#41;](../objects/server-element-assl.md)   
 [Elemento de banco de dados &#40;ASSL&#41;](../objects/database-element-assl.md)   
 [Tipos de dados XML de linguagem script do Analysis Services &#40;ASSL&#41;](analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
