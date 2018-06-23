---
title: Arquivos de elemento (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- Files Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- Files
helpviewer_keywords:
- Files element
ms.assetid: 8a1327cb-1f60-42a7-b8ef-213d45a63e55
caps.latest.revision: 36
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 5f7556009881e1d4155e47a368bcff4b49aa7988
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36010110"
---
# <a name="files-element-assl"></a>Elemento Files (ASSL)
  Contém a coleção de [arquivo](../objects/file-element-assl.md) elementos que compõem um [ClrAssembly](../data-type/assembly-data-type-assl.md) elemento.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<Assembly xsi:type="ClrAssembly">  
   ...  
   <Files>  
      <File xsi:type="ClrAssemblyFile">...</File>  
   </Files>  
   ...  
</Assembly>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Description|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Nenhum|  
|Valor padrão|Nenhum|  
|Cardinalidade|1-1: elemento obrigatório que ocorre apenas uma única vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[Assembly](../objects/assembly-element-assl.md) do tipo [ClrAssembly](../data-type/assembly-data-type-assl.md)|  
|Elementos filho|[Arquivo](../objects/file-element-assl.md) do tipo [ClrAssemblyFile](../data-type/clrassemblyfile-data-type-assl.md)|  
  
## <a name="remarks"></a>Remarks  
 O elemento correspondente no modelo de objeto Analysis Management Objects (AMO) é <xref:Microsoft.AnalysisServices.ClrAssemblyFileCollection>.  
  
## <a name="see-also"></a>Consulte também  
 [Elemento Server &#40;ASSL&#41;](../objects/server-element-assl.md)   
 [Elemento de banco de dados &#40;ASSL&#41;](../objects/database-element-assl.md)   
 [Elemento assemblies &#40;ASSL&#41;](assemblies-element-assl.md)   
 [Elemento de dados &#40;ASSL&#41;](../objects/data-element-assl.md)   
 [Tipo de dados DataBlock &#40;ASSL&#41;](../data-type/datablock-data-type-assl.md)   
 [Bloqueia o elemento &#40;ASSL&#41;](blocks-element-assl.md)   
 [Bloquear elemento &#40;ASSL&#41;](../objects/block-element-assl.md)   
 [Tipo de dados ComAssembly &#40;ASSL&#41;](../data-type/comassembly-data-type-assl.md)   
 [Coleções &#40;ASSL&#41;](collections-assl.md)  
  
  