---
title: Tipo de dados ComAssembly (ASSL) | Microsoft Docs
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: assl
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: b01a29856bf42d275b1c4d59c9041a9f6f4ab270
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/10/2018
---
# <a name="comassembly-data-type-assl"></a>Tipo de dados ComAssembly (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Define um tipo de dados derivado que representa uma biblioteca COM associada a um elemento [Server](../../../analysis-services/scripting/objects/server-element-assl.md) ou [Database](../../../analysis-services/scripting/objects/database-element-assl.md) .  
  
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
  
|Característica|Descrição|  
|--------------------|-----------------|  
|Tipos de dados base|[Assembly](../../../analysis-services/scripting/objects/assembly-element-assl.md)|  
|Tipos de dados derivados|Nenhuma|  
  
## <a name="data-type-relationships"></a>Relação do tipo de dados  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|Nenhuma|  
|Elementos filho|[Origem](../../../analysis-services/scripting/properties/source-element-comassembly-assl.md)|  
|Elementos derivados|Consulte [Assembly](../../../analysis-services/scripting/objects/assembly-element-assl.md) (coleção[Assemblies](../../../analysis-services/scripting/collections/assemblies-element-assl.md) de [Database](../../../analysis-services/scripting/objects/database-element-assl.md) ou [Server](../../../analysis-services/scripting/objects/server-element-assl.md))|  
  
## <a name="remarks"></a>Remarks  
 O **ComAssembly** elemento contém uma referência (o nome de arquivo totalmente qualificado ou o identificador programático) a uma biblioteca COM associada a uma instância de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] ou com um determinado banco de dados em uma instância do [!INCLUDE[ssAS](../../../includes/ssas-md.md)].  
  
 O elemento correspondente no modelo de objeto Analysis Management Objects (AMO) é <xref:Microsoft.AnalysisServices.ComAssembly>.  
  
## <a name="see-also"></a>Consulte também  
 [Tipo de dados ClrAssembly &#40;ASSL&#41;](../../../analysis-services/scripting/data-type/clrassembly-data-type-assl.md)   
 [Tipos de dados XML de linguagem de script & #40; do Analysis Services ASSL & #41;](../../../analysis-services/scripting/data-type/analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
