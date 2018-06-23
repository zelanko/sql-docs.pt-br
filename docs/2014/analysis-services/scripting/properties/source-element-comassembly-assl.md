---
title: Fonte do elemento (ComAssembly) (ASSL) | Microsoft Docs
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
- Source Element (ComAssembly)
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- Source
helpviewer_keywords:
- Source element
ms.assetid: 5c9209e8-ace6-4688-a64d-4987a7648ab9
caps.latest.revision: 38
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: ae014f12e15dd27957ab77eb03720457f3c99b28
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36117038"
---
# <a name="source-element-comassembly-assl"></a>Elemento Source (ComAssembly) (ASSL)
  Contém o nome de arquivo ou identificador programático (ProgID) para um componente COM (Component Object Model).  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<ComAssembly>  
   ...  
   <Source>...</Source>  
   ...  
</ComAssembly>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Description|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Cadeia de caracteres|  
|Valor padrão|Nenhum|  
|Cardinalidade|0-1: elemento opcional que pode ocorrer apenas uma única vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elemento pai|[ComAssembly](../data-type/assembly-data-type-assl.md)|  
|Elementos filho|Nenhum|  
  
## <a name="remarks"></a>Remarks  
 O elemento que corresponde ao pai do `Source` no objeto Analysis Management Objects (AMO) o modelo é <xref:Microsoft.AnalysisServices.ComAssembly>.  
  
## <a name="see-also"></a>Consulte também  
 [Elemento assembly &#40;ASSL&#41;](../objects/assembly-element-assl.md)   
 [Tipo de dados ClrAssembly &#40;ASSL&#41;](../data-type/clrassembly-data-type-assl.md)   
 [Elemento assemblies &#40;ASSL&#41;](../collections/assemblies-element-assl.md)   
 [Elemento de banco de dados &#40;ASSL&#41;](../objects/database-element-assl.md)   
 [Elemento Server &#40;ASSL&#41;](../objects/server-element-assl.md)   
 [Propriedades &#40;ASSL&#41;](properties-assl.md)  
  
  