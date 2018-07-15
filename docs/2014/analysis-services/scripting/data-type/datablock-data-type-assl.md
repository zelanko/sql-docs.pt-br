---
title: Tipo de dados DataBlock (ASSL) | Microsoft Docs
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
caps.latest.revision: 32
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 167af587de6f06d283ec29f8afbc0fedb2ebc99e
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37211956"
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
|Tipos de dados base|Nenhum|  
|Tipos de dados derivados|Nenhum|  
  
## <a name="data-type-relationships"></a>Relação do tipo de dados  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|Nenhum|  
|Elementos filho|[Blocos](../collections/blocks-element-assl.md)|  
|Elementos derivados|[Dados](../objects/data-element-assl.md) elemento de [ClrAssemblyFile](clrassemblyfile-data-type-assl.md) tipo ([arquivos](../collections/files-element-assl.md) coleção de [ClrAssembly](assembly-data-type-assl.md) tipo)|  
  
## <a name="see-also"></a>Consulte também  
 [Elemento assembly &#40;ASSL&#41;](../objects/assembly-element-assl.md)   
 [Elemento de arquivo &#40;ASSL&#41;](../objects/file-element-assl.md)   
 [Bloquear o elemento &#40;ASSL&#41;](../objects/block-element-assl.md)   
 [Tipos de dados XML de linguagem script do Analysis Services &#40;ASSL&#41;](analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
