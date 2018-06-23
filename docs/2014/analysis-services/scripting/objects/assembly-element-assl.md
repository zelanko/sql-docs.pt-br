---
title: Elemento Assembly (ASSL) | Microsoft Docs
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
- Assembly Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- ASSEMBLY
helpviewer_keywords:
- Assembly element [ASSL]
ms.assetid: 1910ccb0-7da0-4ee1-9548-ad6e0068d23d
caps.latest.revision: 34
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 02bc362fd633a7c3cf9fcd4936d2a0580753c01b
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36008281"
---
# <a name="assembly-element-assl"></a>Elemento Assembly (ASSL)
  Representa um [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] assembly ou uma biblioteca de vínculo dinâmico (DLL) COM associado com um [servidor](server-element-assl.md) elemento ou um [banco de dados](database-element-assl.md) elemento.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<Assemblies>  
   <Assembly xsi:type="ClrAssembly">...</Assembly>  
   <!-- or -->  
   <Assembly xsi:type="ComAssembly">...</Assembly>  
</Assemblies>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Description|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|[ClrAssembly](../data-type/assembly-data-type-assl.md), [ComAssembly](../data-type/comassembly-data-type-assl.md)|  
|Valor padrão|Nenhum|  
|Cardinalidade|0-n: Elemento opcional que pode ocorrer mais de uma vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[Assemblies](../collections/assemblies-element-assl.md)|  
|Elementos filho|Nenhum|  
  
## <a name="remarks"></a>Remarks  
 O elemento correspondente no modelo de objeto Analysis Management Objects (AMO) é <xref:Microsoft.AnalysisServices.Assembly>.  
  
## <a name="see-also"></a>Consulte também  
 [Elemento Server &#40;ASSL&#41;](server-element-assl.md)   
 [Elemento de banco de dados &#40;ASSL&#41;](database-element-assl.md)   
 [Objetos &#40;ASSL&#41;](objects-assl.md)  
  
  