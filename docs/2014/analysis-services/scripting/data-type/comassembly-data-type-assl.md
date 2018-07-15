---
title: Tipo de dados ComAssembly (ASSL) | Microsoft Docs
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
- ComAssembly Data Type
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- ComAssembly
helpviewer_keywords:
- ComAssembly data type
ms.assetid: 23c0f4b3-b6ac-4ec8-9254-74d2f84f5244
caps.latest.revision: 49
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 824fb508bb392f6ef84ede39645a5bac0da645e6
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37171547"
---
# <a name="comassembly-data-type-assl"></a>Tipo de dados ComAssembly (ASSL)
  Define um tipo de dados derivado que representa uma biblioteca COM associada com um [Server](../objects/server-element-assl.md) ou [banco de dados](../objects/database-element-assl.md) elemento.  
  
> [!IMPORTANT]  
>  Os assemblies COM podem representar um risco à segurança. Devido a esse risco e outras considerações, os assemblies COM foram preteridos no [!INCLUDE[ssASversion10](../../../includes/ssasversion10-md.md)]. Talvez não haja suporte para assemblies COM em versões futuras.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<ComAssembly>  
      <!-- The following elements extend Assembly -->  
   <Source>...</Source>  
</ComAssembly>  
```  
  
## <a name="data-type-characteristics"></a>Características do tipo de dados  
  
|Característica|Description|  
|--------------------|-----------------|  
|Tipos de dados base|[Assembly](../objects/assembly-element-assl.md)|  
|Tipos de dados derivados|Nenhum|  
  
## <a name="data-type-relationships"></a>Relação do tipo de dados  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|Nenhum|  
|Elementos filho|[Origem](../properties/source-element-comassembly-assl.md)|  
|Elementos derivados|Ver [Assembly](../objects/assembly-element-assl.md) ([Assemblies](../collections/assemblies-element-assl.md) coleção de [banco de dados](../objects/database-element-assl.md) ou [Server](../objects/server-element-assl.md))|  
  
## <a name="remarks"></a>Remarks  
 O `ComAssembly` elemento contém uma referência (o nome de arquivo totalmente qualificado ou o identificador programático) a uma biblioteca COM associada a uma instância do [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] ou com um banco de dados específico em uma instância do [!INCLUDE[ssAS](../../../includes/ssas-md.md)].  
  
 O elemento correspondente no modelo de objeto Analysis Management Objects (AMO) é <xref:Microsoft.AnalysisServices.ComAssembly>.  
  
## <a name="see-also"></a>Consulte também  
 [Tipo de dados ClrAssembly &#40;ASSL&#41;](assembly-data-type-assl.md)   
 [Tipos de dados XML de linguagem script do Analysis Services &#40;ASSL&#41;](analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
