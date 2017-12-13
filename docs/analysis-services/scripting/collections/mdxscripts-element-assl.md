---
title: Elemento MdxScripts (ASSL) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname: MdxScripts Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: MdxScripts
helpviewer_keywords: MdxScripts element
ms.assetid: 0aaa849f-e723-4245-8c16-7ed049590fd2
caps.latest.revision: "34"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 6c071dd12d6f03415974e5226cd060e3107fb3c6
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/08/2017
---
# <a name="mdxscripts-element-assl"></a>Elemento MdxScripts (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]Contém a coleção de [MdxScript](../../../analysis-services/scripting/objects/mdxscript-element-assl.md) elementos associados a um [cubo](../../../analysis-services/scripting/objects/cube-element-assl.md) elemento.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<Cube>  
   ...  
   <MdxScripts>  
      <MdxScript>...</MdxScript>  
   </MdxScripts>  
   ...  
</Cube>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Descrição|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Nenhuma|  
|Valor padrão|Nenhuma|  
|Cardinalidade|0-1: elemento obrigatório que pode ocorrer apenas uma vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[Cube](../../../analysis-services/scripting/objects/cube-element-assl.md)|  
|Elementos filho|[MdxScript](../../../analysis-services/scripting/objects/mdxscript-element-assl.md)|  
  
## <a name="remarks"></a>Comentários  
 O elemento correspondente no modelo de objeto Analysis Management Objects (AMO) é <xref:Microsoft.AnalysisServices.MdxScriptCollection>.  
  
## <a name="see-also"></a>Consulte também  
 [Coleções de &#40; ASSL &#41;](../../../analysis-services/scripting/collections/collections-assl.md)  
  
  
