---
title: Elemento (ASSL) do arquivo | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- File Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- File
helpviewer_keywords:
- File element
ms.assetid: 21c70707-d2f8-4040-9acb-cbce23076bcc
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: ef9527346b0627d6ba414f9535c00e22a4d59ea6
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48169816"
---
# <a name="file-element-assl"></a>Elemento File (ASSL)
  Define um dos arquivos que compõem uma [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] [ClrAssembly](../data-type/assembly-data-type-assl.md) elemento.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<Files>  
   <File xsi:type="ClrAssemblyFile">...</File>  
</Files>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Description|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|[ClrAssemblyFile](../data-type/clrassemblyfile-data-type-assl.md)|  
|Valor padrão|None|  
|Cardinalidade|1-n: elemento obrigatório que pode ocorrer mais de uma vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[Arquivos](../collections/files-element-assl.md)|  
|Elementos filho|None|  
  
## <a name="remarks"></a>Comentários  
 O elemento que corresponde ao pai de `Files` no objeto Analysis Management Objects (AMO) o modelo é <xref:Microsoft.AnalysisServices.ClrAssemblyFile>.  
  
## <a name="see-also"></a>Consulte também  
 [Elemento de servidor &#40;ASSL&#41;](server-element-assl.md)   
 [Elemento de banco de dados &#40;ASSL&#41;](database-element-assl.md)   
 [Elemento assemblies &#40;ASSL&#41;](../collections/assemblies-element-assl.md)   
 [Elemento assembly &#40;ASSL&#41;](assembly-element-assl.md)   
 [Tipo de dados ClrAssembly &#40;ASSL&#41;](../data-type/assembly-data-type-assl.md)   
 [Elemento de dados &#40;ASSL&#41;](data-element-assl.md)   
 [Tipo de dados DataBlock &#40;ASSL&#41;](../data-type/datablock-data-type-assl.md)   
 [Bloqueia o elemento &#40;ASSL&#41;](../collections/blocks-element-assl.md)   
 [Bloquear o elemento &#40;ASSL&#41;](block-element-assl.md)   
 [Tipo de dados ComAssembly &#40;ASSL&#41;](../data-type/comassembly-data-type-assl.md)   
 [Objetos &#40;ASSL&#41;](objects-assl.md)  
  
  
