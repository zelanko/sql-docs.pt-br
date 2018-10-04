---
title: Tipo de dados ClrAssemblyFile (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- ClrAssemblyFile Data Type
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- ClrAssemblyFile
helpviewer_keywords:
- ClrAssemblyFile data type
ms.assetid: 91074677-c149-483b-a56d-0e35d959d9eb
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 700043163aad280f903731a96c4e851e902a5ae0
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48106516"
---
# <a name="clrassemblyfile-data-type-assl"></a>Tipo de dados ClrAssemblyFile (ASSL)
  Define um tipo de dados primitivo que representa um dos arquivos que compõem uma [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] `Assembly` ([ClrAssembly](assembly-data-type-assl.md) elemento).  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<ClrAssemblyFile>  
   <Name>...</Name>  
      <Type>...</Type>  
      <Data>...</Data>  
</ClrAssemblyFile>  
```  
  
## <a name="data-type-characteristics"></a>Características do tipo de dados  
  
|Característica|Description|  
|--------------------|-----------------|  
|Tipos de dados base|None|  
|Tipos de dados derivados|None|  
  
## <a name="data-type-relationships"></a>Relação do tipo de dados  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|None|  
|Elementos filho|[Dados](../objects/data-element-assl.md), [nome](../properties/name-element-assl.md), [tipo](../properties/type-element-clrassemblyfile-assl.md)|  
|Elementos derivados|[Arquivo](../objects/file-element-assl.md) ([arquivos](../collections/files-element-assl.md) coleção de [ClrAssembly](assembly-data-type-assl.md))|  
  
## <a name="remarks"></a>Comentários  
 O elemento correspondente no modelo de objeto Analysis Management Objects (AMO) é <xref:Microsoft.AnalysisServices.ClrAssemblyFile>.  
  
## <a name="see-also"></a>Consulte também  
 [Elemento de servidor &#40;ASSL&#41;](../objects/server-element-assl.md)   
 [Elemento de banco de dados &#40;ASSL&#41;](../objects/database-element-assl.md)   
 [Elemento assemblies &#40;ASSL&#41;](../collections/assemblies-element-assl.md)   
 [Elemento assembly &#40;ASSL&#41;](../objects/assembly-element-assl.md)   
 [Tipo de dados DataBlock &#40;ASSL&#41;](datablock-data-type-assl.md)   
 [Bloqueia o elemento &#40;ASSL&#41;](../collections/blocks-element-assl.md)   
 [Bloquear o elemento &#40;ASSL&#41;](../objects/block-element-assl.md)   
 [Tipo de dados ComAssembly &#40;ASSL&#41;](comassembly-data-type-assl.md)   
 [Tipos de dados XML de linguagem script do Analysis Services &#40;ASSL&#41;](analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
