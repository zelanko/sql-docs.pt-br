---
title: Tipo de dados DataBlock (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- DataBlock Data Type
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- DataBlock
helpviewer_keywords:
- DataBlock data type
ms.assetid: 4192b388-613a-472b-881c-f9c02215aa81
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 706b934c51d280ec588bedf3752d61a4cc46697d
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48082586"
---
# <a name="datablock-data-type-assl"></a>Tipo de dados DataBlock (ASSL)
  Define um tipo de dados primitivo que representa uma coleção de blocos de dados usado para armazenar o conteúdo binário de um [ClrAssemblyFile](clrassemblyfile-data-type-assl.md) elemento.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<DataBlock>  
   <Blocks>...</Blocks>  
</DataBlock>  
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
|Elementos filho|[Blocos](../collections/blocks-element-assl.md)|  
|Elementos derivados|[Dados](../objects/data-element-assl.md) elemento de [ClrAssemblyFile](clrassemblyfile-data-type-assl.md) tipo ([arquivos](../collections/files-element-assl.md) coleção de [ClrAssembly](assembly-data-type-assl.md) tipo)|  
  
## <a name="see-also"></a>Consulte também  
 [Elemento assembly &#40;ASSL&#41;](../objects/assembly-element-assl.md)   
 [Elemento de arquivo &#40;ASSL&#41;](../objects/file-element-assl.md)   
 [Bloquear o elemento &#40;ASSL&#41;](../objects/block-element-assl.md)   
 [Tipos de dados XML de linguagem script do Analysis Services &#40;ASSL&#41;](analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
