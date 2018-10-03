---
title: Elemento Data (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- Data Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- Data
helpviewer_keywords:
- Data element
ms.assetid: e52b1961-7e11-4029-8ab1-84d275845067
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 57958cfe25563b4a7e2fd53f639d3bc289dce07c
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48117344"
---
# <a name="data-element-assl"></a>Elemento Data (ASSL)
  Contém (na coleção de filhos [elemento de bloco &#40;ASSL&#41; ](block-element-assl.md) elementos) o conteúdo binário de um [ClrAssemblyFile](../data-type/clrassemblyfile-data-type-assl.md) elemento.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<File xsi:type="ClrAssemblyFile">  
   ...  
   <Data xsi:type="DataBlock">...</Data>  
   ...  
</ClrAssemblyFile>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Description|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|[DataBlock](../data-type/datablock-data-type-assl.md)|  
|Valor padrão|None|  
|Cardinalidade|1-1: elemento obrigatório que ocorre apenas uma única vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[Arquivo](file-element-assl.md) do tipo [ClrAssemblyFile](../data-type/clrassemblyfile-data-type-assl.md)|  
|Elementos filho|None|  
  
## <a name="remarks"></a>Comentários  
 O elemento que corresponde ao pai de `Data` no objeto Analysis Management Objects (AMO) o modelo é <xref:Microsoft.AnalysisServices.ClrAssemblyFile>.  
  
## <a name="see-also"></a>Consulte também  
 [Elemento assembly &#40;ASSL&#41;](assembly-element-assl.md)   
 [Tipo de dados ClrAssembly &#40;ASSL&#41;](../data-type/assembly-data-type-assl.md)   
 [Arquivos de elemento &#40;ASSL&#41;](../collections/files-element-assl.md)   
 [Bloqueia o elemento &#40;ASSL&#41;](../collections/blocks-element-assl.md)   
 [Objetos &#40;ASSL&#41;](objects-assl.md)  
  
  
