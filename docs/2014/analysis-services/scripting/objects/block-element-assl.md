---
title: Bloquear elemento (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- Block Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- Block
helpviewer_keywords:
- Block element
ms.assetid: f45c32ae-e4e0-465a-9564-9ccfb10a858f
caps.latest.revision: 36
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 44022a2e0bd538b7f4b33b0d1f1fb7b462e676e6
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37279432"
---
# <a name="block-element-assl"></a>Elemento Block (ASSL)
  Contém todo ou parte do conteúdo binário de um [ClrAssemblyFile](../data-type/clrassemblyfile-data-type-assl.md) elemento.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<Blocks>  
   <Block>...</Block>  
</Blocks>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Description|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Base64Binary|  
|Valor padrão|Nenhum|  
|Cardinalidade|1-n: elemento obrigatório que pode ocorrer mais de uma vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[Blocos](../collections/blocks-element-assl.md)|  
|Elementos filho|Nenhum|  
  
## <a name="see-also"></a>Consulte também  
 [Elemento assembly &#40;ASSL&#41;](assembly-element-assl.md)   
 [Tipo de dados ClrAssembly &#40;ASSL&#41;](../data-type/assembly-data-type-assl.md)   
 [Arquivos de elemento &#40;ASSL&#41;](../collections/files-element-assl.md)   
 [Elemento de arquivo &#40;ASSL&#41;](file-element-assl.md)   
 [Tipo de dados ClrAssemblyFile &#40;ASSL&#41;](../data-type/clrassemblyfile-data-type-assl.md)   
 [Elemento de dados &#40;ASSL&#41;](data-element-assl.md)   
 [Tipo de dados DataBlock &#40;ASSL&#41;](../data-type/datablock-data-type-assl.md)   
 [Objetos &#40;ASSL&#41;](objects-assl.md)  
  
  
